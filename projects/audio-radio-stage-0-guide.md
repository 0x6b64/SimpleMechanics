# Stage 0 — Complete Electronics Fundamentals Lab Guide

This document turns **Stage 0** of [`projects/audio-radio-from-scratch.md`](./audio-radio-from-scratch.md) into an executable bench procedure. It intentionally stops before the loudspeaker build in Stage 1.

## Objective

Complete Stage 0 in roughly **4–6 focused hours** and leave with enough practical skill to:

- reason about voltage, current, resistance, and power;
- build and measure series/parallel resistor networks;
- observe RC charging and frequency response;
- explain the role of inductors and magnetic fields;
- observe diode rectification;
- use an NPN transistor as a switch;
- build and characterize a common-emitter amplifier;
- operate a multimeter, function generator, and oscilloscope safely;
- make and inspect a basic solder joint.

The goal is not to master circuit theory. The goal is to predict a circuit's behavior, build it, measure it, and explain discrepancies.

---

## 1. What You Need

### Required components

| Part | Quantity | Notes |
|---|---:|---|
| Solderless breadboard | 1 | Full- or half-size |
| Jumper wires | ~20 | Solid-core breadboard jumpers |
| 5 V DC supply | 1 | Current-limited bench supply preferred; regulated 5 V source is acceptable |
| 1 kΩ resistor | 3+ | 1/4 W |
| 330 Ω resistor | 1+ | LED current limiting |
| 2.2 kΩ resistor | 1+ | Amplifier collector resistor |
| 10 kΩ resistor | 3+ | Divider/RC/bias experiments |
| 15 kΩ resistor | 1+ | Amplifier bias |
| 47 kΩ resistor | 1+ | Amplifier bias |
| 100 nF capacitor | 1+ | RC experiment |
| 1 µF capacitor | 2+ | Coupling; electrolytic is acceptable if polarity is observed |
| 10 µF capacitor | 1 | Optional amplifier emitter bypass experiment |
| 1N4148 diode | 1+ | Rectification |
| 2N3904 NPN transistor | 1+ | Verify the pinout for the exact manufacturer/package you have |
| LED | 1+ | Any ordinary visible LED |
| Pushbutton | 1 | Optional; a jumper can substitute |

### Required tools

- Digital multimeter (DMM)
- Function generator
- Two-channel oscilloscope with probes
- Breadboard and leads

### Soldering exercise

- Soldering iron with stand
- Electronics solder
- Scrap perfboard or spare through-hole component leads
- Wire cutters/strippers
- Eye protection

If no oscilloscope/function generator is available, you can complete the DC labs but **Stage 0 is not complete** under the parent plan until you can generate and observe an AC waveform and characterize the RC/amplifier circuits.

---

## 2. Safety and Instrument Rules

1. Use **5 V** for every powered circuit in this guide.
2. If using a bench supply, set the current limit to approximately **50 mA** before first power-up. Increase it only if a known-good circuit requires it.
3. Never connect a DMM configured for current measurement directly across a voltage source. In current mode the meter presents a low-resistance path and can blow its fuse or damage equipment.
4. Measure voltage **in parallel** between two nodes. Measure current by **breaking the circuit and inserting the meter in series**.
5. Power the circuit off before changing transistor, diode, or electrolytic-capacitor wiring.
6. Verify transistor pinout from the datasheet for the exact part you own. Do not assume all TO-92 2N3904 parts have the same physical lead order.
7. Observe electrolytic capacitor polarity.
8. The ground clips of ordinary bench oscilloscopes/function generators are commonly earth-referenced. In these low-voltage experiments, connect instrument grounds only to the circuit's defined **GND** node.
9. Do not use mains voltage anywhere in Stage 0.
10. Treat the soldering-iron tip and freshly soldered joints as burn hazards; wear eye protection when clipping leads.

---

## 3. Bench Setup

Create two breadboard rails:

```text
+5 V  =================================
GND   =================================
```

Before installing any circuit:

1. Set the supply to 5.0 V with the output disabled.
2. Set current limit to ~50 mA.
3. Connect supply positive to the +5 V rail and supply negative to GND.
4. Enable the supply.
5. Put the DMM in DC-voltage mode.
6. Measure between +5 V and GND.

**Expected:** approximately 5.0 V.

If polarity is negative on the DMM, your probes are reversed. If voltage is near zero, check supply enable, rail continuity, and wiring.

Use this notebook format for every lab:

```text
Question:
Circuit:
Prediction:
Measurement:
Difference:
Explanation:
Change made:
Result:
```

---

# Lab 0A — Ohm's Law

## Concepts

```text
V = I R
I = V / R
P = V I = I²R = V²/R
```

Voltage is a potential difference between two nodes. Current is charge flow through a path. Resistance relates the voltage across a component to the current through it.

## Circuit

Use a 1 kΩ resistor:

```text
+5 V ---- 1 kΩ ---- GND
```

## Predict

For a nominal 1 kΩ resistor and 5 V supply:

```text
I = 5 V / 1000 Ω = 5 mA
P = 5 V × 5 mA = 25 mW
```

A 1/4 W resistor is comfortably within its rating.

## Procedure

1. Turn power off.
2. Remove the 1 kΩ resistor from the circuit and measure its resistance with the DMM in resistance mode. Record (R_measured).
3. Reinstall it between +5 V and GND.
4. Turn power on.
5. Measure the voltage directly across the resistor. Record (V_measured).
6. Calculate (I_predicted = V_measured / R_measured).
7. Turn power off.
8. Move the DMM lead to the meter's current input if required and select DC-current mode.
9. Break the circuit between +5 V and the resistor.
10. Insert the meter in series:

```text
+5 V ---- DMM(A) ---- 1 kΩ ---- GND
```

11. Turn power on and record current.
12. Turn power off and return the DMM lead to the voltage/resistance socket immediately.

## Pass criteria

- Measured current is reasonably close to (V_measured/R_measured) (normally within a few percent given component and instrument tolerances).
- You can explain why an ammeter goes in series and a voltmeter goes in parallel.
- You can answer: if R doubles at fixed V, current halves and power (V²/R) halves.

---

# Lab 0B — Series/Parallel Networks and Voltage Divider

## Concepts

For the unloaded divider:

```text
Vout = Vin × R2 / (R1 + R2)
```

Kirchhoff's current law: current entering a node equals current leaving it.

Kirchhoff's voltage law: voltage rises and drops around a closed loop sum to zero.

## Circuit 1 — Equal divider

Use two 10 kΩ resistors:

```text
+5 V ---- 10 kΩ ----+---- 10 kΩ ---- GND
                    |
                  Vout
```

## Predict

```text
Vout = 5 × 10k/(10k+10k) = 2.5 V
Series current = 5/20k = 0.25 mA
```

## Procedure

1. Power off and build the divider.
2. Power on.
3. Measure +5 V-to-GND, Vout-to-GND, and the voltage across each resistor.
4. Verify that the two resistor drops approximately add to the supply voltage.
5. Replace the lower 10 kΩ resistor with 1 kΩ.
6. Predict before measuring:

```text
Vout = 5 × 1k/(10k+1k) ≈ 0.455 V
```

7. Measure Vout.

## Circuit 2 — Loading

Restore the 10 kΩ/10 kΩ divider. Measure unloaded Vout (~2.5 V).

Now place another 10 kΩ resistor from Vout to GND. The two lower 10 kΩ resistors are now in parallel:

```text
Rlower = 10k || 10k = 5k
Vout = 5 × 5k/(10k+5k) ≈ 1.67 V
```

Measure Vout.

## Pass criteria

- Equal divider measures near 2.5 V.
- 10 kΩ/1 kΩ divider measures near 0.455 V.
- Loaded divider falls near 1.67 V.
- You can explain loading: the load changes the effective lower resistance and therefore the divider ratio.

---

# Lab 0C — Capacitor and RC Response

## Concepts

For a first-order RC circuit:

```text
τ = RC
fc = 1/(2πRC)
```

Use:

- R = 10 kΩ
- C = 100 nF

Therefore:

```text
τ = 10,000 × 100e-9 = 1 ms
fc ≈ 159 Hz
```

At one time constant after a rising step, capacitor voltage is about 63% of the final change. At five time constants it is effectively settled for this experiment.

## Circuit — RC low-pass

```text
Vin ---- 10 kΩ ----+---- Vout
                   |
                 100 nF
                   |
                  GND
```

### Function generator setup

- Waveform: square
- Frequency: 100 Hz
- Low level: 0 V
- High level: about 5 V

If your generator is specified in amplitude/offset rather than high/low levels, configure an equivalent 0–5 V waveform and verify it on the oscilloscope before attaching the RC circuit.

### Oscilloscope setup

- CH1: Vin
- CH2: Vout
- Both probe grounds: circuit GND
- DC coupling
- Start around 1 V/div and 1 ms/div
- Trigger from CH1 rising edge

## Procedure A — Step response

1. Predict (	au = 1 ms).
2. Apply the 100 Hz square wave.
3. Observe CH1 and CH2 simultaneously.
4. On a rising edge, measure how long Vout takes to reach approximately 63% of its final transition.
5. Compare with 1 ms.
6. Observe the exponential charge/discharge shape.

## Procedure B — Frequency response

Switch the generator to a sine wave with approximately 1 Vpp and 0 V offset.

Measure (Vin_{pp}) and (Vout_{pp}) at:

| Frequency | Expected qualitative result |
|---:|---|
| 16 Hz (~0.1 fc) | Vout nearly Vin |
| 159 Hz (~fc) | Vout ≈ 0.707 × Vin |
| 1.59 kHz (~10 fc) | Vout much smaller, ≈ 0.10 × Vin |

For a first-order low-pass:

```text
|H(f)| = 1 / sqrt(1 + (f/fc)²)
```

## Pass criteria

- Measured time constant is recognizably close to 1 ms.
- The output decreases as frequency rises.
- Around 159 Hz, the amplitude ratio is roughly 0.707.
- You can explain that a capacitor can pass changing signals while preventing a steady DC path in a series-coupling configuration.

---

# 0D Preparation — Inductors and Magnetism

No separate powered inductor lab is required by the parent Stage 0, but understand these points before continuing:

- Current through a conductor creates a magnetic field.
- An ideal inductor stores energy in a magnetic field: (E = rac{1}{2}LI²).
- An inductor opposes rapid changes in current.
- Inductive reactance is (X_L = 2πfL), so opposition to AC increases with frequency.
- A changing magnetic flux can induce a voltage.

If you have an inductor, measure its **DC resistance** with the DMM. Do not confuse that resistance with its frequency-dependent inductive reactance. These ideas are prerequisites for the Stage 1 speaker and later LC radio tuner.

---

# Lab 0D — Diode Rectification

## Concepts

A diode conducts much more readily in one direction than the other. A silicon diode such as the 1N4148 commonly exhibits a forward drop on the order of ~0.6–0.8 V at ordinary small currents, but treat this as an operating approximation, not a universal constant.

## Circuit

```text
Vin ----|>|----+---- Vout
       1N4148  |
              1 kΩ
               |
              GND
```

The diode's band marks the **cathode**.

### Generator setup

- Sine wave
- 1 kHz
- 4 Vpp
- 0 V offset

### Scope

- CH1 = Vin
- CH2 = Vout
- DC coupling
- Grounds = circuit GND

## Procedure A — Half-wave rectifier

1. Apply the sine wave.
2. Observe both channels.
3. Positive input portions above the diode's forward threshold should appear at Vout, reduced by the diode drop.
4. Negative portions should be strongly suppressed.
5. Reverse the diode and observe that the opposite half-cycle is passed.

## Procedure B — Add envelope smoothing

Add a 1 µF capacitor from Vout to GND:

```text
Vin ----|>|----+---- Vout
               |
             +-+-+
             |   |
           1 kΩ  1 µF
             |   |
             +-+-+
               |
              GND
```

The load/capacitor time constant is approximately:

```text
τ = 1 kΩ × 1 µF = 1 ms
```

Observe that the capacitor charges near waveform peaks and discharges through the resistor between peaks, producing a smoother waveform. This is the core intuition later used in AM envelope detection.

## Pass criteria

- You can identify which half-cycle is conducted.
- Reversing the diode reverses the passed polarity.
- Adding the capacitor visibly changes the rectified waveform.
- You can explain why diode forward voltage matters for weak signals.

---

# Lab 0E — 2N3904 Transistor as a Switch

## Concepts

A BJT has base, collector, and emitter terminals. In this experiment the transistor is used in two obvious states:

- **cutoff:** negligible base drive, LED off;
- **saturation/on:** sufficient base drive, LED on.

## Circuit

First verify your 2N3904 pinout from its datasheet.

```text
+5 V ---- 330 Ω ---- LED ---- Collector
                               |
                            2N3904
                               |
Emitter ---------------------- GND

+5 V ---- switch/jumper ---- 1 kΩ ---- Base
```

LED polarity: anode toward +5 V; cathode toward the transistor collector.

## Predict

If the LED forward voltage is approximately 2 V and transistor (V_{CE}) is small when on:

```text
ILED ≈ (5 - 2 - 0.2)/330 ≈ 8.5 mA
```

This is only an estimate; LED forward voltage varies.

## Procedure

1. Power off and build the circuit.
2. Leave the base resistor disconnected from +5 V.
3. Power on. LED should be off.
4. Connect the 1 kΩ base resistor to +5 V. LED should turn on.
5. Measure (V_B), (V_C), and (V_E) relative to GND in the on state.
6. Remove base drive and measure collector voltage again.
7. Explain why a small base-control signal changes a larger collector/load current.

## Troubleshooting

- LED never lights: check LED polarity, transistor pinout, base resistor connection, supply, and breadboard row placement.
- LED always lights: check for collector-emitter miswiring or an unintended base connection.
- Supply current limit activates: power off immediately and inspect for shorts.

## Pass criteria

You can deliberately switch the LED on/off through the transistor and identify cutoff versus the on/saturated state.

---

# Lab 0F — Common-Emitter Amplifier

This is the most important Stage 0 analog lab. The objective is to see a small AC signal riding on a DC bias point, then observe an amplified and inverted collector waveform.

## Circuit

Use:

- VCC = 5 V
- R1 = 47 kΩ from +5 V to base
- R2 = 15 kΩ from base to GND
- RC = 2.2 kΩ from +5 V to collector
- RE = 1 kΩ from emitter to GND
- Cin = 1 µF from generator to base
- 2N3904 transistor

```text
                       +5 V
                        |
                      2.2 kΩ
                        |
                        +------ Collector ---- Vout
                        |
                       C
Generator -- 1 µF --+--B  2N3904
                    |  E
          +5 V--47k |  |
                    |  1 kΩ
             GND-15k  |
                    |  |
                    +--+---- GND
```

The 47 kΩ and 15 kΩ resistors form the DC base-bias divider. Cin prevents the generator's DC level from directly disturbing that bias.

If using a polarized 1 µF electrolytic for Cin, first measure the DC voltage on both sides in the intended setup and orient the capacitor so its positive terminal is toward the side with the higher DC potential. A non-polarized capacitor is simpler.

## Predict the DC operating point

Ignoring base loading for a first estimate:

```text
VB ≈ 5 × 15/(47+15) ≈ 1.21 V
VE ≈ VB - 0.7 ≈ 0.51 V
IE ≈ 0.51 V / 1 kΩ ≈ 0.51 mA
VC ≈ 5 - (0.51 mA × 2.2 kΩ) ≈ 3.88 V
```

Real measurements will differ because transistor gain and base current load the divider.

## Procedure A — DC bias

