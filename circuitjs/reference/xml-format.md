# XML Format Specification

### Structure

The root element is `<cir>` (not `<circuit>`), and each element's tag name is its own dump-type identifier — the same single character used in the text format (`getXmlDumpType()` returns that character for any element whose text dump-type is a printable ASCII char in range 65–126; it falls back to the class name with `Elm` stripped only for elements that don't have one). There is **no** generic `<element type="...">` wrapper — the type IS the tag name:

```xml
<cir f="31" ts="5e-6" ic="0.5" cb="50" vr="5" pb="50" mts="1e-9">
  <v x="96 160 96 224" f="0" wf="1" fr="5000" maxv="5"/>
  <r x="192 160 256 160" f="0" r="1000"/>
  <c x="256 160 256 224" f="0" c="1e-7"/>
  <g x="96 224 96 256" f="0"/>
  <w x="96 160 192 160" f="0"/>
</cir>
```

### Element Conversion

**Text to XML Mapping:**
```
Dump Type       → tag name (the element itself, not a "type" attribute)
x y x2 y2       → x attribute (space-separated)
flags           → f attribute
Element data    → individual attributes (shorthand names, e.g. r="1000", c="1e-7", wf="1")
```

### Common Attributes

| Attribute | Type | Example | Meaning |
|-----------|------|---------|---------|
| `x` | string | "192 160 256 160" | Coordinates (x y x2 y2) |
| `f` | int | 0 | Flags |
| `r` | double | 1000 | Resistance (ohms) |
| `c` | double | 0.001 | Capacitance (farads) |
| `l` | double | 0.1 | Inductance (henries) |
| `wf` | int | 1 | Voltage source waveform (0=DC, 1=AC, 2=square, ...) |
| `v` | double | 5.0 | Voltage (volts) |
| `fr` | double | 60 | Frequency (Hz) |
| `hi` | double | 5.0 | High voltage |
| `lo` | double | 0 | Low voltage |
| `te` | string | "label" | Text/label |
| `mo` | int | 256 | Modulus |

### XML Tag → Element Class

```
r    → ResistorElm
c    → CapacitorElm
L    → InductorElm
v    → VoltageElm       (DC/AC/square/etc. — see waveform (wf) attribute; NOT a separate DC/AC class)
a    → OpAmpElm         (op-amp, NOT a voltage source)
i    → CurrentSourceElm
d    → DiodeElm
t    → NTransistorElm / PNPTransistorElm
S    → SwitchElm
w    → WireElm
g    → GroundElm
ln   → LabeledNodeElm    (label text in `te` attribute — see example below)
Scope, Counter2, CustomCompositeElm, etc. → tag is the class name minus "Elm" (no single-char text dump type)
```

### Example XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<cir f="31" ts="5e-6" ic="0.5" cb="50" vr="5" pb="50" mts="1e-9">
  <v x="96 160 96 224" f="0" wf="0" maxv="5"/>
  <r x="192 160 256 160" f="0" r="1000"/>
  <c x="256 160 256 224" f="0" c="1e-7"/>
  <g x="96 224 96 256" f="0"/>
  <w x="96 224 256 224" f="0"/>
</cir>
```

### Labels (labeled nodes)

A labeled node is the tag **`ln`** — the text format dump type is `207`, and it is **not** `n` (`n` is the legacy noise source). The label text goes in the `te` attribute:

```xml
<cir f="31" ts="5e-6" ic="0.5" cb="50" vr="5" pb="50" mts="1e-9">
  <v x="32 160 32 224" f="0" wf="1" fr="1000" maxv="5"/>
  <g x="32 224 32 256" f="0"/>
  <w x="32 160 96 160" f="0"/>
  <ln x="96 160 96 112" f="0" te="in"/>     <!-- tags the node at (96,160); text "in" drawn above -->
  <r x="96 160 192 160" f="0" r="1000"/>
  <c x="192 160 192 224" f="0" c="1.5915e-7"/>
  <g x="192 224 192 256" f="0"/>
  <ln x="192 160 192 112" f="0" te="out"/>  <!-- tags the node at (192,160); text "out" drawn above -->
</cir>
```

Placement rules:
- The **first coordinate pair (point1)** is the electrical connection — it must coincide with a wire junction or element post. The **second pair (point2)** only controls where the text draws; the element does not electrically connect point1 to point2.
- Point point2 into open space (here, straight up from the trace). Text renders just past point2 (offset one font-height for vertical stubs).
- Labels with the **same `te` value connect their nets together** — reuse names deliberately (buses, gnd, etc.), never by accident.
- `te` is raw text in XML; escape `&`, `<`, `"` as `&amp;`, `&lt;`, `&quot;`.
