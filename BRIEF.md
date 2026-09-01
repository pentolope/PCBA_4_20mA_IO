# PCBA_4_20mA_IO — Four-Channel 4–20 mA I/O Module
## Design brief

Design a 24 V industrial module with two 4–20 mA inputs and two 4–20 mA outputs. The logic/host side shall be galvanically isolated from field wiring. Inputs should tolerate common wiring faults expected in a 24 V cabinet; outputs should support at least 500 ohm loop load at nominal supply when practical. Provide calibration storage, status LEDs, and an isolated UART or USB host interface. Keep field protection at the connector edge, maintain the isolation barrier with explicit creepage/clearance, and route precision sense nodes as Kelvin connections where applicable.

## Functional requirements

- All four channels shall run simultaneously and continuously, independent of host polling.
- A per-channel error budget shall be declared: reference, gain, offset, drift, noise, and what calibration removes.
- The host shall read per-channel measured current, commanded current and fault status; LEDs shall show at least power and fault.

## Current input channels

- Each input shall cover 4–20 mA with documented margin to distinguish under-range, over-range and open loop.
- The current-sense element shall be a four-terminal Kelvin connection carrying no loop current in either sense conductor.
- Sense tolerance, tempco, self-heating, protection leakage and noise shall fit the budget; burden voltage shall be documented.

## Current output channels

- Each output shall drive 4–20 mA into 0 Ω up to at least 500 Ω at nominal supply — 10 V compliance at 20 mA — or document the load reached.
- Output current shall stay within budget across the rated load range, be monotonic, and settle within a documented time.
- Outputs shall reach a defined state on power-up, reset and loss of host communication, and survive a short to either field rail.

## Isolation barrier and power

- One continuous barrier shall separate all field terminals and their protection from the logic/host side; each side's powering shall be documented.
- Only parts rated at or above the declared working and isolation voltage shall cross it — no trace, plane, pour, test net, mount or thermal path.
- Minimum creepage and clearance shall be one documented figure held everywhere, with working voltage, pollution degree and material group stated.
- The isolated supply shall hold regulation with all channels at worst case at the bottom of the declared 24 V band; the returns shall never be joined.

## Field protection, layout and grounding

- Every field terminal shall survive, continuously and in either polarity, any voltage between the cabinet supply rails, channel miswiring and reverse supply polarity, without harming other channels.
- Protection shall sit at the connector edge, its fault current clear of sense and reference returns; the claimed transient immunity level shall be declared.
- Kelvin pairs shall route together clear of switching nodes; analog, digital and LED returns shall not share copper.

## Calibration and test access

- Per-channel coefficients shall be stored non-volatile on the module, survive power cycling and firmware update, and be host-writable.
- Stored data shall be integrity-checked and versioned; on failure the module shall use documented defaults, keep running and report it.
- Test points shall reach both rails, each output and each sense node without loading the Kelvin connection.
- The barrier shall pass a production isolation test at the declared voltage, with any bypassed part identified.

## Open choices

- Isolated UART or isolated USB, and whether the host side is bus-powered.
- Converters field-side behind digital isolation or logic-side behind analog isolation; per channel or shared.
- Whether inputs power two-wire transmitters or expect externally powered sources, and whether outputs source or sink.
- Barrier rating, pollution degree and material group; outline, mounting, terminal pitch and layer count.