1. Disconnect/disable the function-generator output.
2. Power the amplifier.
3. Measure base, emitter, and collector DC voltages relative to GND.
4. Record them.
5. Confirm the transistor is neither obviously cutoff ((VC) near 5 V with emitter near 0 V) nor hard saturated ((VC) very near (VE)).

The exact voltages are less important than obtaining a sensible active-region bias point with room for the collector voltage to swing.

## Procedure B — AC gain

Generator:

- sine wave
- 1 kHz
- begin at **20 mVpp**
- 0 V generator offset

Oscilloscope:

- CH1 on the generator side of Cin
- CH2 on collector
- grounds to circuit GND
- use DC coupling initially so the collector's DC bias is visible

1. Enable the generator.
2. Observe input and collector waveforms.
3. Measure input (Vpp).
4. Measure output (Vpp).
5. Calculate approximate voltage gain magnitude:

```text
|Av| = Vout_pp / Vin_pp
```

6. Observe that the collector waveform is approximately **180° inverted** relative to the input.
7. Gradually increase input amplitude until distortion/clipping becomes visible, then reduce it again.

### Optional experiment — emitter bypass

Place 10 µF across the 1 kΩ emitter resistor, positive toward the emitter and negative toward GND. Repeat the gain measurement. Gain should increase substantially because the capacitor reduces AC emitter degeneration at 1 kHz.

## What bias vs signal means

- **Bias** establishes the transistor's DC operating point.
- **Signal** is the time-varying perturbation around that operating point.
- The output energy does not come from the input signal; the transistor controls energy supplied by the 5 V source.

## Pass criteria

- DC node voltages show a valid active operating point.
- A 1 kHz collector waveform is visible.
- Output amplitude is larger than the small input amplitude for a suitable operating point.
- Output is inverted.
- You can calculate approximate voltage gain.
- You can explain bias separately from signal.
- You can intentionally demonstrate clipping by increasing input amplitude.

---

# Lab 0G — Oscilloscope Skills Check

Use the 1 kHz sine wave from Lab 0F.

Without referring to a tutorial, demonstrate:

1. Set vertical scale so the waveform occupies several divisions.
2. Set timebase so several cycles are visible.
3. Trigger from CH1 and obtain a stationary trace.
4. Measure peak-to-peak amplitude.
5. Measure period.
6. Calculate frequency from (f = 1/T).
7. Verify that 1 kHz corresponds to approximately 1 ms.
8. Display input and output simultaneously on two channels.
9. Switch a channel between DC and AC coupling and explain what disappeared: AC coupling removes the displayed DC component, not the actual circuit bias.

**Pass:** you can obtain a stable trace and make amplitude/frequency measurements without trial-and-error dependence on autoset.

---

# Lab 0H — Basic Soldering and Continuity

Stage 0 lists soldering as a prerequisite. Do this on scrap/perfboard, not on the breadboard circuit.

## Procedure

1. Put on eye protection and place the iron securely in its stand.
2. Heat the iron according to the solder/iron manufacturer's guidance.
3. If needed, clean the tip using the appropriate brass wool or damp sponge and apply a small amount of solder to wet/tin the tip.
4. Insert a spare resistor into perfboard.
5. Touch the iron so it heats both the component lead and copper pad.
6. Feed a small amount of solder into the heated joint, not directly onto an untouched iron tip.
7. Remove solder, then remove the iron.
8. Let the joint cool without movement.
9. Inspect it: the solder should wet both lead and pad and should not bridge adjacent pads.
10. Clip the excess lead while wearing eye protection.
11. With the board unpowered, use DMM continuity/resistance mode to verify the intended connection and verify there is no short to the neighboring pad.
12. Make at least three joints and intentionally desolder/rework one if you have suitable wick or a solder sucker.

Use ventilation appropriate for soldering and wash hands after handling solder. Follow the solder manufacturer's handling guidance, especially if using leaded solder.

## Pass criteria

- Joint mechanically holds the component.
- Electrical continuity exists through the intended connection.
- No adjacent short is present.
- You can recognize and rework a poorly wetted or bridged joint.

