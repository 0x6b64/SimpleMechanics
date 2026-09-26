# DIY Audio and Radio Learning & Build Plan

## Goal

Build, from bare components and with minimal black-box modules:

1. A simple loudspeaker
2. A simple dynamic microphone
3. A basic AM radio receiver
4. A basic amateur-radio receiver/transceiver

The learning philosophy is **just-in-time fundamentals**: study only the theory needed for the next build, then immediately validate it in hardware.

## Overall Sequence

| Stage | Learn | Build | Estimated Time |
|---|---|---|---:|
| 0 | DC circuits, measurement, soldering | Basic test circuits | 4–6 h |
| 1 | Magnetism, Lorentz force, AC signals | Loudspeaker | 4–8 h |
| 2 | Electromagnetic induction | Dynamic microphone | 4–8 h |
| 3 | RLC resonance, diodes, envelopes, amplification | AM receiver | 10–20 h |
| 4 | Oscillators, mixing, filtering, RF amplification, antennas | Amateur-radio receiver | 20–40 h |
| 5 | Modulation, transmit chains, impedance matching, RF safety/regulation | Low-power ham transceiver | 20–40+ h |

Total: roughly **60–120 hours**, depending on how deeply each build is instrumented and debugged.

---

# Stage 0 — Electronics Fundamentals and Bench Setup

## Learn

Understand only these concepts before starting:

- Voltage, current, resistance
- Ohm's law: `V = IR`
- Electrical power: `P = VI`
- Series and parallel circuits
- Capacitors: charge storage, AC coupling, filtering
- Inductors: magnetic fields and opposition to changing current
- Diodes: one-way conduction and rectification
- BJT/MOSFET basics: transistor as switch and amplifier
- DC versus AC
- Frequency, period, amplitude
- Ground/reference voltage
- Breadboarding and soldering

Do not study semiconductor physics or advanced circuit analysis yet.

## Bench Tools

Required:

- Digital multimeter
- Breadboards
- Jumper wires
- Soldering iron and solder
- Wire cutters/strippers
- Small pliers
- Magnet wire
- Hookup wire
- AA battery holder and/or 9 V battery clips
- Bench power supply if available

Strongly recommended:

- Oscilloscope
- Function generator

Low-cost USB instruments are sufficient initially.

## Component Starter Kit

- Resistors: 100 Ω to 1 MΩ
- Capacitors: 100 pF, 1 nF, 10 nF, 100 nF, 1 µF, 10 µF, 100 µF
- Assorted µH/mH inductors
- 1N4148 diodes
- 1N400x diodes
- Schottky detector diode such as 1N5711 or BAT46
- 2N3904 and 2N2222 NPN transistors
- 2N3906 PNP transistor
- Small MOSFETs
- 10 kΩ and 100 kΩ potentiometers
- LEDs and pushbuttons

## Exercises

Before proceeding:

1. Measure battery voltage.
2. Calculate and wire an LED current-limiting resistor.
3. Build an RC low-pass filter.
4. Drive an LED with a transistor.
5. Observe an AC waveform with an oscilloscope.

---

# Stage 1 — Build a Loudspeaker From Scratch

## Learn

### Magnetism

Understand:

- Current through wire creates a magnetic field.
- Permanent magnets create static magnetic fields.
- A current-carrying conductor in a magnetic field experiences force.

The useful simplified relationship is:

`F = BIL`

An alternating current therefore produces alternating mechanical force.

### Audio

Understand:

- Sound is air-pressure variation.
- Audio electrical signals are time-varying voltages/currents.
- Human-audible frequencies are approximately 20 Hz–20 kHz.

## Materials

- Neodymium magnet
- 28–34 AWG enamelled copper magnet wire
- Paper or thin plastic diaphragm
- Card stock
- Tape/glue
- Small cylindrical former for winding the coil
- Test leads/audio source
- Optional discrete transistor amplifier

## Build

1. Wind roughly 50–200 turns of magnet wire around a cylindrical former.
2. Secure the winding.
3. Remove enamel from the wire ends.
4. Make a lightweight diaphragm.
5. Attach the coil to its center.
6. Position the permanent magnet inside or immediately adjacent to the coil.
7. Support the diaphragm so it can move axially without rubbing.
8. Apply a low-level audio waveform.
9. Observe motion and listen.
10. Change coil turns, magnet spacing, diaphragm material and frequency.

## Measure

- Coil DC resistance
- Approximate frequency response
- Minimum audible drive voltage
- Effect of magnet spacing

## Completion Criterion

Explain:

`voltage -> current -> magnetic force -> diaphragm motion -> air pressure -> sound`

---

# Stage 2 — Build a Dynamic Microphone

This deliberately reverses the loudspeaker mechanism.

## Learn

Faraday's law:

`V = -N dΦ/dt`

Understand qualitatively:

