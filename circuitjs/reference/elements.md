# Element Reference

### Two-Terminal Linear Elements

#### Resistor
```
r <x> <y> <x2> <y2> <flags> <resistance>
```
- **dump-type**: `r` (114)
- **resistance**: Value in ohms (double)
- **flags**: No `FLAG_*` constants defined in `ResistorElm`; field is unused — always write `0`
- **Example**: `r 192 160 256 160 0 1000`

#### Capacitor
```
c <x> <y> <x2> <y2> <flags> <capacitance>
```
- **dump-type**: `c` (99)
- **capacitance**: Value in farads (double)
- **flags**: `FLAG_BACK_EULER` (2) — use backward-Euler integration instead of trapezoidal; `FLAG_RESISTANCE` (4) — an extra trailing series-resistance value follows the capacitance/state fields in the dump line (current builds always set this flag when dumping)
- **Example**: `c 192 224 256 224 0 0.001`

#### Inductor
```
l <x> <y> <x2> <y2> <flags> <inductance>
```
- **dump-type**: `l` (108, **lowercase L**) — not to be confused with Logic Input, which uses uppercase `L` (76); these are two separate dump-types, they don't collide
- **inductance**: Value in henries (double)
- **flags**: No `FLAG_*` constants defined in `InductorElm`
- **Example**: `l 192 288 256 288 0 0.1`

### Voltage/Current Sources