---

# 4. Stage 0 Final Knowledge Gate

Answer these without looking up the answers.

1. What is voltage measured between?
2. Why is current measurement performed in series?
3. A 5 V source is applied to 1 kΩ. What current and resistor power do you expect?
4. What happens to current and power if resistance doubles at fixed voltage?
5. Why does a voltage divider change when loaded?
6. What do Kirchhoff's current and voltage laws state qualitatively?
7. For R = 10 kΩ and C = 100 nF, what are (	au) and (f_c)?
8. Why does an RC low-pass attenuate high frequencies?
9. What does an inductor store, and how does its reactance change with frequency?
10. What does a diode do to a bipolar sine wave in the half-wave rectifier?
11. Why does adding an RC after a diode smooth the rectified waveform?
12. What are the base, collector, and emitter?
13. What are cutoff and saturation?
14. What is transistor bias, and how is it different from the AC signal?
15. Where does an amplifier's extra output energy come from?
16. Why is a common-emitter output inverted?
17. What are volts/div, time/div, and trigger used for?
18. What is the period of a 1 kHz signal?
19. What is the difference between oscilloscope AC and DC coupling?
20. Why must transistor pinout and electrolytic polarity be checked before power-up?

If any answer is only memorized wording, return to the corresponding measurement and explain the causal mechanism.

---

# 5. Definition of Done

Stage 0 is complete only when all of the following are true:

- [ ] DMM verified a ~5 V supply.
- [ ] Lab 0A: predicted and measured resistor current.
- [ ] Lab 0B: predicted/measured unloaded and loaded voltage dividers.
- [ ] Lab 0C: observed RC step response and frequency-dependent attenuation.
- [ ] Inductor/magnetism concepts can be explained qualitatively.
- [ ] Lab 0D: observed diode half-wave rectification and RC smoothing.
- [ ] Lab 0E: switched an LED with a 2N3904.
- [ ] Lab 0F: measured common-emitter DC bias and AC gain/inversion.
- [ ] Lab 0G: independently operated a two-channel oscilloscope and measured 1 kHz ≈ 1 ms.
- [ ] Lab 0H: made and continuity-tested basic solder joints.
- [ ] All 20 final knowledge-gate questions can be answered from first principles.
- [ ] Lab notebook contains predictions and measurements for Labs 0A–0H.

Once this checklist is complete, proceed to **Stage 1 — Loudspeaker** in the parent project.

---

# 6. Troubleshooting Order

When a circuit does not work, do not randomly replace components. Check in this order:

1. **Power:** Is +5 V actually present relative to GND?
2. **Ground:** Do supply, generator, and scope share the intended circuit reference?
3. **Placement:** Are breadboard rows/rails connected the way you think they are?
4. **Value:** Measure resistor values; read capacitor markings.
5. **Polarity/orientation:** LED, diode, electrolytic capacitor, transistor pinout.
6. **DC operating point:** Measure node voltages before reasoning about AC behavior.
7. **Input:** Verify the function-generator waveform on the scope before the circuit.
8. **Stage boundary:** Compare input and output of one block at a time.
9. **Prediction:** State what voltage/waveform you expected before changing anything.
10. **Change one variable:** Modify one thing, remeasure, and record the result.

This same debug discipline should be carried into every later audio and RF stage.

---

# 7. Minimal Reference Set

Use the references already selected by the parent plan rather than adding a large reading list:

- All About Circuits, Direct Current: https://www.allaboutcircuits.com/textbook/direct-current/
- All About Circuits, Alternating Current: https://www.allaboutcircuits.com/textbook/alternating-current/
- All About Circuits, Semiconductors: https://www.allaboutcircuits.com/textbook/semiconductors/
- MIT OpenCourseWare 6.002, only when a concept needs more depth: https://ocw.mit.edu/courses/6-002-circuits-and-electronics-spring-2007/

Read only enough theory to predict the next measurement. Stage 0 is complete through measured behavior, not through finishing a textbook.