- Moving a coil through a magnetic field changes magnetic flux.
- Changing flux generates voltage.
- Greater diaphragm velocity generally produces a larger signal.

## Materials

Reuse the magnet, wire and diaphragm materials.

Additional:

- Shielded audio cable
- Resistors/capacitors
- Transistors for a discrete preamplifier

## Build

1. Wind a lightweight coil.
2. Attach it to a thin diaphragm.
3. Suspend it in the permanent magnet's field.
4. Connect the coil to an oscilloscope.
5. Speak into the diaphragm and observe the generated waveform.
6. Build a single-transistor common-emitter amplifier.
7. Feed microphone output into the amplifier.
8. Feed amplified output into the Stage 1 loudspeaker.

## Final Experiment

`voice -> homemade microphone -> discrete amplifier -> homemade speaker`

## Completion Criterion

Explain both conversions:

Speaker: `electrical -> mechanical -> acoustic`

Microphone: `acoustic -> mechanical -> electrical`

---

# Stage 3 — Build an AM Radio Receiver

AM is the best first radio because useful demodulation can be achieved with extremely simple circuitry.

## Learn

### LC Resonance

`f = 1 / (2π√LC)`

Understand that the antenna receives many frequencies while a resonant circuit preferentially selects a frequency range.

### Amplitude Modulation

Understand the RF carrier and the audio information represented by changes in carrier amplitude.

### Envelope Detection

Understand how a diode plus RC network recovers the slowly varying audio envelope.

## Architecture

`Antenna -> LC tuner -> diode detector -> audio amplifier -> speaker`

## Materials

- Ferrite rod
- Magnet wire
- Variable capacitor, approximately 10–365 pF
- Schottky/germanium detector diode
- Resistors/capacitors
- 2N3904/2N2222 transistors
- Several metres of antenna wire
- Crystal earpiece or oscilloscope for initial testing
- Homemade loudspeaker

## Build

1. Wind approximately 50–100 turns around the ferrite rod.
2. Connect the variable capacitor across the coil to make the tuner.
3. Attach the antenna.
4. Add the detector diode.
5. Add the RC envelope filter.
6. Verify recovered audio with a high-impedance earpiece or oscilloscope.
7. Build one or two discrete transistor audio-amplifier stages.
8. Drive the homemade loudspeaker.

Final chain:

`radio wave -> antenna -> resonance -> detection -> amplification -> sound`

## Experiments

Change:

- Antenna length
- Coil turns
- Capacitance
- Diode type
- Amplifier gain

Observe the effect on tuning, selectivity and sensitivity.

---

# Stage 4 — Build an Amateur-Radio Receiver

Start receive-only. This permits RF experimentation without transmitting.

A practical first target is a simple direct-conversion receiver for one HF amateur band.

## Learn

### RF Basics

- Frequency and wavelength
- Antenna resonance
- Impedance
- Bandwidth

`λ = c/f`

### Oscillators

Learn how transistor LC and crystal oscillators generate RF signals.

### Mixing

A nonlinear mixer produces frequency components including:

`f_out = f_RF ± f_LO`

This permits an RF signal to be translated directly to audio or to an intermediate frequency.

### Filtering

Understand low-pass, high-pass and band-pass filters.

### RF Amplification

Understand why RF layout, grounding, parasitic capacitance/inductance and impedance matter much more than they did in the audio builds.

## Architecture

`Antenna -> band-pass filter -> RF amplifier -> mixer <- local oscillator -> audio filter -> audio amplifier -> speaker/headphones`

## Materials

- Magnet wire
- Toroid cores
- Variable and fixed capacitors
- RF-capable discrete transistors
- Diodes for a simple mixer
- Crystal resonators and/or LC oscillator components
- Potentiometers
- Coaxial cable
- RF connectors
- Wire for a dipole or long-wire receive antenna

## Build

1. Choose one amateur HF band.
2. Build and characterize a resonant input circuit.
3. Build and measure a local oscillator.
4. Build a simple diode/transistor mixer.
5. Inject a known RF signal if suitable test equipment is available.
6. Verify mixer products.
7. Add RF input filtering.
8. Add an RF gain stage if needed.
9. Add an audio low-pass filter.
10. Add discrete audio amplification.
11. Connect headphones or the homemade speaker.
12. Connect an antenna.
13. Tune and receive amateur transmissions.

## Completion Criterion

For every stage, identify:

- Input frequency
- Output frequency
- Expected gain/loss
- Why desired frequencies pass
- Why unwanted frequencies are rejected

---

# Stage 5 — Build a Low-Power Amateur-Radio Transceiver

Begin transmitting only after understanding the receiver and checking the licensing, band and operating requirements applicable to your jurisdiction.

## Learn

### Modulation

Learn the fundamentals of:

- CW
- AM
- SSB
- FM

Use **CW for the first transmitter** because its signal chain can be extremely simple.

### RF Power Amplification

Understand:

