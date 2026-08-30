# PCBA_4_20mA_IO — Four-Channel 4–20 mA I/O Module

**Benchmark ID:** 11  
**Difficulty:** 3/5  
**Brief detail:** 4/5  
**Category:** industrial-analog  
**Likely layer count:** 4  
**Primary stressors:** precision current loop, 24V domains, protection, isolation

## Design brief

Design a 24 V industrial module with two 4–20 mA inputs and two 4–20 mA outputs. The logic/host side shall be galvanically isolated from field wiring. Inputs should tolerate common wiring faults expected in a 24 V cabinet; outputs should support at least 500 ohm loop load at nominal supply when practical. Provide calibration storage, status LEDs, and an isolated UART or USB host interface. Keep field protection at the connector edge, maintain the isolation barrier with explicit creepage/clearance, and route precision sense nodes as Kelvin connections where applicable.

## Benchmark intent

This brief is intentionally one member of a heterogeneous PCBA-autodesign benchmark. Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements. The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.
