# Embedding CircuitJS1

Source: [pfalstad/circuitjs1 README](https://github.com/pfalstad/circuitjs1), "Embedding" section, plus the actual `JSInterface.java` / `CircuitElm.java` GWT source (ground truth for the JS API below).

## Linking vs. embedding

- **Link** to the full-page app: `http://<host>/<path>/circuitjs.html`.
- **Embed** it in another page with an `<iframe>` whose `src` is that same full-page URL. This is also the only supported way to reach the JS interface (same-origin iframe).

## Startup query parameters

Append these to `circuitjs.html?...` to control startup behavior:

| Parameter | Effect |
|---|---|
| `cct=<string>` | Load the circuit from the URL (like `#` in the old Java version) |
| `ctz=<string>` | Load the circuit from **compressed** data in the URL (LZString — see [working-with-files.md](working-with-files.md)) |
| `startCircuit=<filename>` | Load circuit `filename` from the `circuits` directory |
| `startCircuitLink=<URL>` | Load a circuit from a URL — must support CORS (e.g. a Dropbox shared file) |
| `euroResistors=true` | Force "Euro" style resistors (default: based on browser language) |
| `usResistors=true` | Force "US" style resistors (default: based on browser language) |
| `IECGates=true` | Force IEC logic gate symbols (default: based on browser language) |
| `whiteBackground=<true\|false>` | White background instead of black |
| `conventionalCurrent=<true\|false>` | Current direction convention |
| `running=<true\|false>` | Start with simulation running (default `true`) |
| `hideSidebar=<true\|false>` | Hide the sidebar (default `false`) |
| `hideMenu=<true\|false>` | Hide the menu (default `false`) |
| `editable=<true\|false>` | Allow circuit editing (default `true`) |
| `positiveColor=%23rrggbb` | Positive voltage color |
| `negativeColor=%23rrggbb` | Negative voltage color |
| `selectColor=%23rrggbb` | Selection color |
| `currentColor=%23rrggbb` | Current-flow color |
| `mouseWheelEdit=<true\|false>` | Allow changing element values with the mouse wheel |
| `mouseMode=<item>` | Set the initial mouse mode; can also trigger startup UI actions (e.g. opening "about", `importfromlocalfile`) |
| `hideInfoBox=<true\|false>` | Hide the element info box |

Colors are URL-encoded hex (`#` → `%23`).

**Example:**
```
circuitjs.html?startCircuit=default.txt&hideSidebar=true&editable=false&whiteBackground=true
```

## JavaScript interface

Requires the host page and the iframe to be **same-origin**. Set a load hook before the iframe's `CircuitJS1` global exists, then grab it once ready:

```html
<iframe id="circuitFrame" width="800" height="550" src="circuitjs.html?startCircuit=jsinterface.txt"></iframe>
<script>
var iframe = document.getElementById("circuitFrame");
var sim;

function simLoaded() {
  sim = iframe.contentWindow.CircuitJS1;
  sim.onupdate = didUpdate;     // called on every display update
  sim.ontimestep = didStep;     // called every simulation timestep
  sim.onanalyze = didAnalyze;   // called when the circuit is (re)loaded or edited
  sim.onsvgrendered = svgRendered; // called after getCircuitAsSVG() finishes
}
iframe.contentWindow.oncircuitjsloaded = simLoaded;
</script>
```

### `CircuitJS1` global object

| Method | Signature | Notes |
|---|---|---|
| `setSimRunning(run)` | `(boolean) → void` | Start/stop the simulation |
| `isRunning()` | `() → boolean` | |
| `getTime()` | `() → double` | Simulation time in seconds |
| `getTimeStep()` | `() → double` | |
| `setTimeStep(ts)` | `(double) → void` | Discouraged — see upstream issue #843 |
| `getMaxTimeStep()` | `() → double` | |
| `setMaxTimeStep(ts)` | `(double) → void` | Also resets `timeStep` to `ts` |
| `getNodeVoltage(name)` | `(string) → double` | Voltage of a labeled node (see [Labeled Node](elements.md)) |
| `setExtVoltage(name, v)` | `(string, double) → void` | Sets the voltage of an `ExtVoltageElm` (external voltage source) matching `name` |
| `getElements()` | `() → Element[]` | Array of live element wrapper objects, see below |
| `exportCircuit()` | `() → string` | Dumps the circuit in [text format](text-format.md) |
| `importCircuit(text, subcircuitsOnly)` | `(string, boolean) → void` | Loads a circuit from text; `subcircuitsOnly` imports only its subcircuit definitions into the current circuit instead of replacing it |
| `getCircuitAsSVG()` | `() → void` | Renders async; result arrives via the `onsvgrendered(sim, svgString)` callback, not a return value |

### Callbacks (assign as properties on the `CircuitJS1` object)

| Callback | Fires |
|---|---|
| `oncircuitjsloaded(CircuitJS1)` | Set on `iframe.contentWindow` *before* the iframe finishes loading — called once the app is ready |
| `onupdate(sim)` | Every display refresh |
| `ontimestep(sim)` | Every simulation timestep |
| `onanalyze(sim)` | Whenever the circuit is loaded or edited (topology re-analyzed) |
| `onsvgrendered(sim, svgString)` | After `getCircuitAsSVG()` finishes |

### Per-element methods (each item from `getElements()`)

| Method | Signature | Notes |
|---|---|---|
| `getType()` | `() → string` | Class name, e.g. `"ResistorElm"` |
| `getInfo()` | `() → string` | Same multi-line info text shown in the element's popup |
| `getPostCount()` | `() → int` | Number of connection points |
| `getVoltageDiff()` | `() → double` | Voltage across a two-terminal element |
| `getVoltage(n)` | `(int) → double` | Voltage at post `n` |
| `getCurrent()` | `() → double` | Current through the element (amps) |
| `getLabelName()` | `() → string` | Only meaningful on `LabeledNodeElm` |

Full worked example: `war/jsinterface.html` in the upstream repo.

## Building an Electron desktop app

1. Compile the web app with GWT as usual (`./dev.sh compile` or the Eclipse GWT compile).
2. Download a pre-built Electron binary (tested with v9.3.2) for the target platform.
3. Copy this repo's `app` directory into the Electron binary directory per [Electron's application-distribution docs](https://electronjs.org/docs/tutorial/application-distribution).
4. Copy the compiled `war` directory into that same `app` directory.
5. Run the `Electron` executable — it loads CircuitJS1 automatically.

**Known limitation:** "Create short URL" under "Export as URL" doesn't work in the Electron build (it depends on server-side relay support — see `shortrelay.php` in [apis-and-tools.md](apis-and-tools.md)).