- Biasing
- RF power stages
- Harmonics
- Efficiency

### Impedance Matching

Amateur RF systems commonly use approximately 50 Ω interfaces.

Learn:

- Source/load impedance
- Reflection
- Standing-wave ratio
- Simple matching networks

### Harmonic Filtering

Understand why a transmitter requires an output filter before connection to an antenna.

## Architecture

`oscillator -> buffer -> RF power amplifier -> low-pass filter -> matching -> antenna`

## Materials

- Crystal or oscillator components for the chosen amateur band
- RF transistor(s)
- Toroid inductors
- Capacitors
- Key/switch
- 50 Ω low-power dummy load
- Coax cable/connectors
- SWR meter or antenna analyzer
- Low-pass-filter components
- Dipole antenna material

## Build

1. Build the oscillator.
2. Observe its RF output.
3. Add a buffer stage.
4. Add a low-power RF amplifier.
5. Build a 50 Ω dummy load.
6. Test the transmitter into the dummy load only.
7. Build the harmonic low-pass filter.
8. Measure the filtered output and harmonics with appropriate instrumentation.
9. Build a resonant dipole.
10. Measure antenna impedance/SWR.
11. Integrate receiver and transmitter.
12. Add transmit/receive switching.
13. Once appropriately licensed, operate only within permitted amateur frequencies and power limits.

---

# Progressive Radio Milestones

Do not make worldwide communication the first target.

1. Detect a strong local AM broadcast station.
2. Receive an amateur HF station.
3. Receive a distant HF station when propagation permits.
4. Build a low-power CW transmitter and test it into a dummy load.
5. Make a legal local amateur contact.
6. Improve receiver sensitivity and antenna performance.
7. Attempt progressively longer-distance contacts.

---

# Optional Stage 6 — FM Radio

Attempt FM after AM and the simple HF receiver.

Learn:

- Frequency modulation
- Frequency deviation
- Discriminators
- PLL concepts
- VHF construction
- Parasitic capacitance and inductance

Possible architecture:

`antenna -> RF filter/amplifier -> mixer -> IF filter/amplifier -> FM discriminator -> audio amplifier -> speaker`

Expect construction to become substantially more sensitive to physical layout at VHF.

---

# Engineering Method

For every subsystem:

1. Draw the circuit yourself.
2. Predict voltage, current, frequency and waveform at important nodes.
3. Build only that subsystem.
4. Measure it.
5. Compare measurement with prediction.
6. Explain discrepancies.
7. Only then connect the next subsystem.

Do not simply assemble an entire radio schematic and debug it as one unit. The objective is to understand the physical and electrical mechanism of every stage.

---

# Consolidated Materials

## Mechanical / Electromagnetic

- Neodymium magnets
- 28–34 AWG enamelled magnet wire
- Ferrite rods
- Toroid cores
- Card stock
- Thin paper/plastic diaphragm material
- Glue/tape

## Electronics

- Breadboards
- Jumper/hookup wire
- Resistor assortment
- Capacitor assortment
- Variable capacitors
- Inductor assortment
- 2N3904, 2N3906, 2N2222 transistors
- Schottky/germanium detector diodes
- 1N4148 diodes
- Potentiometers
- Crystal resonators
- Switches/buttons
- Battery holders

## RF

- Coaxial cable
- BNC/SMA connectors/adapters
- Antenna wire
- Components for a 50 Ω low-power dummy load
- Optional antenna analyzer/SWR meter

## Test Equipment — Acquisition Priority

1. Digital multimeter
2. Oscilloscope
3. Function generator
4. Adjustable DC power supply
5. RF signal generator
6. Frequency counter
7. Antenna analyzer/SWR meter
8. Small spectrum analyzer such as a TinySA

Do not buy everything on day one. Add instrumentation as the experiments require it.

---

# Final Knowledge Map

At completion, you should understand the causal chain:

`sound`
→ diaphragm motion
→ electromagnetic induction
→ voltage/current
→ transistor amplification
→ oscillation
→ resonance/filtering
→ modulation/demodulation
→ RF amplification
→ impedance matching
→ antenna current
→ electromagnetic radiation

and the reverse:

`electromagnetic radiation`
→ antenna voltage/current
→ filtering/tuning
→ mixing/detection
→ audio amplification
→ coil force
→ diaphragm motion
→ sound

The objective is not merely to own working devices. It is to understand why each device works at the component and physical-system level.


---

# How to Use This Plan

This document is intended to be executable as a syllabus rather than merely a project list.

For each stage:

1. Read only the prerequisite material listed for that stage.
2. Answer the knowledge-gate questions.
3. Perform the prerequisite experiments.
4. Build one subsystem at a time.
5. Write down expected voltage, current, frequency, or waveform before measuring it.
6. Compare prediction against measurement.
7. Integrate the next subsystem only after the current one behaves as expected.

