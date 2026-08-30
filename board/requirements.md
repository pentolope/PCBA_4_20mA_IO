# Requirements — Four-Channel 4–20 mA I/O Module

Two lists. The difference between them is the whole point of this file.

A **fixed requirement** is something [BRIEF.md](../BRIEF.md) asks for. Each one
below quotes the brief text that substantiates it; if a statement cannot be
quoted, it is not a requirement here. An **open decision** is a choice the brief
deliberately left to whoever designs this board.

> Missing details are design freedom, not permission to fabricate unstated user
> requirements.

Promoting a decision into a requirement is the failure this file exists to
prevent. Record a choice under the decision it answers, with the reasoning that
made it — never by adding it to the list above.

Bound to `BRIEF.md` SHA-256 `7cf59b5f7204d3e280be2c89489fa2832001794b673967f96952d0f0d6f8157f`.

## Fixed by the brief

### REQ-01 — Provide exactly two 4–20 mA inputs and two 4–20 mA outputs.

Brief text:

> two 4–20 mA inputs and two 4–20 mA outputs

### REQ-02 — The module is a 24 V industrial module.

Brief text:

> Design a 24 V industrial module

### REQ-03 — The logic/host side must be galvanically isolated from field wiring.

Brief text:

> The logic/host side shall be galvanically isolated from field wiring.

### REQ-04 — Inputs should tolerate common wiring faults expected in a 24 V cabinet.

Brief text:

> Inputs should tolerate common wiring faults expected in a 24 V cabinet

### REQ-05 — Outputs should support at least a 500 ohm loop load at nominal supply, when practical.

Brief text:

> outputs should support at least 500 ohm loop load at nominal supply when practical.

### REQ-06 — Provide on-board calibration storage.

Brief text:

> Provide calibration storage, status LEDs

### REQ-07 — Provide status LEDs.

Brief text:

> Provide calibration storage, status LEDs

### REQ-08 — Provide an isolated host interface — either UART or USB.

Brief text:

> an isolated UART or USB host interface

### REQ-09 — Field protection must be placed at the connector edge.

Brief text:

> Keep field protection at the connector edge

### REQ-10 — Maintain the isolation barrier with explicit creepage/clearance — the spacing is to be explicit rather than left implied; the brief states no distances.

Brief text:

> maintain the isolation barrier with explicit creepage/clearance

### REQ-11 — Precision sense nodes must be routed as Kelvin connections where applicable.

Brief text:

> route precision sense nodes as Kelvin connections where applicable.

### REQ-12 — Stated brief requirements are authoritative; choices the brief leaves open must be made and documented as engineering decisions rather than back-filled as hidden user requirements.

Brief text:

> Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements.

### REQ-13 — This repository stays a consumer of the shared PCBA_AutoDesignAndTest toolkit; board-specific logic must not be pushed into the toolkit.

Brief text:

> The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.

## Open — the design agent decides

### OPEN-01 — Whether the isolated host interface is UART or USB.

The brief explicitly offers both as alternatives ("an isolated UART or USB host interface") and does not pick one.

*Decision:* **not yet made.**

### OPEN-02 — How signals cross the isolation barrier — the isolation technology, the number of crossing channels, and their direction.

The brief requires galvanic isolation but names no technology, part, or channel budget.

*Decision:* **not yet made.**

### OPEN-03 — How the field side is powered across the barrier, and whether field power is derived on-board or supplied externally.

The brief states isolation but is silent on isolated power transfer; it says nothing about where field-side rails come from.

*Decision:* **not yet made.**

### OPEN-04 — The isolation working/withstand voltage the barrier is designed to, and the specific creepage and clearance dimensions that follow from it.

The brief requires the spacing be "explicit" but states no voltage rating, pollution degree, or millimetre figure to derive it from.

*Decision:* **not yet made.**

### OPEN-05 — Whether a microcontroller or other digital controller is present, and which one.

Calibration storage and a host interface imply digital housekeeping, but the brief never names or requires a controller, let alone a specific device.

*Decision:* **not yet made.**

### OPEN-06 — The input signal chain architecture — sense-resistor value, single-ended vs differential sensing, converter type and resolution, per-channel vs multiplexed conversion.

The brief specifies only that the inputs are 4–20 mA and that precision sense nodes get Kelvin routing; the chain itself is unspecified.

*Decision:* **not yet made.**

### OPEN-07 — The output driver architecture — DAC plus voltage-to-current stage, an integrated loop driver, sourcing vs sinking, and whether loops are module-powered or externally powered.

The brief fixes only the 500 ohm load target at nominal supply; it names no topology or part.