#### Voltage Source (DC/AC/square/triangle/sawtooth/pulse/noise)
```
v <x> <y> <x2> <y2> <flags> <waveform> <frequency> <max-voltage> <bias> <phase-shift> <duty-cycle>
```
- **dump-type**: `v` (118) — a single `VoltageElm` class backs every waveform; the waveform is a parameter, not a separate dump type
- **waveform**: `0`=DC, `1`=AC (sine), `2`=square, `3`=triangle, `4`=sawtooth, `5`=pulse, `6`=noise, `7`=var/rail
- **frequency**: Frequency in Hz (double, ignored for DC but still present positionally)
- **max-voltage**: Peak voltage in volts (double)
- **bias**: DC offset added to the waveform (double)
- **phase-shift**: Radians (double)
- **duty-cycle**: 0–1, used by square/pulse waveforms (double)
- All fields after `flags` are read in a try/catch and default to `frequency=40, max-voltage=5, bias=0, phase-shift=0, duty-cycle=0.5, waveform=DC` if omitted — but they're read positionally, so a short line still shifts values (e.g. a single trailing `5` is read as `waveform=5` i.e. pulse, not a 5V value). Always write the full 6 fields.
- **flags**: `FLAG_COS` (2) — legacy only: on load, sets `phase-shift = π/2` then self-clears, never write it; `FLAG_PULSE_DUTY` (4) — marks the duty-cycle field as meaningfully set for the pulse waveform (if clear and `waveform=5`, duty-cycle is forced to `1/(2π)` regardless of the field's value); `FLAG_CIRCLE_SYMBOL` (8) — draw a circle symbol at DC source terminals; `FLAG_SHOW_VOLTAGE` (16) — show a voltage readout on the element; `FLAG_TIME_SPEC` (32) — reserved for time-zero bookkeeping (used with the var/rail waveform); `FLAG_SHOW_VOLTAGE_RAIL` (64) — separate "show voltage" bit used only by the rail-element subtype
- **DC 5V example**: `v 96 160 96 224 0 0 40 5 0 0 0.5`
- **AC 5V @ 5kHz example**: `v 96 160 96 224 0 1 5000 5 0 0 0.5`

#### Op-Amp
```
a <x> <y> <x2> <y2> <flags> <max-out> <min-out> <gain-bandwidth> <v-in-plus> <v-in-minus> <gain>
```
- **dump-type**: `a` (97) — this is `OpAmpElm`, **not** a voltage source. It draws as a triangle with `+`/`-` input leads and needs both inputs driven; leaving them unconnected shows as floating (red) nodes.
- **max-out** / **min-out**: Output voltage rail limits (double, default 15 / -15)
- **gain-bandwidth**, **v-in-plus**, **v-in-minus**, **gain**: Optional trailing fields (all default if omitted)
- **flags**: `FLAG_SWAP` (1) — swap the +/- input positions; `FLAG_SMALL` (2) — draw a small symbol; `FLAG_LOWGAIN` (4) — legacy gain of 1000 instead of 100000 (only consulted when `FLAG_GAIN` is clear); `FLAG_GAIN` (8) — marks the trailing `gain` field as explicit/valid, skipping the legacy default entirely
- **Example**: `a 96 160 96 224 0 15 -15`

#### Current Source
```
i <x> <y> <x2> <y2> <flags> <current>
```
- **dump-type**: `i` (105) — class `CurrentElm`
- **current**: Current in amps (double)
- **flags**: No `FLAG_*` constants defined in `CurrentElm`; field is unused
- **Example**: `i 96 160 96 224 0 0.001`

### Switches and Logic

All switch-family elements (`SwitchElm` and its subclasses `Switch2Elm`, `LogicInputElm`, `DPDTSwitchElm`) share a base grammar: the string-dump constructor reads `<position> <momentary>` positionally right after `<flags>`, before any subclass-specific fields — and, if `FLAG_LABEL` is set, an escaped label string at the very end. Base `SwitchElm` flags (inherited by all of them):
- `FLAG_IEC` (2) — draw the IEC-style switch symbol
- `FLAG_LABEL` (4) — a trailing escaped label string follows the normal fields

#### Switch (SPST)
```
s <x> <y> <x2> <y2> <flags> <position> <momentary>
```
- **dump-type**: `s` (115, **lowercase**) — class `SwitchElm`
- **position**: `0`=closed, `1`=open (int)
- **momentary**: `true`/`false` — push-button behavior
- **flags**: see base switch-family flags above; no additional flags of its own
- **Example**: `s 192 160 256 160 0 0 false`

#### Switch (SPDT)
```
S <x> <y> <x2> <y2> <flags> <position> <momentary> <link> <throw-count>
```
- **dump-type**: `S` (83, **uppercase**) — class `Switch2Elm`, a *different* element from the SPST switch above (it extends `SwitchElm`, not the reverse); the two dump-types don't collide
- **link**: pole-group id used to keep multiple poles of a multi-pole switch in sync (int)
- **throw-count**: number of throws, typically 2 (int)
- **flags**: base switch-family flags, plus `FLAG_CENTER_OFF` (1) — allow a center "off" position (only honored when `throw-count == 2`)
- **Example**: `S 192 160 256 160 0 0 false 0 2`

#### Logic Input
```
L <x> <y> <x2> <y2> <flags> <position> <momentary> <high-voltage> <low-voltage>
```
- **dump-type**: `L` (76, **uppercase**) — class `LogicInputElm`, extends `SwitchElm`; distinct from the Inductor's lowercase `l` (108)
- **high-voltage**: High state voltage (double, default 5)
- **low-voltage**: Low state voltage (double, default 0)
- **flags**: base switch-family flags, plus `FLAG_TERNARY` (1) — 3-state (0/½/1) instead of 2-state, `FLAG_NUMERIC` (2) — display state as a digit instead of the L/H letter
- **Example**: `L 192 224 240 224 0 0 false 5 0`

#### DPDT Switch (Multi-Pole)
```
429 <x> <y> <x2> <y2> <flags> <position> <momentary> <pole-count>
```
- **dump-type**: `429` — class `DPDTSwitchElm`, extends `SwitchElm`
- **pole-count**: Number of poles (2, 3, etc.)
- **flags**: base switch-family flags above; no additional flags of its own
- **Example**: `429 192 160 256 160 0 0 false 2`

### Diodes and Transistors

#### Diode
```
d <x> <y> <x2> <y2> <flags> [fwdrop | model-name]
```
- **dump-type**: `d` (100)
- **flags**: `FLAG_FWDROP` (1) — a trailing forward-voltage-drop value follows (only read when `FLAG_MODEL` is clear); `FLAG_MODEL` (2) — a trailing escaped model-name string follows instead (current builds always set this when dumping)
- **Example**: `d 192 160 256 160 0`

#### NPN/PNP Transistor
```
t <x> <y> <x2> <y2> <flags> <pnp-flag>
```
- **dump-type**: `t` (116) — dump class is `TransistorElm` itself (confirmed via `getDumpClass()`); `NTransistorElm`/`PTransistorElm` are just UI-construction subclasses (fixed `pnp-flag`), not separate dump types
- **pnp-flag**: 1 for NPN, -1 for PNP (integer)
- **flags**: `FLAG_FLIP` (1) — swap emitter/collector visually; `FLAG_CIRCLE` (2) — **global**: draws a circle around the symbol for every transistor in the circuit, not just this instance (applied via a shared static, though stored per-element)
- **Example**: `t 192 160 256 160 0 1`

### Chips and Digital Logic

#### Counter (up/down, mod N)
```
164 <x> <y> <x2> <y2> <flags> <invert-reset> <modulus>
```
- **dump-type**: `164` (not 202 — that dump-type doesn't exist in current source) — class `CounterElm`
- **invert-reset**: `true`/`false`
- **modulus**: Modulus value (e.g., 256, 0 for unbounded)
- **flags**: `FLAG_UP_DOWN` (4) — count down instead of up; `FLAG_NEGATIVE_EDGE` (8) — clock on falling edge instead of rising
- **Example**: `164 192 160 256 160 0 true 256`

#### Counter (simple, with clear pin)
```
421 <x> <y> <x2> <y2> <flags> <modulus>
```
- **dump-type**: `421` — class `Counter2Elm`, a separate chip from the up/down counter above
- **modulus**: Modulus value
- **flags**: No `FLAG_*` constants defined
- **Example**: `421 192 160 256 160 0 256`

#### Analog Mux
```
432 <x> <y> <x2> <y2> <flags> <selectBits> <r_on> <r_off> <threshold>
```
- **dump-type**: `432`
- **selectBits**: Number of select bits (2-4 typical)
- **r_on**: On resistance in ohms (double, e.g., 20)
- **r_off**: Off resistance in ohms (double, e.g., 1e10)
- **threshold**: Logic threshold voltage (double, e.g., 2.5)
- **flags**: `FLAG_PULLDOWN` (2) — unselected inputs pulled to ground through `r_off` instead of connected to the output through `r_off`
- **Example**: `432 192 160 256 160 0 2 20 1e10 2.5`

#### Custom Composite (Subcircuit)
```
CompositeElm:<model-name> <x> <y> <x2> <y2> <flags>
```
- **Element type**: `CustomCompositeElm:ModelName`
- Uses special class naming convention
- **flags**: `FLAG_ESCAPE` (1, inherited from `CompositeElm`) — model name is stored escaped, always set; `FLAG_SMALL` (2) — render the chip at small grid size
- **Example**: `CustomCompositeElm:MyFilter 192 160 256 160 0`

### Wires and Connections

#### Wire
```
w <x> <y> <x2> <y2> <flags>
```
- **dump-type**: `w` (119)
- **flags**: `busWidth` is **not** stored in flags (a plain dumped `WireElm` is always single-width — bus wires are a separate runtime/routing feature, not a flag bit). Real flags are display toggles: `FLAG_SHOWCURRENT` (1), `FLAG_SHOWVOLTAGE` (2), `FLAG_SHOW_BUS_VALUE` (4), `FLAG_SHOW_BUS_VALUE_HEX` (8)
- **Example**: `w 192 160 256 160 0`

#### Ground
```
g <x> <y> <x2> <y2> <flags> [symbol-type]
```
- **dump-type**: `g` (103)
- **flags**: `FLAG_OLD_STYLE` (1) — legacy compatibility bit kept only so old subcircuit dumps still render with the old symbol; in current builds the symbol style is actually chosen by the trailing `symbol-type` int field, not by this flag
- **Example**: `g 192 224 192 256 0`

#### Labeled Node
```
207 <x> <y> <x2> <y2> <flags> <label>
```
- **dump-type**: `207` (text) — XML tag is `<ln>` (attribute `te="..."`)
- **label**: Node label text
- **flags**: `FLAG_ESCAPE` (4) if the label is stored escaped (`CustomLogicModel.escape()`); `FLAG_INTERNAL` (1); `FLAG_ROTATE_TEXT` (8) rotates text for vertical stubs
- **Example (text)**: `207 192 160 256 160 4 output`
- **Example (XML)**: `<ln x="192 160 256 160" f="0" te="output"/>`

How labels work (this matters):
- The labeled node **connects electrically only at `point1`** — it tags that node with a name and does NOT bridge `point1` to `point2`. `point2` (and the short stub drawn toward it) is purely where the text renders. To label a node, put `point1` exactly on a wire junction / element post; `point2` points into open space where you want the text.
- **Two labeled nodes with the same label are connected together** (like global nets / buses). Never reuse a name unintentionally, and don't use the same name twice on different nets.
- Text placement: for a horizontal stub, text sits just past `point2` (right edge for left→right, left edge for right→left). For a vertical stub, text is centered on `point2.x` and offset one font-height past `point2` in the stub direction — point `point2` a bit further out so text clears the trace.
- In text format, escape spaces/special chars with `CustomLogicModel.escape()` and set `FLAG_ESCAPE`. In XML, `te` is raw text (XML-escape `&`, `<`, `"` only).

### Visualization

#### Scope
```
403 <x> <y> <x2> <y2> <flags> <scope-data-token>     # text format
```
- **dump-type**: `403` (text format); the **XML tag is `o`** — not `107`; `107` doesn't exist anywhere in current source. Class `ScopeElm`
- **scope-data-token** (text format): a single underscore-delimited string parsed by the embedded `Scope` object's own `undump()` — display options (which signal(s) to show, log scale, stacked traces, etc.) live inside that token, not in the `<flags>` field. There is no `<probe-count> [names...]` grammar on the element line itself
- **flags**: No `FLAG_*` constants defined on `ScopeElm` itself
- **Example (text)**: `403 96 96 160 160 0 <scope-internal-token>`

**Scope in XML.** A scope serializes as a top-level `<o>` element. It is handled
specially by `XMLDeserializer.readElements` (the `o` tag is checked before the
tag→class map, and `ScopeElm`'s own `getXmlDumpType()` would be `Scope`), so do
**not** give it coordinates: its `x` attribute is the optional scope caption
text, not a position. Each traced signal is a child `<p>`:

```xml
<o en="5" sp="64" f="2" p="0" x="caption">
  <p v="0" sc="5"/>          <!-- element `en`, value 0 (voltage) -->
  <p e="0" v="0" sc="5"/>    <!-- element 0, value 0 -->
</o>
```

| Attribute | Meaning |
|---|---|
| `en` | **Index of the plotted element** in the circuit's element list — file order, 0-based, **scopes excluded** (a scope is not in `elmList`). The scope shows that element's voltage/current, so it needs no probe wires |
| `sp` | scope plot speed in sim-timestep units per pixel (default 64). Lower = finer time base; pick one that shows ~2–4 cycles of the signal or the trace is unreadable |
| `f` | display flags — bit 0 `showI`, bit 1 `showV`, bit 2 `showMax` (inverted), bit 3 `showFreq`, … Set `f="2"` or voltage traces won't render (`Scope.calcVisiblePlots` hides `VAL_VOLTAGE` plots unless `showV`) |
| `p` | scope stack position in the scope panel (default 0) |
| `x` | optional caption text (XML-escaped); **not** coordinates |
| `<p v>` | value shown: `0` voltage, `3` current, `7` power (see `Scope.VAL_*`) |
| `<p e>` | element index for this trace; defaults to the parent `en` |
| `<p sc>` | vertical scale for the trace's units |

Because `en`/`e` are positional indices, inserting or removing elements above the
plotted one shifts which element the scope points at — recompute them after
changing the netlist. (This `<o>` form is the floating scope the "add scope"
menu produces; the on-canvas `ScopeElm` element instead dumps as `<Scope x=…>`
wrapping this same `<o>` child.)

#### Data Recorder
```
210 <x> <y> <x2> <y2> <flags> <data-count>
```
- **dump-type**: `210`
- **data-count**: Number of data samples (int, default 10240)
- **flags**: No `FLAG_*` constants defined
- **Example**: `210 96 96 160 160 0 10240`

#### Output (test point)
```
O <x> <y> <x2> <y2> <flags> <scale>
```
- **dump-type / XML tag**: `O` / `<O>` — a **1-post** measurement point (`getPostCount() == 1`); only the first coordinate pair connects, the second just positions the readout text
- **flags**: `FLAG_VALUE` (`1`) = display the measured voltage at the point; `FLAG_FIXED` (`2`) = freeze decimal precision. No flag → the point draws the literal label `out`
- **scale**: display scale — `SCALE_AUTO` (`0`) by default, else `SCALE_K` (`1`), `SCALE_M` (`2`), `SCALE_MU` (`3`) …; in XML this is the `sc` attribute
- **XML example**: `<O x="96 224 96 256" f="1" sc="0"/>`
- **Text example**: `O 96 224 96 256 1 0`

---

## Dump Type → Element Class Map

```python
DUMP_TYPE_MAP = {
    'r': 'ResistorElm',
    'c': 'CapacitorElm',
    'l': 'InductorElm',       # lowercase L — uppercase 'L' below is a different element
    'v': 'VoltageElm',       # DC/AC/square/etc. — see waveform field
    'a': 'OpAmpElm',         # NOT a voltage source — triangle op-amp symbol
    'i': 'CurrentElm',
    'd': 'DiodeElm',
    't': 'TransistorElm',     # NPN/PNP both dump as this class (getDumpClass() confirms)
    's': 'SwitchElm',          # SPST — lowercase 's'
    'S': 'Switch2Elm',         # SPDT — uppercase 'S', a different element from SwitchElm
    'L': 'LogicInputElm',      # uppercase L — extends SwitchElm; not the Inductor
    'n': 'NoiseElm',           # legacy noise source ('n' is NOT the label type)
    207: 'LabeledNodeElm',     # text dump type; XML tag is <ln>
    'O': 'OutputElm',
    'w': 'WireElm',
    'g': 'GroundElm',
    403: 'ScopeElm',           # not 107 — that dump-type doesn't exist in current source
    164: 'CounterElm',         # up/down mod-N counter — not 202
    421: 'Counter2Elm',        # simple incrementing counter, separate chip from CounterElm
    210: 'DataRecorderElm',
    429: 'DPDTSwitchElm',
    432: 'AnalogMuxElm',
}
```