Use a lab notebook with this template:

```text
Question:
Setup:
Prediction:
Measurement:
Difference:
Explanation:
Change made:
Result:
```

The objective is not to memorize electronics theory. It is to repeatedly connect a physical principle to a circuit, a measurement, and finally a working device.

# Core References

## Electronics Fundamentals — Free

**All About Circuits textbook**
https://www.allaboutcircuits.com/textbook/

Use:
- Direct Current for voltage, current, resistance, networks, measurement, magnetism.
- Alternating Current for capacitors, inductors, impedance, resonance and filters.
- Semiconductors for diodes, BJTs and amplifiers.

This is the default reference for basic concepts in this plan.

**MIT OpenCourseWare 6.002 — Circuits and Electronics**
https://ocw.mit.edu/courses/6-002-circuits-and-electronics-spring-2007/

This is a full undergraduate circuits course with lectures, problem sets and exams. Use individual sections when a topic needs more depth; completing the entire course is not a prerequisite.

## Radio Engineering

**ARRL technical/instruction resources**
https://www.arrl.org/instruction-arrl-resources

Useful topics include radio fundamentals, oscillators, mixers, receivers, transmitters, antennas, propagation, measurements and construction.

The **ARRL Handbook for Radio Communications** is an optional comprehensive reference rather than required reading.

## Canadian Amateur-Radio Rules

For operation in Canada, the authority is **Innovation, Science and Economic Development Canada (ISED)**.

Certification path:
https://ised-isde.canada.ca/site/spectrum-management-telecommunications/en/licences-and-certificates/radio-authorizations/amateur-radio-operator-certification/how-become-amateur-radio-operator-overview

Operating standards, amateur bands, bandwidths and required qualifications:
https://ised-isde.canada.ca/site/spectrum-management-telecommunications/en/licences-and-certificates/regulations-reference-rbr/rbr-4-standards-operation-radio-stations-amateur-radio-service

ISED amateur-radio publications:
https://ised-isde.canada.ca/site/amateur-radio-operator-certificate-services/en/publications

Treat ISED as authoritative for transmitting privileges in Canada. ARRL is used here as a technical learning resource.

# Safety Boundaries

- Use low-voltage battery or current-limited bench supplies.
- Do not experiment directly with mains electricity.
- Disconnect power before rewiring.
- Set a conservative current limit before powering a new circuit.
- Check electrolytic capacitor polarity.
- Use eye protection when clipping component leads.
- Treat soldering irons and molten solder as burn hazards.
- Neodymium magnets can pinch fingers and damage magnetically sensitive objects.
- Start RF work with receivers.
- Develop and measure transmitter stages into an appropriate dummy load before considering antenna connection.
- Before transmitting, verify current ISED certification, frequency, bandwidth and operating requirements.

---

# Stage 0 — Detailed Fundamentals

## 0.1 Voltage, Current and Resistance

Read:
https://www.allaboutcircuits.com/textbook/direct-current/

Be able to explain:

- voltage as potential difference between two nodes
- current as charge flow
- resistance
- Ohm's law
- electrical power
- why voltage is measured across two nodes
- why current measurement changes the current path

### Lab 0A — Ohm's Law

Use a low-voltage supply, resistor and multimeter.

Before connecting the circuit:

1. Measure resistance.
2. Measure supply voltage.
3. Calculate expected current with `I = V/R`.
4. Connect the resistor.
5. Measure current.
6. Compare calculation and measurement.

Knowledge gate: if resistance doubles while voltage stays fixed, explain what happens to current and power.

## 0.2 Series/Parallel Networks

Learn voltage division and basic Kirchhoff laws from the same DC textbook.

### Lab 0B — Voltage Divider

Build:

```
VCC --- R1 ---+--- R2 --- GND
              |
            Vout
```

Calculate Vout before measuring it. Change one resistor and repeat.

Knowledge gate: explain why a voltage divider's output can change when a low-resistance load is connected.

## 0.3 Capacitors

Read the capacitor/RC sections:
https://www.allaboutcircuits.com/textbook/alternating-current/

Learn:

- charge storage
- `τ = RC`
- DC blocking / AC coupling
- frequency-dependent impedance
- low-pass and high-pass RC networks

### Lab 0C — RC Response

Apply a step to an RC network.

Predict the time constant, observe capacitor voltage on the oscilloscope, and compare prediction with measurement.

Then feed a sine wave and change frequency. Observe the frequency-dependent response.

## 0.4 Inductors and Magnetism

Use:
https://www.allaboutcircuits.com/textbook/

Study the sections on inductors, magnetic fields, electromagnetism and electromagnetic induction.

Learn:

- current creates magnetic field
- changing magnetic flux can induce voltage
- inductors store energy magnetically
- inductive impedance depends on frequency

These concepts directly become the speaker, microphone and radio tuner.

## 0.5 Diodes

