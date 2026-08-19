# Tools and Utilities

### JavaScript Export API

Full API (methods, callbacks, per-element accessors) is documented in [embedding.md](embedding.md#javascript-interface) — requires embedding the app in a same-origin iframe. Quick taste:

```javascript
var circuitText = sim.exportCircuit();          // dump current circuit as text
sim.importCircuit(circuitText, false);           // load a circuit from text
sim.getElements().forEach(elem => {              // inspect live elements
    console.log(elem.getType(), elem.getInfo());
});
```

### WebSocket API

Source: `websocket/README.md` and `websocket/circuitws_server.py` in the upstream repo. A shim (`websocket/circuitws.html` + `circuitws.js`, copied into `war/`) connects the running simulator to a WebSocket endpoint and exchanges JSON commands — useful for driving/reading a browser-hosted simulation from any language.

**Setup:** serve `circuitws.html`/`circuitws.js` alongside the app, then open it with a `ws=` query param pointing at your WebSocket endpoint:
```
http://127.0.0.1:8123/circuitws.html?ws=ws%3A%2F%2F127.0.0.1%3A4444%2Fws
```
Optional params: `src=` (initial iframe `src`, defaults sensibly) and `autoshutoff` (shim shuts itself down after one connection closes — useful for short-lived servers).

**Command envelope** — every request needs `cmd`; `msgid` is optional but echoed back in the response so replies can be correlated even out-of-order:
```json
{ "cmd": "cmdname", "msgid": 1234, "...extra params": "..." }
```

**Supported commands:**

| Command | Purpose | Extra params |
|---|---|---|
| `status` | Query simulator state (`running`, `time`, `timestep`) | — |
| `set_running` | Start/stop the simulator | `state` (bool) |
| `reload` | Reload the iframe (source can't change) | `args` (dict of query params for the new iframe) |
| `set_timestamp` | Set the simulation timestep | `timestep` (double) |
| `get_node_voltage` | Query voltage of named labeled nodes | `nodes` (list of names) |
| `get_elements` | List all circuit elements | — |
| `set_ext_voltage` | Set external voltage source(s) | `voltages` (name→value dict) |
| `get_svg` | Render circuit as SVG | result arrives async as an `svg_rendered` event |
| `circuit_export` | Get the circuit in [text format](text-format.md) | — |
| `circuit_import` | Load a circuit from text | `circuit` (string) |

**Example response** (note the envelope: `type`, `status`, `cmd`, `msgid`, `data`):
```json
{"type": "response", "status": "ok", "cmd": "status", "msgid": 1,
 "data": {"running": true, "time": 1.0127750000024012, "timestep": 5e-06}}
```

**Try it locally** (needs Python 3.10+ and `aiohttp`): `python3 websocket/circuitws_server.py` serves the `war/` dir on `:8123` and opens a WS listener on `:8080` with an interactive CLI (`?`, `start`, `stop`, `svg`, `export`, `import`, `help`, `q`) for manually issuing commands while you watch the browser react.

---

## Validation Checklist

When creating circuits programmatically (XML preferred, see [xml-format.md](xml-format.md)):

- [ ] Root element is `<cir>` with the options attributes (`f`, `ts`, `ic`, `cb`, `vr`, `pb`, `mts`) — or, for hand-written text format, first line starts with `$`
- [ ] All coordinates are integers on grid (multiple of 8)
- [ ] Elements reference valid dump types / tag names
- [ ] Element flags (`f` attribute, or the flags field in text format) are valid integers (0-255 typical)
- [ ] Data values match element type expectations
- [ ] Special characters in labels are valid XML attribute text (or escape-sequence-encoded, for text format)
- [ ] At least one ground element present
- [ ] No duplicate element positions (usually)
- [ ] All wires properly connected

---

## Tips and Tricks

### Making Circuits Portable

1. Use relative coordinates from origin
2. Avoid hardcoded node references unless necessary
3. Document any custom parameters
4. Test round-trip: export → import → export

### Optimizing File Size

1. Omit XML attributes that just take their default value (or remove unnecessary spaces, for hand-written text format)
2. Use compression (LZString) for URLs
3. Minimize floating-point precision (3-4 decimals)
4. Remove whitespace/comments

### Debugging

1. Export circuit, examine the XML
2. Check element positions with GUI
3. Validate coordinate ranges
4. Use browser console for JavaScript debugging

---

## References

- **INTERNALS.md** (repo root): architecture and implementation details
- **war/jsinterface.html**: worked JavaScript API example (see [embedding.md](embedding.md))
- **websocket/README.md**: WebSocket protocol documentation (see above)
- Source files: `CircuitElm.java`, `CircuitLoader.java`, `XMLSerializer.java`, `XMLDeserializer.java`, `JSInterface.java`
