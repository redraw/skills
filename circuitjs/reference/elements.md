# Element Reference

### Two-Terminal Linear Elements

#### Resistor
```
r <x> <y> <x2> <y2> <flags> <resistance>
```
- **dump-type**: `r` (114)
- **resistance**: Value in ohms (double)
- **flags**: Typically 0
- **Example**: `r 192 160 256 160 0 1000`

#### Capacitor
```
c <x> <y> <x2> <y2> <flags> <capacitance>
```
- **dump-type**: `c` (99)
- **capacitance**: Value in farads (double)
- **Example**: `c 192 224 256 224 0 0.001`

#### Inductor
```
L <x> <y> <x2> <y2> <flags> <inductance>
```
- **dump-type**: `L` (76)
- **inductance**: Value in henries (double)
- **Example**: `L 192 288 256 288 0 0.1`

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
- **DC 5V example**: `v 96 160 96 224 0 0 40 5 0 0 0.5`
- **AC 5V @ 5kHz example**: `v 96 160 96 224 0 1 5000 5 0 0 0.5`

#### Op-Amp
```
a <x> <y> <x2> <y2> <flags> <max-out> <min-out> <gain-bandwidth> <v-in-plus> <v-in-minus> <gain>
```
- **dump-type**: `a` (97) — this is `OpAmpElm`, **not** a voltage source. It draws as a triangle with `+`/`-` input leads and needs both inputs driven; leaving them unconnected shows as floating (red) nodes.
- **max-out** / **min-out**: Output voltage rail limits (double, default 15 / -15)
- **gain-bandwidth**, **v-in-plus**, **v-in-minus**, **gain**: Optional trailing fields (all default if omitted)
- **Example**: `a 96 160 96 224 0 15 -15`

#### Current Source
```
i <x> <y> <x2> <y2> <flags> <current>
```
- **dump-type**: `i` (105)
- **current**: Current in amps (double)
- **Example**: `i 96 160 96 224 0 0.001`

### Switches and Logic

#### Switch (SPST)
```
S <x> <y> <x2> <y2> <flags>
```
- **dump-type**: `S` (83)
- **flags**: Initial position in lower bits
- **Example**: `S 192 160 256 160 1`

#### Logic Input
```
L <x> <y> <x2> <y2> <flags> <high-voltage> <low-voltage>
```
- **dump-type**: `L` (76)
- **high-voltage**: High state voltage (double, default 5)
- **low-voltage**: Low state voltage (double, default 0)
- **flags**: Can include FLAG_TERNARY (1) or FLAG_NUMERIC (2)
- **Example**: `L 192 224 240 224 0 5 0`

#### DPDT Switch (Multi-Pole)
```
429 <x> <y> <x2> <y2> <flags> <pole-count>
```
- **dump-type**: `429`
- **pole-count**: Number of poles (2, 3, etc.)
- **Example**: `429 192 160 256 160 0 2`

### Diodes and Transistors

#### Diode
```
d <x> <y> <x2> <y2> <flags>
```
- **dump-type**: `d` (100)
- **Example**: `d 192 160 256 160 0`

#### NPN Transistor
```
t <x> <y> <x2> <y2> <flags> <pnp-flag>
```
- **dump-type**: `t` (116)
- **pnp-flag**: 1 for NPN, -1 for PNP (integer)
- **Example**: `t 192 160 256 160 0 1`

### Chips and Digital Logic

#### Counter (mod N)
```
202 <x> <y> <x2> <y2> <flags> <modulus>
```
- **dump-type**: `202`
- **modulus**: Module value (e.g., 256, 0 for unbounded)
- **Example**: `202 192 160 256 160 0 256`

#### Analog Mux
```
432 <x> <y> <x2> <y2> <flags> <selectBits> <r_on> <r_off> <threshold>
```
- **dump-type**: `432`
- **selectBits**: Number of select bits (2-4 typical)
- **r_on**: On resistance in ohms (double, e.g., 20)
- **r_off**: Off resistance in ohms (double, e.g., 1e10)
- **threshold**: Logic threshold voltage (double, e.g., 2.5)
- **Example**: `432 192 160 256 160 0 2 20 1e10 2.5`

#### Custom Composite (Subcircuit)
```
CompositeElm:<model-name> <x> <y> <x2> <y2> <flags>
```
- **Element type**: `CustomCompositeElm:ModelName`
- Uses special class naming convention
- **Example**: `CustomCompositeElm:MyFilter 192 160 256 160 0`

### Wires and Connections

#### Wire
```
w <x> <y> <x2> <y2> <flags>
```
- **dump-type**: `w` (119)
- **flags**: Bus width in lower bits (1 for single wire, >1 for buses)
- **Example**: `w 192 160 256 160 0`

#### Ground
```
g <x> <y> <x2> <y2> <flags>
```
- **dump-type**: `g` (103)
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
107 <x> <y> <x2> <y2> <flags> <probe-count> [probe1_name] [probe2_name] ...
```
- **dump-type**: `107`
- **probe-count**: Number of probes attached (integer)
- **probe-names**: Names of signal connections
- **Example**: `107 96 96 160 160 0 2 voltage current`

#### Data Recorder
```
210 <x> <y> <x2> <y2> <flags> <data-count>
```
- **dump-type**: `210`
- **data-count**: Number of data samples (int, default 10240)
- **Example**: `210 96 96 160 160 0 10240`

---

## Dump Type → Element Class Map

```python
DUMP_TYPE_MAP = {
    'r': 'ResistorElm',
    'c': 'CapacitorElm',
    'L': 'InductorElm',
    'v': 'VoltageElm',       # DC/AC/square/etc. — see waveform field
    'a': 'OpAmpElm',         # NOT a voltage source — triangle op-amp symbol
    'i': 'CurrentSourceElm',
    'd': 'DiodeElm',
    't': 'NTransistorElm',
    'S': 'SwitchElm',
    'n': 'NoiseElm',           # legacy noise source ('n' is NOT the label type)
    207: 'LabeledNodeElm',     # text dump type; XML tag is <ln>
    'O': 'OutputElm',
    'w': 'WireElm',
    'g': 'GroundElm',
    107: 'ScopeElm',
    202: 'Counter2Elm',
    210: 'DataRecorderElm',
    429: 'DPDTSwitchElm',
    432: 'AnalogMuxElm',
}
```