Read:
https://www.allaboutcircuits.com/textbook/semiconductors/

Learn:

- forward/reverse bias
- rectification
- approximate forward-voltage behavior
- why weak-signal detection benefits from a low-threshold detector device

### Lab 0D — Rectification

Feed a low-voltage sine wave through a diode and resistor.

Observe input and output simultaneously.

Then add an RC network after the diode and observe how the waveform changes.

This becomes the conceptual basis for the AM detector.

## 0.6 BJTs and Amplification

Use the semiconductor reference above.

Initially learn only:

- base, collector, emitter
- bias point
- cutoff and saturation
- common-emitter configuration
- small AC signal riding on a DC operating point
- voltage/current gain

### Lab 0E — Transistor Switch

Use a 2N3904 to control an LED.

### Lab 0F — Common-Emitter Amplifier

Build a simple common-emitter amplifier.

Measure:

- DC node voltages
- input AC amplitude
- output AC amplitude
- approximate voltage gain
- phase relationship

Knowledge gate: explain the difference between **bias** and the **signal**.

## 0.7 Oscilloscope Skills

Before Stage 1, be able to:

- set volts/div
- set time/div
- trigger on a repetitive waveform
- use two channels
- measure amplitude
- measure period
- calculate frequency
- understand AC vs DC input coupling

Example knowledge gate:

A 1 kHz waveform has period `T = 1/f = 1 ms`.

---

# Stage 1 — Loudspeaker: Detailed Bring-Up

## Read First

From the core electronics textbook, study:

- magnetic fields
- electromagnetism
- force involving a current-carrying conductor
- AC waveforms

A moving-coil speaker can be mentally decomposed into:

- permanent magnet
- magnetic gap
- voice coil
- diaphragm
- suspension
- frame

Your handmade version only needs to reproduce the essential mechanism.

## Build in Two Steps

### Step A — Prove Mechanical Motion

After winding the coil:

1. Measure its DC resistance.
2. Check continuity.
3. Position it in the magnetic field.
4. Apply a small, current-limited DC stimulus briefly.
5. Observe direction of motion.
6. Reverse polarity.
7. Confirm the direction reverses.

This isolates the electromagnetic mechanism from audio.

### Step B — Produce Sound

Use a function generator initially.

Start with a low-amplitude sine wave in the mid-audio range and increase drive conservatively while watching the coil and diaphragm.

Do not assume a phone or laptop audio jack is suitable for driving an arbitrary handmade coil.

## Troubleshooting

No motion:
- verify continuity
- verify current flow
- check magnet position
- reduce excessive magnetic gap

Motion but weak sound:
- diaphragm may be too heavy or stiff
- mechanical coupling may be poor
- coil may rub
- diaphragm area may be too small

Rattle/distortion:
- asymmetric suspension
- rubbing coil
- loose winding
- excessive excursion

## Experiment

Sweep frequency while keeping the test setup otherwise constant.

Record relative response versus frequency.

The important lesson is that a transducer has a **frequency response**.

Knowledge gate: explain the chain:

`electrical waveform -> coil current -> force -> diaphragm acceleration -> pressure wave`

---

# Stage 2 — Microphone: Detailed Bring-Up

## Read First

Study electromagnetic induction/Faraday's law in:
https://www.allaboutcircuits.com/textbook/

## First Experiment — Reverse the Speaker

Before building another device:

1. Disconnect the Stage 1 speaker from its source.
2. Connect it to the oscilloscope.
3. Move/tap the diaphragm or speak close to it.
4. Look for a generated voltage.

This demonstrates transducer reversibility directly.

## Dedicated Microphone

Compared with the speaker, prioritize:

- lightweight diaphragm
- lightweight moving coil
- low-friction motion
- strong magnetic field

Bring-up order:

`microphone -> oscilloscope`

then

`microphone -> preamp -> oscilloscope`

then

`microphone -> preamp -> audio output stage -> speaker`

Measure at each boundary before adding the next stage.

## Knowledge Gate

Explain why:

- the microphone produces a small electrical signal
- the speaker requires substantially more power
- therefore an amplification chain is needed between them

Final milestone:

`voice -> homemade microphone -> discrete amplifier -> homemade speaker`

---

# Stage 3 — AM Radio: Detailed Curriculum

## 3.1 Resonance Before Radio

Read the resonance sections:
https://www.allaboutcircuits.com/textbook/alternating-current/

Know:

`f_0 = 1/(2π√LC)`

### Lab 3A — Measure LC Resonance

Before attaching an antenna:

1. Build an LC resonant network.
2. Excite it weakly from a function generator.
3. Sweep frequency.
4. Observe the response.
5. Find measured resonance.
6. Calculate theoretical resonance.
7. Explain the discrepancy.

Only after observing resonance on the bench should you use the same principle to select a broadcast station.

## 3.2 Understand AM

Learn to identify:

- carrier
- modulating/audio signal
- envelope

