# Text Format Specification

### Overall Structure

```
$ <flags> <maxTimeStep> <iterCount> <currentBar> <voltageRange> <powerBar> <minTimeStep>
<element-line-1>
<element-line-2>
...
<element-line-n>
```

### Options Line (Line 1)

```
$ <flags> <maxTimeStep> <iterCount> <currentBar> <voltageRange> <powerBar> <minTimeStep>
```

**Parameters:**

| Parameter | Type | Range | Description |
|-----------|------|-------|-------------|
| `flags` | int | 0-255 | Option flags (see below) |
| `maxTimeStep` | double | e.g., 5e-06 | Maximum simulation time step |
| `iterCount` | double | e.g., 0.5 | Iteration count (affects speed) |
| `currentBar` | int | 0-100 | Current bar position |
| `voltageRange` | double | e.g., 5.0 | Voltage display range |
| `powerBar` | int | 0-100 | Power bar position |
| `minTimeStep` | double | e.g., 1e-09 | Minimum time step |

**Flags Breakdown:**
```
Bit 0 (1):   Dots checkbox (current animation enabled)
Bit 1 (2):   Small grid checkbox
Bit 2 (4):   Volts checkbox (INVERTED - 0=on, 1=off)
Bit 3 (8):   Power checkbox
Bit 4 (16):  Show values checkbox (INVERTED - 0=on, 1=off)
Bit 5 (32):  (reserved)
Bit 6 (64):  Adjust time step
Bit 7 (128): Auto DC on reset
```

**Example:**
```
$ 31 5e-06 0.5 50 5 50 1e-09
```
Flags = 31 = 00011111b = dots + small grid + volts OFF + power + show values OFF

### Element Lines

**Format:**
```
<dump-type> <x> <y> <x2> <y2> <flags> [element-specific-data...]
```

**Common Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `dump-type` | char/int | Element type identifier (see [elements.md](elements.md)) |
| `x` | int | Starting X coordinate (pixels) |
| `y` | int | Starting Y coordinate (pixels) |
| `x2` | int | Ending X coordinate (pixels) |
| `y2` | int | Ending Y coordinate (pixels) |
| `flags` | int | Element-specific flags (orientation, state, etc.) |

**Coordinate System:**
- Origin (0,0) is top-left
- Grid size typically 8 pixels
- Positive X = right, Positive Y = down

**Flag Encoding for dump-type:**
- Character codes (e.g., 'r', 'L', 'I'): stored as single char + space
- Numeric (200+): stored as number + space
