# Architecture — Four-Channel 4–20 mA I/O Module

**A worksheet, not a design.** Every line below is a question this board has to
answer, and none of them is answered here. Nothing in this file is a
recommendation, and the order of the sections carries no preference.

The questions were derived from [the brief](../BRIEF.md) and from what this
board is meant to stress in the benchmark:

- precision current loop
- 24V domains
- protection
- isolation

Those are the places where a wrong answer shows up in copper.

Answer them in this file as the design is made, each answer carrying the
evidence that supports it, and record the corresponding choice against its
`OPEN-nn` entry in [board/requirements.md](../board/requirements.md). An answer
without evidence is a guess wearing a document's clothes — and this benchmark is
allowed to refuse an unsupported claim rather than invent one.

## Isolation barrier definition

- Where exactly does the barrier run across the board, and which nets are permitted on each side?
- What working voltage and withstand rating is the barrier designed to, and what evidence sets that number?
- What creepage and clearance distances result, and how are they measured and shown on the layout?
- How many signals must cross the barrier, in which directions, and what carries them?
- Does anything else bridge the gap — a plane, a mounting hole, a silkscreen fill, a thermal relief, a test point?
- Is the barrier maintained through the finished assembly (mask, coating, connector bodies), not just in copper?

## Field-side power and the 24 V domain

- What supply input range around nominal is accepted, and what happens outside it?
- How is field-side power derived, and does it cross the isolation barrier or arrive separately?
- What rails exist on each side of the barrier, and what is each one's load?
- How is supply miswiring or reverse polarity handled without defeating the isolation?
- What is the total worst-case current draw with all four channels active?

## 4–20 mA input channel chain

- How is loop current converted to a measurable quantity, and at what sense value?
- Is sensing single-ended or differential, and against which field-side reference?
- Which converter handles the inputs, at what resolution, and is conversion per-channel or multiplexed?
- How is the 4 mA to 20 mA span mapped to the converter's usable range, and how much headroom is reserved for over-range and fault conditions?
- What limits input current during a fault so the protection, not the sense element, absorbs the event?
- How do the two input channels relate to each other — shared reference, or independent?

## 4–20 mA output loop drivers

- What topology generates the loop current, and does the module source the loop or ride an external supply?
- What is the compliance voltage at 20 mA, and does it actually clear 500 ohms at nominal supply?
- If 500 ohms is not achievable, what is the real limit and what makes the shortfall the practical outcome the brief allows?
- What happens to the loop on power-up, brown-out, reset, and host-link loss?
- Is the output protected against a shorted or open loop, and against back-feed from field wiring?
- How much power does each driver dissipate at worst case, and where does that heat go?

## Field protection at the connector edge

- Which specific fault scenarios does the protection cover — miswiring to the 24 V rail, reversed polarity, cross-channel shorts, surge, ESD, induced transients?
- What protection element classes are used, and in what order from the connector inward?
- Which protection elements sit physically at the connector edge, as the brief requires, and does any of them end up further inboard — and if so, why?
- Where does fault energy return to, and does that return path stay on the field side of the barrier?
- How much series impedance does the protection add, and what does that cost in measurement accuracy or compliance voltage?
- How is the protection verified rather than asserted?

## Precision, calibration and error budget

- What is the target end-to-end accuracy for inputs and for outputs, and what justifies that target?
- What is the contribution of each error source — reference, sense element, converter offset and gain, drift over temperature, self-heating?
- Which errors are removed by calibration and which remain after it?
- What is stored in calibration storage, in what format, and when is it written?
- What endurance and retention does the calibration store need over the product's life?
- How is calibration performed in production, and what does that require of the board?

## Kelvin sensing and precision layout

- Which nodes qualify as precision sense nodes requiring Kelvin connections?
- For each, where do the force and sense connections physically separate, and does the layout actually implement that?
- How much IR drop would a non-Kelvin connection introduce, and does that exceed the error budget?
- How are sense traces shielded or referenced to avoid picking up switching or loop-driver currents?
- Does the reference distribution reach each precision node without sharing a high-current return?

## Host interface and digital housekeeping

- Is the host interface UART or USB, and what decides it?
- Is the interface's power and ground return isolated too, or only its signals?
- Is there a controller on board; if so, what peripherals and pin count does the full channel set demand?
- What does the host protocol need to expose — readings, output setpoints, calibration, status, faults?
- How is firmware loaded and updated, and does that path cross the barrier?

## Status indication and diagnostics

- How many LEDs, and what does each one mean?
- Which faults are detectable in hardware, and which are only inferable in firmware?
- Are LEDs on the logic side, the field side, or both, and does their placement respect the barrier?
- Can a technician distinguish a field wiring fault from a module fault from the LEDs alone?

## Stackup, grounding and layout planning

- What is the layer assignment across the chosen layer count, and how do the isolated domains occupy them?
- How are the field-side and logic-side reference planes split, and does any plane cross the barrier on an inner layer?
- Where are the analog, digital and any switching returns kept separate, and where do they meet?
- Are there any controlled-impedance requirements, and if not, why not?
- Does the chosen fabricator's capability set support the stackup, spacings and drill sizes used?

## Mechanical, connectors and manufacturability

- What is the board outline and size, and what drives it — connector pitch, barrier width, mounting, or an enclosure?
- What field and host connectors are used, and what wiring do they accept?
- How does the connector arrangement keep field wiring physically away from the logic side?
- Are all parts placeable and assemblable in one process, and does anything need hand work?
- Does the barrier region stay free of assembly features that would compromise spacing?

## Test, bring-up and verification

- What test points are needed to verify each channel, and are any on the barrier's wrong side?
- How is the isolation barrier verified after assembly?
- How is loop compliance measured against the 500 ohm target?
- What bench setup proves input fault tolerance without destroying the board?
- What measurements must exist before any accuracy claim is written down?

## Answers still owed

All of them. See [status.md](status.md).