If the function generator supports AM, inspect a known AM waveform on the oscilloscope.

## 3.3 Detector Before Receiver

Build the detector independently:

`known AM signal -> diode -> RC -> oscilloscope`

Verify that the output follows the modulation envelope.

## 3.4 Incremental Receiver Integration

Test in this order:

1. `signal source -> tuner -> scope`
2. `signal source -> tuner -> detector -> scope`
3. `antenna -> tuner -> detector -> scope/high-impedance earpiece`
4. `antenna -> tuner -> detector -> amplifier -> scope`
5. `antenna -> tuner -> detector -> amplifier -> speaker`

## Debugging Strategy

No station:
- confirm the tuner covers the desired frequency range
- verify coil continuity
- verify detector orientation
- verify antenna connection
- locate the last stage where a signal is visible

Several stations simultaneously:
- investigate resonator Q/selectivity
- investigate antenna loading
- verify LC values

Weak audio:
- measure detector output first
- check whether the amplifier loads the detector
- separately verify amplifier gain
- separately verify speaker efficiency

Never debug all stages simultaneously.

Knowledge gate: explain why tuning, detection and amplification are three different operations.

---

# Stage 4 — HF Amateur Receiver: Detailed Curriculum

A **direct-conversion receiver** is recommended as the first HF receiver because it exposes frequency conversion directly.

Conceptual architecture:

```
                         +----------------+
                         | local oscillator|
                         +-------+--------+
                                 |
antenna -> RF filter -> mixer ---+-> audio LPF -> audio amp -> headphones
```

## Read First

ARRL technical resources:
https://www.arrl.org/instruction-arrl-resources

Study the sections/resources relevant to:

- radio fundamentals
- receiver architecture
- oscillators
- mixers
- RF filters
- antennas
- propagation

Continue using the All About Circuits textbook for component-level circuit questions.

## Module A — Oscillator

Build a low-level oscillator as a bench experiment.

Measure:

- frequency
- waveform
- startup behavior
- short-term frequency drift

Knowledge gate: explain the feedback/energy mechanism that sustains oscillation.

## Module B — Mixer

Test frequency conversion with laboratory signals before using an antenna.

Example reasoning exercise:

- input RF: 7.001 MHz
- local oscillator: 7.000 MHz
- difference product: 1 kHz

The important result is observing that nonlinear mixing can translate an RF frequency difference into the audio range.

## Module C — Audio Filter

Build and measure a low-pass filter.

Plot or tabulate response at several frequencies.

## Module D — Audio Amplifier

Reuse concepts from the microphone stage. Verify it independently.

## Module E — RF Input Filter

Build a tuned/band-pass input network and characterize it with low-level signals before attaching the antenna.

## Module F — Receive Antenna

Start simple. A wire receive antenna is enough for initial experiments.

Then learn the relationship:

`λ = c/f`

and build a resonant dipole as a separate antenna experiment.

## Integration

Combine modules in this order:

1. oscillator + mixer
2. audio filter
3. audio amplifier
4. RF input filter
5. antenna

Probe the interface between every pair of blocks.

## Next Architecture

After the direct-conversion receiver works, study the superheterodyne receiver:

`RF -> mixer -> fixed IF -> IF filter/amplifier -> detector -> audio`

Do not build this first. Its advantages are easier to understand after personally observing direct conversion.

---

# Stage 5 — Amateur Transmitter: Learning and Validation Plan

## Regulatory Gate

Before over-the-air operation, use the current ISED certification process:
https://ised-isde.canada.ca/site/spectrum-management-telecommunications/en/licences-and-certificates/radio-authorizations/amateur-radio-operator-certification/how-become-amateur-radio-operator-overview

Verify current operating requirements in RBR-4:
https://ised-isde.canada.ca/site/spectrum-management-telecommunications/en/licences-and-certificates/regulations-reference-rbr/rbr-4-standards-operation-radio-stations-amateur-radio-service

Do not rely on a static summary in this repository for current operating privileges.

## Learn the Blocks

For a first transmitter, study CW because the conceptual chain is comparatively small:

`oscillator -> buffer -> RF output stage -> harmonic filter -> impedance interface -> load/antenna`

Use ARRL technical references for:

- oscillators
- RF amplification
- transmitter architectures
- harmonics
- output filtering
- transmission lines
- impedance matching
- SWR
- antennas
- RF safety

## Development Sequence

Treat every block as a separate laboratory project.

1. Characterize the oscillator at low level.
2. Study why buffering isolates an oscillator from load changes.
3. Characterize the RF output stage into a suitable 50 Ω dummy load.
4. Characterize the output filter independently.
5. Measure the integrated chain into the dummy load.
6. Inspect frequency and unwanted spectral components with suitable instrumentation.
7. Build and measure the antenna as a separate project.
8. Verify current ISED privileges and requirements.
9. Only then consider over-the-air operation.

