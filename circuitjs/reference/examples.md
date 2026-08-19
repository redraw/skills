# CircuitJS1 Example Circuits Index

Categorized list of the example circuits shipped with the upstream [CircuitJS1](https://github.com/pfalstad/circuitjs1) repo (`src/com/lushprojects/circuitjs1/public/circuits/`), generated from its `setuplist.txt` menu. All files are in the legacy text format (see [text-format.md](text-format.md)) — still valid as CircuitJS1 import.

Files are copied verbatim from the upstream repo (GPLv2) for inspiration and reuse — grep by topic below or open a `.txt` directly instead of hand-writing a circuit from scratch. When adapting one for output, prefer converting it to XML (see [xml-format.md](xml-format.md)) per this skill's format preference, rather than emitting it as-is in text format.

## Basics

- [`ohms.txt`](../examples/ohms.txt) — Ohm's Law
- [`resistors.txt`](../examples/resistors.txt) — Resistors
- [`cap.txt`](../examples/cap.txt) — Capacitor
- [`induct.txt`](../examples/induct.txt) — Inductor
- [`lrc.txt`](../examples/lrc.txt) — LRC Circuit
- [`voltdivide.txt`](../examples/voltdivide.txt) — Voltage Divider
- [`pot.txt`](../examples/pot.txt) — Potentiometer
- [`potdivide.txt`](../examples/potdivide.txt) — Potentiometer Divider
- [`thevenin.txt`](../examples/thevenin.txt) — Thevenin's Theorem
- [`norton.txt`](../examples/norton.txt) — Norton's Theorem

## A/C Circuits

- [`capac.txt`](../examples/capac.txt) — Capacitor
- [`inductac.txt`](../examples/inductac.txt) — Inductor
- [`capmultcaps.txt`](../examples/capmultcaps.txt) — Caps of Various Capacitances
- [`capmultfreq.txt`](../examples/capmultfreq.txt) — Caps w/ Various Frequencies
- [`indmultind.txt`](../examples/indmultind.txt) — Inductors of Various Inductances
- [`indmultfreq.txt`](../examples/indmultfreq.txt) — Inductors w/ Various Frequencies
- [`impedance.txt`](../examples/impedance.txt) — Impedances of Same Magnitude
- [`res-series.txt`](../examples/res-series.txt) — Series Resonance
- [`res-par.txt`](../examples/res-par.txt) — Parallel Resonance

## Passive Filters

- [`filt-hipass.txt`](../examples/filt-hipass.txt) — High-Pass Filter (RC)
- [`filt-lopass.txt`](../examples/filt-lopass.txt) — Low-Pass Filter (RC)
- [`filt-hipass-l.txt`](../examples/filt-hipass-l.txt) — High-Pass Filter (RL)
- [`filt-lopass-l.txt`](../examples/filt-lopass-l.txt) — Low-Pass Filter (RL)
- [`bandpass.txt`](../examples/bandpass.txt) — Band-pass Filter
- [`bandnoise.txt`](../examples/bandnoise.txt) — Band-pass w/ Noise
- [`notch.txt`](../examples/notch.txt) — Notch Filter
- [`twint.txt`](../examples/twint.txt) — Twin-T Filter
- [`crossover.txt`](../examples/crossover.txt) — Crossover
- [`butter10lo.txt`](../examples/butter10lo.txt) — Butterworth Low-Pass (10 pole)
- [`butter10hi.txt`](../examples/butter10hi.txt) — Butterworth High-Pass (10 pole)
- [`butter10loaud.txt`](../examples/butter10loaud.txt) — Butterworth Low-Pass w/ Noise
- [`butter10hiaud.txt`](../examples/butter10hiaud.txt) — Butterworth High-Pass w/ Noise
- [`butterbandstop.txt`](../examples/butterbandstop.txt) — Butterworth Band-Stop
- [`besselbutter.txt`](../examples/besselbutter.txt) — Bessel vs Butterworth
- [`ringing.txt`](../examples/ringing.txt) — Band-pass with Ringing
- [`comb.txt`](../examples/comb.txt) — Comb Filter

## Other Passive Circuits


### Series/Parallel

- [`indseries.txt`](../examples/indseries.txt) — Inductors in Series
- [`indpar.txt`](../examples/indpar.txt) — Inductors in Parallel
- [`capseries.txt`](../examples/capseries.txt) — Caps in Series
- [`cappar.txt`](../examples/cappar.txt) — Caps in Parallel

### Transformers

- [`transformer.txt`](../examples/transformer.txt) — Transformer
- [`transformerdc.txt`](../examples/transformerdc.txt) — Transformer w/ DC
- [`transformerup.txt`](../examples/transformerup.txt) — Step-Up Transformer
- [`transformerdown.txt`](../examples/transformerdown.txt) — Step-Down Transformer
- [`longdist.txt`](../examples/longdist.txt) — Long-Distance Power Transmission

#### Saturable Core

- [`satcore-inductor.txt`](../examples/satcore-inductor.txt) — Saturable vs Linear Inductor (DC)
- [`satcore-comparison.txt`](../examples/satcore-comparison.txt) — Low vs High Drive (AC Saturation)
- [`satcore-transformer.txt`](../examples/satcore-transformer.txt) — Transformer with Saturable Core

### Relays

- [`relay.txt`](../examples/relay.txt) — Relay
- [`relayand.txt`](../examples/relayand.txt) — Relay AND
- [`relayor.txt`](../examples/relayor.txt) — Relay OR
- [`relayxor.txt`](../examples/relayxor.txt) — Relay XOR
- [`relaymux.txt`](../examples/relaymux.txt) — Relay Mux
- [`relayff.txt`](../examples/relayff.txt) — Relay Flip-Flop
- [`relaytff.txt`](../examples/relaytff.txt) — Relay Toggle Flip-Flop
- [`relayosc.txt`](../examples/relayosc.txt) — Relay Oscillator
- [`relayctr.txt`](../examples/relayctr.txt) — Relay Counter
- [`3way.txt`](../examples/3way.txt) — 3-Way Light Switches
- [`4way.txt`](../examples/4way.txt) — 3- and 4-Way Light Switches
- [`diff.txt`](../examples/diff.txt) — Differentiator
- [`wheatstone.txt`](../examples/wheatstone.txt) — Wheatstone Bridge
- [`lrc-critical.txt`](../examples/lrc-critical.txt) — Critically Damped LRC
- [`currentsrcelm.txt`](../examples/currentsrcelm.txt) — Current Source
- [`inductkick.txt`](../examples/inductkick.txt) — Inductive Kickback
- [`inductkick-snub.txt`](../examples/inductkick-snub.txt) — Blocking Inductive Kickback
- [`powerfactor1.txt`](../examples/powerfactor1.txt) — Power Factor
- [`powerfactor2.txt`](../examples/powerfactor2.txt) — Power Factor Correction
- [`grid.txt`](../examples/grid.txt) — Resistor Grid
- [`grid2.txt`](../examples/grid2.txt) — Resistor Grid 2
- [`cube.txt`](../examples/cube.txt) — Resistor Cube

### Coupled LC's

- [`coupled1.txt`](../examples/coupled1.txt) — LC Modes (2)
- [`coupled2.txt`](../examples/coupled2.txt) — Weak Coupling
- [`coupled3.txt`](../examples/coupled3.txt) — LC Modes (3)
- [`ladder.txt`](../examples/ladder.txt) — LC Ladder
- [`phaseseq.txt`](../examples/phaseseq.txt) — Phase-Sequence Network
- [`3phasewye.txt`](../examples/3phasewye.txt) — 3-Phase Wye-Wye Balanced Load

## Diodes

- [`diodevar.txt`](../examples/diodevar.txt) — Diode
- [`diodecurve.txt`](../examples/diodecurve.txt) — Diode I/V Curve
- [`rectify.txt`](../examples/rectify.txt) — Half-Wave Rectifier
- [`fullrect.txt`](../examples/fullrect.txt) — Full-Wave Rectifier
- [`fullrectf.txt`](../examples/fullrectf.txt) — Full-Wave Rectifier w/ Filter
- [`diodelimit.txt`](../examples/diodelimit.txt) — Diode Limiter

### Zener Diodes

- [`zeneriv.txt`](../examples/zeneriv.txt) — I/V Curve
- [`zenerref.txt`](../examples/zenerref.txt) — Voltage Reference
- [`zenerreffollow.txt`](../examples/zenerreffollow.txt) — Voltage Reference w/ Follower
- [`dcrestoration.txt`](../examples/dcrestoration.txt) — DC Restoration
- [`inductkick-block.txt`](../examples/inductkick-block.txt) — Blocking Inductive Kickback
- [`spikegen.txt`](../examples/spikegen.txt) — Spike Generator

### Voltage Multipliers

- [`voltdouble.txt`](../examples/voltdouble.txt) — Voltage Doubler
- [`voltdouble2.txt`](../examples/voltdouble2.txt) — Voltage Doubler 2
- [`volttriple.txt`](../examples/volttriple.txt) — Voltage Tripler
- [`voltquad.txt`](../examples/voltquad.txt) — Voltage Quadrupler
- [`amdetect.txt`](../examples/amdetect.txt) — AM Detector
- [`diodeclip.txt`](../examples/diodeclip.txt) — Waveform Clipper
- [`sinediode.txt`](../examples/sinediode.txt) — Triangle-to-Sine Converter
- [`ringmod.txt`](../examples/ringmod.txt) — Ring Modulator

## Op-Amps

- [`opamp.txt`](../examples/opamp.txt) — Op-Amp
- [`opampfeedback.txt`](../examples/opampfeedback.txt) — Op-Amp Feedback

### Amplifiers

- [`amp-invert.txt`](../examples/amp-invert.txt) — Inverting Amplifier
- [`amp-noninvert.txt`](../examples/amp-noninvert.txt) — Noninverting Amplifier
- [`amp-follower.txt`](../examples/amp-follower.txt) — Follower
- [`amp-diff.txt`](../examples/amp-diff.txt) — Differential Amplifier
- [`amp-sum.txt`](../examples/amp-sum.txt) — Summing Amplifier
- [`logconvert.txt`](../examples/logconvert.txt) — Log Amplifier
- [`classd.txt`](../examples/classd.txt) — Class-D Amplifier

### Oscillators

- [`relaxosc.txt`](../examples/relaxosc.txt) — Relaxation Oscillator
- [`phaseshiftosc.txt`](../examples/phaseshiftosc.txt) — Phase-Shift Oscillator
- [`triangle.txt`](../examples/triangle.txt) — Triangle Wave Generator
- [`sine.txt`](../examples/sine.txt) — Sine Wave Generator
- [`sawtooth.txt`](../examples/sawtooth.txt) — Sawtooth Wave Generator
- [`vco.txt`](../examples/vco.txt) — Voltage-Controlled Oscillator
- [`trianglevco.txt`](../examples/trianglevco.txt) — Triangle VCO
- [`amp-rect.txt`](../examples/amp-rect.txt) — Half-Wave Rectifier (inverting)
- [`amp-fullrect.txt`](../examples/amp-fullrect.txt) — Full-Wave Rectifier
- [`peak-detect.txt`](../examples/peak-detect.txt) — Peak Detector
- [`amp-integ.txt`](../examples/amp-integ.txt) — Integrator
- [`amp-dfdx.txt`](../examples/amp-dfdx.txt) — Differentiator (inverting)
- [`amp-schmitt.txt`](../examples/amp-schmitt.txt) — Schmitt Trigger
- [`nic-r.txt`](../examples/nic-r.txt) — Negative Impedance Converter
- [`gyrator.txt`](../examples/gyrator.txt) — Gyrator
- [`capmult.txt`](../examples/capmult.txt) — Capacitance Multiplier
- [`howland.txt`](../examples/howland.txt) — Howland Current Source
- [`itov.txt`](../examples/itov.txt) — I-to-V Converter
- [`delta-pwm.txt`](../examples/delta-pwm.txt) — Delta PWM Encoder
- [`opamp-regulator.txt`](../examples/opamp-regulator.txt) — Voltage Regulator
- [`opint.txt`](../examples/opint.txt) — 741 Internals
- [`opint-invert-amp.txt`](../examples/opint-invert-amp.txt) — 741 (inverting amplifier)
- [`opint-slew.txt`](../examples/opint-slew.txt) — 741 Slew Rate
- [`opint-current.txt`](../examples/opint-current.txt) — 741 Current Limits

### Chaotic Circuits

- [`rossler.txt`](../examples/rossler.txt) — Rossler
- [`vilnius.txt`](../examples/vilnius.txt) — Vilnius
- [`chua.txt`](../examples/chua.txt) — Chua
- [`chaos1.txt`](../examples/chaos1.txt) — Chaos 1
- [`chaos2.txt`](../examples/chaos2.txt) — Chaos 2
- [`jerk.txt`](../examples/jerk.txt) — Jerk

## Transistors

- [`npn.txt`](../examples/npn.txt) — NPN Transistor
- [`pnp.txt`](../examples/pnp.txt) — PNP Transistor
- [`transswitch.txt`](../examples/transswitch.txt) — Switch
- [`follower.txt`](../examples/follower.txt) — Emitter Follower

### Multivibrators

- [`multivib-a.txt`](../examples/multivib-a.txt) — Astable Multivib
- [`multivib-bi.txt`](../examples/multivib-bi.txt) — Bistable Multivib (Flip-Flop)
- [`multivib-mono.txt`](../examples/multivib-mono.txt) — Monostable Multivib (One-Shot)
- [`ceamp.txt`](../examples/ceamp.txt) — Common-Emitter Amplifier
- [`phasesplit.txt`](../examples/phasesplit.txt) — Unity-Gain Phase Splitter
- [`schmitt.txt`](../examples/schmitt.txt) — Schmitt Trigger
- [`currentsrc.txt`](../examples/currentsrc.txt) — Current Source
- [`currentsrcramp.txt`](../examples/currentsrcramp.txt) — Current Source Ramp
- [`mirror.txt`](../examples/mirror.txt) — Current Mirror
- [`darlington.txt`](../examples/darlington.txt) — Darlington Pair

### Differential Amplifiers

- [`trans-diffamp.txt`](../examples/trans-diffamp.txt) — Differential Input
- [`trans-diffamp-common.txt`](../examples/trans-diffamp-common.txt) — Common-Mode Input
- [`trans-diffamp-cursrc.txt`](../examples/trans-diffamp-cursrc.txt) — Common-Mode w/Current Source

### Push-Pull Follower

- [`pushpullxover.txt`](../examples/pushpullxover.txt) — Simple, with distortion
- [`pushpull.txt`](../examples/pushpull.txt) — Improved

### Oscillators

- [`colpitts.txt`](../examples/colpitts.txt) — Colpitts Oscillator
- [`hartley.txt`](../examples/hartley.txt) — Hartley Oscillator
- [`eclosc.txt`](../examples/eclosc.txt) — Emitter-Coupled LC Oscillator
- [`crystalosc2.txt`](../examples/crystalosc2.txt) — Crystal Oscillator
- [`gilbertcell.txt`](../examples/gilbertcell.txt) — Gilbert Cell Multiplier
- [`rmsconverter.txt`](../examples/rmsconverter.txt) — True RMS Converter
- [`joule-thief.txt`](../examples/joule-thief.txt) — Joule Thief
- [`transrectifier.txt`](../examples/transrectifier.txt) — Full-Wave Rectifier
- [`early.txt`](../examples/early.txt) — Early Effect

## MOSFETs

- [`nmosfet.txt`](../examples/nmosfet.txt) — n-MOSFET
- [`pmosfet.txt`](../examples/pmosfet.txt) — p-MOSFET
- [`mosswitch.txt`](../examples/mosswitch.txt) — Switch
- [`mosfollower.txt`](../examples/mosfollower.txt) — Source Follower
- [`moscurrentsrc.txt`](../examples/moscurrentsrc.txt) — Current Source
- [`moscurrentramp.txt`](../examples/moscurrentramp.txt) — Current Ramp
- [`mosmirror.txt`](../examples/mosmirror.txt) — Current Mirror
- [`mosfetamp.txt`](../examples/mosfetamp.txt) — Common-Source Amplifier
- [`cmosinverter.txt`](../examples/cmosinverter.txt) — CMOS Inverter
- [`cmosinvertercap.txt`](../examples/cmosinvertercap.txt) — CMOS Inverter (w/capacitance)
- [`cmosinverterslow.txt`](../examples/cmosinverterslow.txt) — CMOS Inverter (slow transition)
- [`cmostransgate.txt`](../examples/cmostransgate.txt) — CMOS Transmission Gate
- [`mux.txt`](../examples/mux.txt) — CMOS Multiplexer
- [`samplenhold.txt`](../examples/samplenhold.txt) — Sample-and-Hold
- [`delayrc.txt`](../examples/delayrc.txt) — Delayed Buffer
- [`leadingedge.txt`](../examples/leadingedge.txt) — Leading-Edge Detector
- [`switchfilter.txt`](../examples/switchfilter.txt) — Switchable Filter
- [`voltinvert.txt`](../examples/voltinvert.txt) — Voltage Inverter
- [`invertamp.txt`](../examples/invertamp.txt) — Inverter Amplifier
- [`inv-osc.txt`](../examples/inv-osc.txt) — Inverter Oscillator
- [`crystalosc.txt`](../examples/crystalosc.txt) — CMOS Crystal Oscillator

## 555 Timer Chip

- [`555square.txt`](../examples/555square.txt) — Square Wave Generator
- [`555int.txt`](../examples/555int.txt) — Internals
- [`555saw.txt`](../examples/555saw.txt) — Sawtooth Oscillator
- [`555lowduty.txt`](../examples/555lowduty.txt) — Low-duty-cycle Oscillator
- [`555monostable.txt`](../examples/555monostable.txt) — Monostable Multivibrator
- [`555pulsemod.txt`](../examples/555pulsemod.txt) — Pulse Width Modulator
- [`555sequencer.txt`](../examples/555sequencer.txt) — Pulse Sequencer
- [`555schmitt.txt`](../examples/555schmitt.txt) — Schmitt Trigger (inverting)
- [`555missing.txt`](../examples/555missing.txt) — Missing Pulse Detector
- [`555dutycycle.txt`](../examples/555dutycycle.txt) — Adjustable Duty Cycle Oscillator

## Active Filters

- [`filt-vcvs-lopass.txt`](../examples/filt-vcvs-lopass.txt) — VCVS Low-Pass Filter
- [`filt-vcvs-hipass.txt`](../examples/filt-vcvs-hipass.txt) — VCVS High-Pass Filter
- [`switchedcap.txt`](../examples/switchedcap.txt) — Switched-Capacitor Filter
- [`allpass1.txt`](../examples/allpass1.txt) — Allpass
- [`allpass2.txt`](../examples/allpass2.txt) — Allpass w/ Square
- [`actbutterlo.txt`](../examples/actbutterlo.txt) — Butterworth Low-Pass
- [`actbutterhi.txt`](../examples/actbutterhi.txt) — Butterworth High-Pass
- [`actbutterband.txt`](../examples/actbutterband.txt) — Butterworth Band-Pass

## Logic Families


### RTL

- [`rtlinverter.txt`](../examples/rtlinverter.txt) — RTL Inverter
- [`rtlnor.txt`](../examples/rtlnor.txt) — RTL NOR
- [`rtlnand.txt`](../examples/rtlnand.txt) — RTL NAND

### DTL

- [`dtlinverter.txt`](../examples/dtlinverter.txt) — DTL Inverter
- [`dtlnand.txt`](../examples/dtlnand.txt) — DTL NAND
- [`dtlnor.txt`](../examples/dtlnor.txt) — DTL NOR

### TTL

- [`ttlinverter.txt`](../examples/ttlinverter.txt) — TTL Inverter
- [`ttlnand.txt`](../examples/ttlnand.txt) — TTL NAND
- [`ttlnor.txt`](../examples/ttlnor.txt) — TTL NOR
- [`fanout.txt`](../examples/fanout.txt) — Fan-Out

### NMOS

- [`nmosinverter.txt`](../examples/nmosinverter.txt) — NMOS Inverter
- [`nmosinverter2.txt`](../examples/nmosinverter2.txt) — Inverter with only MOSFETs
- [`nmosinverter3.txt`](../examples/nmosinverter3.txt) — Depletion-load NMOS Inverter
- [`nmosnand.txt`](../examples/nmosnand.txt) — NMOS NAND

### CMOS

- [`cmosinverter.txt`](../examples/cmosinverter.txt) — CMOS Inverter
- [`cmosnand.txt`](../examples/cmosnand.txt) — CMOS NAND
- [`cmosnor.txt`](../examples/cmosnor.txt) — CMOS NOR
- [`cmosxor.txt`](../examples/cmosxor.txt) — CMOS XOR
- [`cmosff.txt`](../examples/cmosff.txt) — CMOS Flip-Flop
- [`cmosmsff.txt`](../examples/cmosmsff.txt) — CMOS Master-Slave Flip-Flop

### ECL

- [`eclnor.txt`](../examples/eclnor.txt) — ECL NOR/OR

### Ternary

- [`3-cgand.txt`](../examples/3-cgand.txt) — CGAND
- [`3-cgor.txt`](../examples/3-cgor.txt) — CGOR
- [`3-invert.txt`](../examples/3-invert.txt) — Complement (F210)
- [`3-f211.txt`](../examples/3-f211.txt) — F211
- [`3-f220.txt`](../examples/3-f220.txt) — F220
- [`3-f221.txt`](../examples/3-f221.txt) — F221

## Combinational Logic

- [`xor.txt`](../examples/xor.txt) — Exclusive OR
- [`halfadd.txt`](../examples/halfadd.txt) — Half Adder
- [`fulladd.txt`](../examples/fulladd.txt) — Full Adder
- [`decoder.txt`](../examples/decoder.txt) — 1-of-4 Decoder
- [`priencoder.txt`](../examples/priencoder.txt) — Priority Encoder
- [`mux3state.txt`](../examples/mux3state.txt) — 2-to-1 Mux
- [`majority.txt`](../examples/majority.txt) — Majority Logic
- [`digcompare.txt`](../examples/digcompare.txt) — 2-Bit Comparator
- [`7segdecoder.txt`](../examples/7segdecoder.txt) — 7-Segment LED Decoder
- [`brentkung.txt`](../examples/brentkung.txt) — Brent-Kung Adder
- [`alu74181.txt`](../examples/alu74181.txt) — 74181 ALU

## Sequential Logic


### Flip-Flops

- [`nandff.txt`](../examples/nandff.txt) — SR Flip-Flop
- [`clockedsrff.txt`](../examples/clockedsrff.txt) — Clocked SR Flip-Flop
- [`masterslaveff.txt`](../examples/masterslaveff.txt) — Master-Slave Flip-Flop
- [`edgedff.txt`](../examples/edgedff.txt) — Edge-Triggered D Flip-Flop
- [`jkff.txt`](../examples/jkff.txt) — JK Flip-Flop

### Counters

- [`counter.txt`](../examples/counter.txt) — 4-Bit Ripple Counter
- [`counter8.txt`](../examples/counter8.txt) — 8-Bit Ripple Counter
- [`synccounter.txt`](../examples/synccounter.txt) — Synchronous Counter
- [`updownctr.txt`](../examples/updownctr.txt) — Up/Down Counter
- [`deccounter.txt`](../examples/deccounter.txt) — Decimal Counter
- [`graycode.txt`](../examples/graycode.txt) — Gray Code Counter
- [`johnsonctr.txt`](../examples/johnsonctr.txt) — Johnson Counter
- [`ringcascade.txt`](../examples/ringcascade.txt) — Cascading Ring Counters

### Shift Registers

- [`sipo-sr.txt`](../examples/sipo-sr.txt) — Serial-In Parallel-Out
- [`piso-sr.txt`](../examples/piso-sr.txt) — Parallel-In Serial-Out
- [`unishiftreg.txt`](../examples/unishiftreg.txt) — Universal
- [`divideby2.txt`](../examples/divideby2.txt) — Divide-by-2
- [`divideby3.txt`](../examples/divideby3.txt) — Divide-by-3
- [`ledflasher.txt`](../examples/ledflasher.txt) — LED Flasher
- [`traffic.txt`](../examples/traffic.txt) — Traffic Light
- [`sram.txt`](../examples/sram.txt) — Static RAM
- [`dram.txt`](../examples/dram.txt) — Dynamic RAM

### TD4 CPU

- [`td4.txt`](../examples/td4.txt) — TD4 LED Strobe
- [`td4-ctr.txt`](../examples/td4-ctr.txt) — TD4 Counter
- [`td4-ctr-dn.txt`](../examples/td4-ctr-dn.txt) — TD4 Down Counter
- [`td4-ctr-up-dn.txt`](../examples/td4-ctr-up-dn.txt) — TD4 Up-Down Counter
- [`td4-add2.txt`](../examples/td4-add2.txt) — TD4 Add 2

## Analog/Digital

- [`flashadc.txt`](../examples/flashadc.txt) — Flash ADC
- [`deltasigma.txt`](../examples/deltasigma.txt) — Delta-Sigma ADC
- [`hfadc.txt`](../examples/hfadc.txt) — Half-Flash (Subranging) ADC
- [`dac.txt`](../examples/dac.txt) — Binary-Weighted DAC
- [`r2rladder.txt`](../examples/r2rladder.txt) — R-2R Ladder DAC
- [`swtreedac.txt`](../examples/swtreedac.txt) — Switch-Tree DAC
- [`digsine.txt`](../examples/digsine.txt) — Digital Sine Wave
- [`qam-256.txt`](../examples/qam-256.txt) — QAM-256 Modulator/Demodulator

## Power Converters

- [`conv-boost.txt`](../examples/conv-boost.txt) — Boost Converter
- [`conv-buck.txt`](../examples/conv-buck.txt) — Buck Converter
- [`conv-buckboost.txt`](../examples/conv-buckboost.txt) — Buck-Boost Converter
- [`conv-cuk.txt`](../examples/conv-cuk.txt) — Ćuk Converter
- [`conv-sepic.txt`](../examples/conv-sepic.txt) — SEPIC Converter

## Phase-Locked Loops

- [`xorphasedet.txt`](../examples/xorphasedet.txt) — XOR Phase Detector
- [`pll.txt`](../examples/pll.txt) — Type I PLL
- [`phasecomp.txt`](../examples/phasecomp.txt) — Phase Comparator (Type II)
- [`phasecompint.txt`](../examples/phasecompint.txt) — Phase Comparator Internals
- [`pll2.txt`](../examples/pll2.txt) — Type II PLL
- [`pll2a.txt`](../examples/pll2a.txt) — Type II PLL (fast)
- [`freqdouble.txt`](../examples/freqdouble.txt) — Frequency Doubler

## Transmission Lines

- [`tl.txt`](../examples/tl.txt) — Simple TL
- [`tlstand.txt`](../examples/tlstand.txt) — Standing Wave
- [`tlterm.txt`](../examples/tlterm.txt) — Termination
- [`tlmismatch.txt`](../examples/tlmismatch.txt) — Mismatched lines (Pulse)
- [`tlmis1.txt`](../examples/tlmis1.txt) — Mismatched lines (Standing Wave)
- [`tlmatch1.txt`](../examples/tlmatch1.txt) — Impedance Matching (L-Section)
- [`tlmatch2.txt`](../examples/tlmatch2.txt) — Impedance Matching (Shunt Stub)
- [`tlfreq.txt`](../examples/tlfreq.txt) — Stub Frequency Response
- [`tllopass.txt`](../examples/tllopass.txt) — Low-Pass Filter
- [`tllight.txt`](../examples/tllight.txt) — Light Switch

## Controlled Sources

- [`cs-resistor.txt`](../examples/cs-resistor.txt) — VCCS Resistor
- [`cs-varyresistor.txt`](../examples/cs-varyresistor.txt) — VCCS Varying Resistor
- [`cs-opamp.txt`](../examples/cs-opamp.txt) — VCVS Op-Amp
- [`cs-opamprail.txt`](../examples/cs-opamprail.txt) — VCVS Op-Amp With Rails
- [`cs-multiplier.txt`](../examples/cs-multiplier.txt) — VCVS Multiplier
- [`cs-fullrectifier.txt`](../examples/cs-fullrectifier.txt) — VCVS Full Rectifier
- [`cs-ramp.txt`](../examples/cs-ramp.txt) — VCVS Voltage Ramp
- [`cs-currentadder.txt`](../examples/cs-currentadder.txt) — Current Adder
- [`cs-integrator.txt`](../examples/cs-integrator.txt) — VCVS Integrator
- [`cs-diff.txt`](../examples/cs-diff.txt) — VCVS Differentiator
- [`cs-varinduct.txt`](../examples/cs-varinduct.txt) — CCVS Variable Inductor
- [`cs-varicap.txt`](../examples/cs-varicap.txt) — VCCS Variable Capacitor

## Subcircuits

- [`fullrect-sc.txt`](../examples/fullrect-sc.txt) — Full Rectifier
- [`adder4-sc.txt`](../examples/adder4-sc.txt) — Full Adder (nested)

## Misc Devices


### JFETs

- [`jfetcurrentsrc.txt`](../examples/jfetcurrentsrc.txt) — JFET Current Source
- [`jfetfollower.txt`](../examples/jfetfollower.txt) — JFET Follower
- [`jfetfollower-nooff.txt`](../examples/jfetfollower-nooff.txt) — JFET Follower w/zero offset
- [`jfetamp.txt`](../examples/jfetamp.txt) — Common-Source Amplifier
- [`volume.txt`](../examples/volume.txt) — Volume Control
- [`lambda-diode.txt`](../examples/lambda-diode.txt) — Lambda Diode
- [`lambda-diode-osc.txt`](../examples/lambda-diode-osc.txt) — Lambda Diode Oscillator

### Tunnel Diodes

- [`tdiode.txt`](../examples/tdiode.txt) — I/V Curve
- [`tdosc.txt`](../examples/tdosc.txt) — LC Oscillator
- [`tdrelax.txt`](../examples/tdrelax.txt) — Relaxation Oscillator

### Memristors

- [`mr.txt`](../examples/mr.txt) — Memristor
- [`mr-sine.txt`](../examples/mr-sine.txt) — Sine Wave
- [`mr-square.txt`](../examples/mr-square.txt) — Square Wave
- [`mr-triangle.txt`](../examples/mr-triangle.txt) — Triangle Wave
- [`mr-sine2.txt`](../examples/mr-sine2.txt) — Hard-Switching 1
- [`mr-sine3.txt`](../examples/mr-sine3.txt) — Hard-Switching 2
- [`mr-crossbar.txt`](../examples/mr-crossbar.txt) — Crossbar Memory

### Triodes

- [`triode.txt`](../examples/triode.txt) — Triode
- [`triodeamp.txt`](../examples/triodeamp.txt) — Amplifier

### Silicon-Controlled Rectifiers

- [`scr.txt`](../examples/scr.txt) — SCR
- [`scractrig.txt`](../examples/scractrig.txt) — AC Trigger

### Current Conveyor

- [`cc2.txt`](../examples/cc2.txt) — CCII+
- [`cc2n.txt`](../examples/cc2n.txt) — CCII-
- [`ccinductor.txt`](../examples/ccinductor.txt) — Inductor Simulator
- [`cc2imp.txt`](../examples/cc2imp.txt) — CCII+ Implementation
- [`cc2impn.txt`](../examples/cc2impn.txt) — CCII- Implementation
- [`cciamp.txt`](../examples/cciamp.txt) — Current Amplifier
- [`ccvccs.txt`](../examples/ccvccs.txt) — VCCS
- [`ccdiff.txt`](../examples/ccdiff.txt) — Current Differentiator
- [`ccint.txt`](../examples/ccint.txt) — Current Integrator
- [`ccitov.txt`](../examples/ccitov.txt) — Current-Controlled Voltage Source

### Spark Gap

- [`spark-sawtooth.txt`](../examples/spark-sawtooth.txt) — Sawtooth Generator
- [`tesla.txt`](../examples/tesla.txt) — Tesla Coil
- [`spark-marx.txt`](../examples/spark-marx.txt) — Marx Generator

### Operational Transconductance Amplifier (OTA)

- [`ota-vca.txt`](../examples/ota-vca.txt) — OTA Voltage Controlled Amplifier (VCA)
- [`ota-vcf-single.txt`](../examples/ota-vcf-single.txt) — OTA Single Stage VCF (low pass)
- [`ota-ringmod.txt`](../examples/ota-ringmod.txt) — OTA Ring Modulator
- [`ota-gain.txt`](../examples/ota-gain.txt) — LM137000 Gain Oddity

### Light Bulb

- [`lightbulb.txt`](../examples/lightbulb.txt) — Light Bulb
- [`wienbridge.txt`](../examples/wienbridge.txt) — Wien Bridge Oscillator

### Varactor

- [`varactor.txt`](../examples/varactor.txt) — Varactor
- [`varactorvco.txt`](../examples/varactorvco.txt) — VCO

### Norton Amplifier

- [`norton-invert.txt`](../examples/norton-invert.txt) — Norton Inverting Amplifier
- [`norton-noninvert.txt`](../examples/norton-noninvert.txt) — Norton Noninverting Amplifier
- [`norton-saw.txt`](../examples/norton-saw.txt) — Norton Sawtooth Oscillator
- [`ledarray.txt`](../examples/ledarray.txt) — LED Array
- [`triacdimmer.txt`](../examples/triacdimmer.txt) — DIAC/TRIAC Dimmer
- [`ujtosc.txt`](../examples/ujtosc.txt) — Unijunction Oscillator
- [`3motor.txt`](../examples/3motor.txt) — 3-Phase Motor
- [`latchingrelay.txt`](../examples/latchingrelay.txt) — Latching Relay
- [`gyratorelm.txt`](../examples/gyratorelm.txt) — Gyrator

## 2-D Scope

- [`lissa.txt`](../examples/lissa.txt) — Lissajous Figures
- [`plot2d-checker.txt`](../examples/plot2d-checker.txt) — Checkerboard
- [`plot2d-color.txt`](../examples/plot2d-color.txt) — Color Checkerboard
- [`plot2d-smile.txt`](../examples/plot2d-smile.txt) — Smiley
- [`blank.txt`](../examples/blank.txt) — Blank Circuit

## Other files (not in the categorized menu)

- [`analogrecip.txt`](../examples/analogrecip.txt) — Analog reciprocal (uses function-source `f` element)
- [`avr8js-analog.txt`](../examples/avr8js-analog.txt) — AVR8js microcontroller simulation, analog pins
- [`avr8js-logic.txt`](../examples/avr8js-logic.txt) — AVR8js microcontroller simulation, logic pins
- [`avr8js-strobe.txt`](../examples/avr8js-strobe.txt) — AVR8js microcontroller simulation, strobe pins
- [`jsinterface.txt`](../examples/jsinterface.txt) — Demo circuit for the JavaScript interface
- [`motorprotect.txt`](../examples/motorprotect.txt) — Motor protection circuit
- [`relays.txt`](../examples/relays.txt) — Relay examples
