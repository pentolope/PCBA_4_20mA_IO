# Benchmark entry — board 11 of 32

[metadata.json](metadata.json) is the supplied catalogue entry for this board,
preserved byte for byte from the seed pack. It is the same record that appears
in `boards_index.json` in
[PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench), and the two must agree.

| | |
|---|---|
| Repository | `PCBA_4_20mA_IO` |
| Board id | `current_loop_io` |
| Category | industrial-analog |
| Difficulty | 3 / 5 |
| Brief detail | 4 / 5 |
| Likely layer count | 4 |
| Primary stressors | precision current loop, 24V domains, protection, isolation |

`difficulty` is how hard the board is. `detail` is how much of it the brief
states — and a low `detail` is not a low bar. A detail-1 brief leaves the
architecture open on purpose, and an agent that fills the silence with invented
user requirements has failed the board more thoroughly than one that designs it
badly.

At difficulty 3/5 with brief detail 4/5, this board tests whether a design agent can honour a genuinely specific analog brief without either dropping stated constraints or inflating them into invented ones. Its stressors — precision current loop, 24V domains, protection and isolation — collide in layout as much as in schematic: the isolation barrier, the connector-edge protection and the Kelvin sense routing are all placement requirements that a plausible-looking schematic can silently violate. The interesting failure mode here is a design that reads correct on paper but cannot substantiate its isolation spacing, its loop compliance headroom, or its accuracy claims.

## What goes here

Compact results only: metrics, verdicts, and the commit each was measured at.
The evidence for a result is the artefact the toolkit recomputes, not a summary
of it.

Routing search output, candidate pools, build trees and field-solver dumps do
**not** go here. They are ignored by [.gitignore](../.gitignore) and are
regenerated from what is committed. Thirty-two repositories share one benchmark
clone; weight here is paid thirty-two times.

## Protocol

The attempt protocol is defined once, in the umbrella repository, so that
thirty-two boards cannot drift into thirty-two protocols. See
[PCBA_AutoDesignAndTest_Bench/BENCHMARK.md](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench/blob/main/BENCHMARK.md).