The engineering objective is to be able to account for the signal's frequency, approximate power, load, filtering and spectral cleanliness before an antenna is connected.

## Antenna Reference

ARRL antenna resources:
https://www.arrl.org/instruction-arrl-resources

Optional deep reference: **The ARRL Antenna Book**.

Study:

- wavelength
- dipoles
- feed points
- coaxial transmission lines
- characteristic impedance
- reflections
- SWR
- matching
- radiation pattern

Use a simple dipole as the first antenna architecture rather than optimizing for compactness or gain.

---

# Stage 6 — FM Extension

FM comes last because VHF construction introduces an important principle: **physical geometry becomes part of the circuit**.

At higher frequency:

- wire length matters
- component leads contribute inductance
- nearby conductors contribute capacitance
- breadboards introduce parasitics
- grounding geometry matters
- unintended coupling becomes important

Before integrating an FM receiver, separately study and measure:

1. VHF resonance
2. VHF oscillator behavior
3. layout sensitivity
4. frequency conversion
5. FM detection/discrimination

Then integrate the receiver one block at a time.

---

# Instrumentation Learning Path

## Digital Multimeter — Stage 0

Know how to measure:

- DC voltage
- resistance
- continuity
- DC current

## Oscilloscope — Stage 0/1

Know how to measure:

- waveform vs time
- amplitude
- period/frequency
- DC offset
- phase relationship between two signals

## Function Generator — Stage 0/1

Use it to replace an unknown real-world source with a known signal.

Examples:

- known audio into speaker
- known small signal into amplifier
- frequency sweep into filters
- known signal into detector experiments

## RF Signal Generator — Stage 3/4

Useful for testing radio stages independently of actual stations and propagation.

## Spectrum Analyzer — Stage 4/5

Understand the distinction:

- oscilloscope: signal versus **time**
- spectrum analyzer: signal versus **frequency**

This becomes important for oscillators, mixers and transmitter validation.

## Antenna Analyzer / VNA — Stage 5

Use it to make RF impedance visible.

Learn:

- impedance versus frequency
- resonance
- SWR
- basic reflection/S-parameter intuition

---

# What Not to Use Initially

To preserve the learning objective, do not make these the core of the first implementation:

- Bluetooth audio modules
- integrated audio amplifier boards
- complete AM/FM receiver ICs
- SDR as the receiver itself
- PLL synthesizer modules
- integrated radio/transceiver modules

They can be introduced later for comparison.

Sophisticated **test equipment is fine**. The restriction is on hiding the mechanism of the device being learned, not on measurement tools.

---

# Four-Day Intensive Path

The target is **four full build days**, not twelve weeks. This requires aggressive just-in-time learning: do not read entire textbooks or courses. Read only the linked section needed to understand the experiment immediately in front of you.

Assume approximately **8–12 focused hours per day** and obtain all parts/test equipment before Day 1.

The four-day objective is:

`fundamentals -> speaker -> microphone -> amplifier -> AM receiver -> HF receiver`

The low-power amateur transmitter remains the next project after the four-day sprint unless the receiver work finishes early and the measurement/regulatory prerequisites are already satisfied.

## Before Day 1 — Preparation Only

Do this before the clock starts:

- acquire the consolidated BOM
- acquire multimeter, oscilloscope and function generator
- obtain breadboards, soldering tools and hookup wire
- organize resistors/capacitors/transistors by value/type
- obtain magnets, magnet wire, ferrite rod, variable capacitor and antenna wire
- bookmark the references in this document
- verify test equipment powers on and probes/leads work

Do not spend Day 1 shopping or configuring equipment.

## Day 1 — Learn Electronics by Building a Speaker

### Morning — 3–4 h

Learn only:

- voltage/current/resistance
- Ohm's law
- series/parallel circuits
- voltage dividers
- AC versus DC
- frequency/amplitude/period
- capacitor intuition
- inductor/magnetic-field intuition
- diode intuition
- basic BJT operation
- multimeter and oscilloscope operation

Execute Labs 0A–0F rapidly.

Do not pursue mathematical circuit-analysis depth beyond what the experiments require.

### Afternoon — 3–4 h

Build the Stage 1 loudspeaker.

Required sequence:

1. wind coil
2. measure coil resistance
3. place coil in magnetic field
4. verify polarity-dependent motion
5. attach diaphragm
6. drive with function generator
7. produce audible tone
8. sweep frequency

### Evening — 1–2 h

Review the measurements and explain from memory:

`voltage -> current -> magnetic field/force -> diaphragm -> sound`

**Day 1 exit criterion:** homemade speaker produces a recognizable tone and you can explain why.

---

## Day 2 — Reverse the Physics: Microphone + Amplifier

### Morning — 2 h

Learn only:

- Faraday's law qualitatively
- electromagnetic induction
- transistor bias
- common-emitter amplification
- coupling capacitors

