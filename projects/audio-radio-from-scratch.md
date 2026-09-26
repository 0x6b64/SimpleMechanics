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