*Decision:* **not yet made.**

### OPEN-08 — The calibration storage medium, capacity, and the stored data format / calibration procedure.

The brief says "Provide calibration storage" and stops there — no technology, size, or scheme.

*Decision:* **not yet made.**

### OPEN-09 — The accuracy, resolution, linearity, drift and temperature-coefficient targets, and the error budget that justifies them.

The brief calls the sense nodes "precision" but states no numeric accuracy requirement anywhere.

*Decision:* **not yet made.**

### OPEN-10 — Which specific faults count as "common wiring faults expected in a 24 V cabinet", and the protection strategy and component classes that cover them.

The brief names the fault class in words only — no fault list, no voltage/energy levels, no protection scheme.

*Decision:* **not yet made.**

### OPEN-11 — Field and host connector selection — type, pin count, pitch, wire gauge, pluggable vs fixed, and pinout.

The brief locates protection at the connector edge but never says what the connectors are.

*Decision:* **not yet made.**

### OPEN-12 — Board outline, dimensions, and mechanical mounting or enclosure/rail fit.

The brief gives no mechanical envelope, mounting scheme, or dimensional constraint at all.

*Decision:* **not yet made.**

### OPEN-13 — Stackup detail beyond the likely layer count — layer assignment, copper weights, dielectric choice, and whether any controlled impedance is needed.

Only a likely layer count of 4 comes from metadata; the brief says nothing about stackup or impedance.

*Decision:* **not yet made.**

### OPEN-14 — Status LED count, colours, placement, and what each one indicates.

The brief requires "status LEDs" in the plural and specifies nothing further.

*Decision:* **not yet made.**

### OPEN-15 — Field-side reference topology — whether all four channels share one field ground domain, or channels are isolated from each other.

The brief isolates logic from field wiring but is silent on channel-to-channel relationships within the field side.

*Decision:* **not yet made.**

### OPEN-16 — Supply input handling — accepted input range around nominal, reverse-polarity and miswiring protection on the supply, and how on-board rails are generated.

The brief names the 24 V context but gives no supply tolerance window, no polarity requirement, and no rail list.

*Decision:* **not yet made.**

### OPEN-17 — Worst-case power dissipation budget and the thermal approach, particularly for the output loop drivers.

The brief is silent on thermal limits, ambient temperature, and enclosure conditions.

*Decision:* **not yet made.**

### OPEN-18 — Test, bring-up, calibration and programming access — test points, headers, and any self-test provisions.

The brief mentions calibration storage but describes no calibration or test access mechanism.

*Decision:* **not yet made.**

### OPEN-19 — Environmental operating range and any standards, certification or EMC targets the module is designed against.

The brief is simply silent on environment, standards and compliance.

*Decision:* **not yet made.**

## Where a decision gets recorded

1. Answer it under its `OPEN-nn` heading above, with the reasoning and the
   evidence that made the choice.
2. Set `chosen` and `rationale` on the matching entry in
   [requirements.json](requirements.json).
3. Cite the datasheet or standard in [docs/sources.md](../docs/sources.md).

A choice recorded this way stays visibly a choice. That is what lets a later
reader tell this board's engineering apart from its brief.

## Where this board is most likely to be faked

Places where a design run would be tempted to assert something it cannot
substantiate:

- Stating an isolation rating without citing the barrier component's working voltage and without a measured creepage/clearance figure taken from the actual layout — the brief specifically requires the spacing be explicit.
- Claiming the 500 ohm load target is met without a compliance-voltage calculation from the chosen driver's headroom at nominal supply. The brief's "when practical" is an invitation to justify a shortfall, not a licence to skip the arithmetic.
- Inventing a precision figure ("0.1% FS", "16-bit accurate") that appears nowhere in the brief, instead of assembling an error budget from cited reference, converter and sense-resistor specifications.
- Compressing "common wiring faults expected in a 24 V cabinet" into a single unspecified protection part without ever enumerating which faults are covered, at what level, and what is not covered.
- Drawing Kelvin connections in the schematic and then not implementing them in copper — force and sense must physically separate at the sense element for the claim to hold.
- Letting something quietly bridge the barrier: an inner-layer plane, a mounting hole, a thermal relief, a test point, a connector body, or the host interface's ground return when only its signals were isolated.
- Choosing UART or USB and then treating the choice as free, when the interface's isolation, power delivery and cable environment differ substantially between them.
- Drifting board-specific logic into the shared PCBA_AutoDesignAndTest toolkit, which the benchmark-intent section rules out — the repository is to remain a consumer of that toolkit.