First use the Day 1 speaker as a microphone and observe its generated waveform.

### Midday — 3–4 h

Build the dedicated dynamic microphone.

Measure the raw microphone output before adding electronics.

### Afternoon — 2–3 h

Build/debug the discrete microphone preamplifier and audio output stage.

Bring up in this order:

`microphone -> scope`

`microphone -> preamp -> scope`

`microphone -> preamp -> output amp -> scope`

`microphone -> preamp -> output amp -> homemade speaker`

### Evening — 1 h

Trace one spoken sound through every energy conversion.

**Day 2 exit criterion:**

`voice -> homemade microphone -> discrete electronics -> homemade speaker`

works well enough to recognize the input sound.

---

## Day 3 — Build the AM Radio

### Morning — 2–3 h

Learn only:

- capacitor/inductor AC behavior
- LC resonance
- resonant frequency
- Q/selectivity intuition
- amplitude modulation
- diode rectification
- RC envelope detection

### Lab — 1–2 h

Before attempting reception:

1. build LC resonator
2. predict resonance
3. sweep it with the function generator
4. measure resonance
5. build diode + RC detector
6. observe rectification/envelope behavior

### Afternoon/Evening — 4–6 h

Build the AM receiver incrementally:

`LC tuner -> detector -> audio amplifier -> speaker`

Test each stage before connecting the next.

Then attach the antenna and tune for a strong broadcast station.

Do not optimize sensitivity or audio quality yet.

**Day 3 exit criterion:** receive at least one broadcast station and explain tuning, detection and amplification as separate operations.

---

## Day 4 — From Radio to Amateur HF Receiver

### Morning — 2–3 h

Learn only:

- wavelength/frequency
- RF filters
- oscillation
- local oscillators
- nonlinear mixing
- sum/difference frequencies
- direct-conversion receiver architecture
- basic antenna resonance
- HF propagation intuition

### Midday — 2–3 h

Build/test modules separately:

1. local oscillator
2. mixer
3. audio low-pass filter
4. RF input filter

Use known laboratory signals wherever possible rather than debugging against unknown over-the-air conditions.

The key experiment is to demonstrate frequency conversion:

`RF + LO -> audible difference frequency`

### Afternoon/Evening — 4–6 h

Integrate:

`antenna -> RF filter -> mixer + LO -> audio filter -> amplifier -> headphones/speaker`

Attempt to receive an HF amateur signal.

If reception fails, the Day 4 fallback completion criterion is a fully bench-validated receive chain where oscillator, mixer, filtering and audio stages have each been independently demonstrated.

### Final Review — 1 h

From a blank page, draw and explain:

- speaker
- microphone
- AM receiver
- direct-conversion HF receiver

For every block state:

- physical principle
- input
- output
- expected frequency
- expected signal magnitude/gain behavior
- measurement used to verify it

**Day 4 primary exit criterion:** receive an amateur HF signal with the homemade receiver.

**Day 4 minimum exit criterion:** all receiver subsystems work independently and frequency conversion has been experimentally demonstrated.

---

# After the Four Days — First Transmitter

Stage 5 follows immediately after the sprint.

Do not squeeze transmitter construction into Day 4 at the expense of understanding the receiver. The transmitter introduces additional requirements—output power, harmonics, filtering, impedance matching, antenna loading, spectral measurement and regulatory compliance—that deserve their own measured bring-up.

At the end of Day 4 you should already understand most of the conceptual blocks needed to begin it.

# Four-Day Scope Discipline

To make this schedule realistic:

- **Do not** complete entire courses.
- **Do not** optimize aesthetics.
- **Do not** design PCBs.
- **Do not** chase high audio fidelity.
- **Do not** optimize receiver sensitivity.
- **Do not** build multiple alternative circuits.
- **Do not** spend hours deriving equations already covered by a reference.
- **Do** predict before measuring.
- **Do** use the oscilloscope constantly.
- **Do** validate every block independently.
- **Do** move forward once the physical principle has been demonstrated.

The four-day goal is not mastery of electronics or RF engineering. It is a working first-principles mental model backed by physical experiments and functioning prototypes.

# Definition of Done

At the end, answer these from first principles:

1. Why does current through a speaker coil produce motion?
2. Why does moving a microphone coil produce voltage?
3. Why does an LC circuit select a frequency range?
4. Why can a diode recover audio information from AM?
5. Why does an analog amplifier need a bias point?
6. Why does a mixer translate signals between frequencies?
7. What sustains an oscillator?
8. How does antenna size relate to wavelength?
9. Why does antenna/load impedance matter at RF?
10. Why are transmitter harmonics filtered?
11. Why can HF propagation permit communication far beyond line of sight?
12. Why does physical layout increasingly matter as frequency rises?

If an answer reduces to “because that block does it,” return to that experiment. The goal is a physical and circuit-level explanation.
