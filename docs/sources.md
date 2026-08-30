# Sources — Four-Channel 4–20 mA I/O Module

The evidence this board's design will have to cite. **Classes of document, not
documents:** the specific parts are not chosen yet, so naming a datasheet here
would be choosing one.

A number that reaches the board carries its provenance: source, document id or
URL, retrieval date, units, and the condition it applies under. A number without
that is not evidence, and no live network lookup may change a validation or
release result.

| Kind of source | What the design needs from it |
|---|---|
| Isolation component datasheets (barrier-crossing devices) | Establish the actual working and withstand voltage, package creepage/clearance, transient immunity and channel count that the isolation claim rests on. |
| Creepage and clearance / safety-spacing guidance for the chosen working voltage and pollution degree | The brief demands explicit creepage/clearance; the numbers must be derived from a citable spacing rule, not chosen by eye. |
| Isolated power-transfer component datasheets | Needed if field-side rails are generated across the barrier — sets available power, isolation rating and emissions behaviour. |
| Precision converter datasheets (ADC and/or DAC) | Supply offset, gain, INL/DNL and drift figures that populate the input and output error budgets. |
| Current-loop driver / voltage-to-current stage datasheets | Compliance-voltage-versus-supply data is the only way to substantiate the 500 ohm load claim rather than assert it. |
| Voltage reference datasheet | Initial accuracy and temperature coefficient dominate absolute accuracy for both the sense and drive paths. |
| Sense resistor datasheet | Tolerance, temperature coefficient, power rating and self-heating feed directly into input accuracy and fault survivability. |
| Protection device datasheets (transient, overcurrent and clamping classes) | Standoff voltage, clamping level, energy handling and leakage determine both fault coverage and the accuracy penalty at the connector edge. |
| 24 V industrial cabinet environment references — expected miswiring, transients and surge conditions | The brief's "common wiring faults expected in a 24 V cabinet" needs an external definition before protection can be sized to it. |
| Controller / MCU datasheet, if a controller is used | Peripheral availability, pin count, and package thermal data for the housekeeping, host link and calibration functions. |
| Non-volatile memory datasheet for calibration storage | Endurance, retention and write behaviour bound how and how often calibration data can be stored. |
| PCB fabricator capability page for the chosen layer count | Minimum trace/space, drill, annular ring and stackup options must permit both the barrier spacing and the fine-pitch precision parts. |

## Recording a source, once one is chosen

Replace the class with the actual document — manufacturer, part number, revision
and date — and state the fact taken from it, in the units the document uses.
Keep the class row: it says why the document was needed.

JLCPCB-wide process limits are **not** recorded here. They live in the toolkit's
`profiles/jlcpcb/`, with their own provenance; this board records only its own
tighter targets and its own selected options. A limit copied into two places is
a rival threshold, and the toolkit has a gate that says so.
