---
name: circuitjs
description: Reference for CircuitJS1 (pfalstad/circuitjs1) — circuit file format (text and XML), embedding via iframe/query params, the JavaScript and WebSocket APIs, and build/deployment. Use when creating, parsing, converting, or debugging CircuitJS1 circuit files, or embedding/scripting/deploying the simulator.
---

# CircuitJS1 Reference

Reference for [CircuitJS1](https://github.com/pfalstad/circuitjs1), the browser-based electronic circuit simulator: its circuit file format, embedding, scripting APIs, and deployment.

## Hosted versions

For a hosted version of the application (e.g. to generate a `cct=`/`ctz=` link or embed via iframe without deploying your own copy — see [embedding.md](reference/embedding.md)):

- **Paul's Page**: http://www.falstad.com/circuit/
- **Iain's Page**: http://lushprojects.com/circuitjs/
- **Development Branch Version**: https://pfalstad.github.io/circuitjs1/circuitjs.html

CircuitJS1 circuits are stored in two primary formats:

- **Text format** — human-readable, space-delimited, also the compressed form used in URLs. Still fully supported for hand-authoring and import.
- **XML format** — internal format for undo/redo and storage, more robust, preserves all state. Used by the WebSocket API and local storage.

Import auto-detects which one you're feeding it: `CircuitLoader.readCircuit()` checks whether the string starts with `<` — if so it parses XML, otherwise the flat text format — so both are valid input to "Import from Text" or a loaded file. Note that on current builds, the "Export as Text" dialog and the `cct=`/`ctz=` URL export both actually emit **XML** (they call the same internal `dumpCircuit()` used for undo/redo).

**In this skill, prefer the XML format over plain text** when generating, writing, or hand-authoring circuits — it's what current builds actually export/import, is more robust (preserves all state, no positional-field guessing), and is straightforward to build with a standard XML library instead of string-joining. See [xml-format.md](reference/xml-format.md) first. The flat text format is documented for reading/parsing legacy `.txt` circuit files and older worked examples, not as the preferred output format.

## Text file skeleton

```
$ <flags> <maxTimeStep> <iterCount> <currentBar> <voltageRange> <powerBar> <minTimeStep>
<element-line-1>
<element-line-2>
...
```

Each element line: `<dump-type> <x> <y> <x2> <y2> <flags> [element-specific-data...]`. Coordinates are pixel ints on an 8px grid, origin top-left.

## Quick dump-type lookup

| Type | Element | Type | Element |
|------|---------|------|---------|
| `r` | Resistor | `w` | Wire |
| `c` | Capacitor | `g` | Ground |
| `l` (lowercase) | Inductor | `n` | Noise Source (legacy text type) |
| `L` (uppercase) | Logic Input | `s` (lowercase) | Switch (SPST) |
| `v` | Voltage Source (DC/AC/etc., see waveform field) | `S` (uppercase) | Switch (SPDT) |
| `a` | Op-Amp | `d` | Diode |
| `i` | Current Source | `t` | Transistor (NPN/PNP) |
| `207` (text) / `<ln>` (XML) | Labeled Node | `429` | DPDT Switch |
| `403` | Scope | `432` | Analog Mux |
| `210` | Data Recorder | `O` | Output (test point) |
| `164` | Counter (up/down) | `421` | Counter (simple) |

## Reference files

Load only what the task needs:

- [reference/xml-format.md](reference/xml-format.md) — XML structure, attribute mapping, element type names — **preferred format, start here for generation**
- [reference/text-format.md](reference/text-format.md) — full options-line spec, flags breakdown, element-line format, coordinate system — for parsing/importing legacy text circuits
- [reference/elements.md](reference/elements.md) — full element-by-element syntax reference (resistor, sources, switches, chips, wires, scope, etc.) plus the dump-type → class map (shared by both formats)
- [reference/examples.md](reference/examples.md) — categorized index into [examples/](examples/), the library of ~370 real circuits mirrored from the upstream repo — see "Example circuit library" below
- [reference/working-with-files.md](reference/working-with-files.md) — Python load/save helpers (XML-first, text-format fallback), label escaping, LZString URL compression
- [reference/embedding.md](reference/embedding.md) — iframe embedding, startup query parameters (`ctz`, `startCircuit`, colors, `mouseMode`, etc.), the full `CircuitJS1` JS interface (methods, callbacks, per-element accessors), and building an Electron desktop app
- [reference/apis-and-tools.md](reference/apis-and-tools.md) — JS export API summary, full WebSocket JSON-command API, validation checklist, tips for portability/debugging, source file pointers
- [reference/deployment.md](reference/deployment.md) — building CircuitJS1 itself (Eclipse, Gradle, cloud dev containers, Docker/Podman) and deploying a compiled instance (file layout, `shortrelay.php`, Dropbox key)

## Example circuit library

[examples/](examples/) mirrors the ~370 example circuits shipped with the upstream repo (`src/com/lushprojects/circuitjs1/public/circuits/`), verbatim, in the legacy text format. Use [reference/examples.md](reference/examples.md) — a categorized, searchable index (Basics, A/C Circuits, Filters, Op-Amps, Digital Logic, Oscillators, etc.) — to find a real circuit close to what's being built, for inspiration or to reuse/adapt directly instead of authoring from scratch. When reusing one as output, prefer converting it to XML per this skill's format preference rather than emitting the text form as-is.

## Round-tripping

When generating circuits programmatically: build the `<cir>` root + element tags per [xml-format.md](reference/xml-format.md), validate against the checklist in [apis-and-tools.md](reference/apis-and-tools.md), and confirm with an export → import → export round trip.

## Embedding quick start

```html
<iframe id="circuitFrame" src="circuitjs.html?startCircuit=default.txt&hideSidebar=true"></iframe>
```
Same-origin iframe → `iframe.contentWindow.CircuitJS1` exposes `exportCircuit()`, `importCircuit()`, `getElements()`, `setExtVoltage()`, `getNodeVoltage()`, and `onupdate`/`ontimestep`/`onanalyze` callbacks. Full detail in [embedding.md](reference/embedding.md).
