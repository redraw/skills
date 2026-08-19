# Working with Files

Prefer the XML format for generating/writing circuits (see [xml-format.md](xml-format.md)) — it's a standard tree structure, so a real XML library (e.g. `xml.etree.ElementTree`) handles quoting/escaping for you instead of hand-rolling delimiter and escape logic. The text-format helpers below remain useful for reading/importing legacy `.txt` circuit files.

### Loading/Saving a Circuit as XML

**Python Example:**
```python
import xml.etree.ElementTree as ET

def load_circuit_xml(filename):
    tree = ET.parse(filename)
    root = tree.getroot()  # <cir ...>
    options = dict(root.attrib)
    elements = [{'tag': child.tag, **child.attrib} for child in root]
    return options, elements

def save_circuit_xml(filename, options, elements):
    root = ET.Element('cir', options)
    for elem in elements:
        tag = elem['tag']
        attribs = {k: v for k, v in elem.items() if k != 'tag'}
        ET.SubElement(root, tag, attribs)
    ET.ElementTree(root).write(filename, encoding='UTF-8', xml_declaration=True)
```

No manual escaping is needed for labels/text (`te` attribute) — `ElementTree` escapes attribute values automatically, unlike the text format's `%20`/backslash scheme below.

### Loading a Circuit from Text

**Python Example:**
```python
def load_circuit_file(filename):
    with open(filename, 'r') as f:
        lines = f.readlines()
    
    options_line = lines[0].strip()
    parse_options(options_line)
    
    elements = []
    for line in lines[1:]:
        if line.strip() and not line.startswith('#'):
            elements.append(parse_element(line))
    
    return elements

def parse_element(line):
    tokens = line.strip().split()
    dump_type = tokens[0]
    x, y, x2, y2 = int(tokens[1]), int(tokens[2]), int(tokens[3]), int(tokens[4])
    flags = int(tokens[5])
    data = tokens[6:] if len(tokens) > 6 else []
    
    return {
        'type': dump_type,
        'x': x, 'y': y, 'x2': x2, 'y2': y2,
        'flags': flags,
        'data': data
    }
```

### Saving a Circuit as Text

**Python Example:**
```python
def save_circuit_file(filename, options, elements):
    with open(filename, 'w') as f:
        # Write options line
        f.write(format_options(options) + '\n')
        
        # Write elements
        for elem in elements:
            f.write(format_element(elem) + '\n')

def format_element(elem):
    parts = [elem['type'], str(elem['x']), str(elem['y']), 
             str(elem['x2']), str(elem['y2']), str(elem['flags'])]
    parts.extend(elem['data'])
    return ' '.join(parts)
```

### Parsing Special Characters

Labeled nodes and text elements use escape sequences:

```python
def escape_text(text):
    """Escape special characters for circuit format"""
    text = text.replace('\\', '\\\\')
    text = text.replace(' ', '%20')
    return text

def unescape_text(text):
    """Unescape special characters from circuit format"""
    text = text.replace('%20', ' ')
    text = text.replace('\\\\', '\\')
    return text
```

### URL-Encoded Format

Circuits can be compressed in URLs using LZString:

```javascript
// Compress circuit for URL
var compressedCircuit = LZString.compressToEncodedURIComponent(circuitText);
var url = `https://pfalstad.github.io/circuitjs1/circuitjs.html?ctz=${compressedCircuit}`;

// Decompress circuit from URL
var circuitText = LZString.decompressFromEncodedURIComponent(compressedCircuit);
```
