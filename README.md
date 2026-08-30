# Four-Channel 4–20 mA I/O Module

A 24 V industrial module with two 4–20 mA inputs and two 4–20 mA outputs, galvanically isolating the logic/host side from field wiring.

This repository holds the design problem for `PCBA_4_20mA_IO`, a four-channel industrial current-loop I/O module. The brief fixes the channel mix (two 4–20 mA inputs, two 4–20 mA outputs), the 24 V industrial context, and a galvanic isolation boundary between the logic/host side and field wiring. It also imposes several concrete constraints on top of that: inputs should tolerate common 24 V cabinet wiring faults, outputs should drive at least a 500 ohm loop load at nominal supply where practical, and the board must carry calibration storage, status LEDs and an isolated UART or USB host interface — with field protection placed at the connector edge, explicit creepage/clearance across the barrier, and Kelvin connections on precision sense nodes. What the brief does **not** fix is every part, topology and dimension: no converter architecture, no isolation technology, no isolation voltage rating, no accuracy target, no connector, no board outline. Those are recorded below as open decisions for the design agent to make and justify, not to inherit.

> **This board has not been designed.** There is no schematic, no layout and no
> part selection here — only the brief, a reading of the brief, and the
> scaffolding a design run needs. That is the intended state of this repository,
> not a gap in it.

## What the brief fixes, and what it leaves open

The brief pins down 13 requirements and deliberately leaves
19 decisions to whoever designs the board. The `Source` column says
which is which: `brief` is quoted from [BRIEF.md](BRIEF.md), `metadata` comes
from the benchmark catalogue, and `open` means the brief does not fix it.

| Aspect | Value | Source |
|---|---|---|
| Channel count and mix | Two 4–20 mA inputs and two 4–20 mA outputs (four channels total) | brief |
| System voltage domain | A 24 V industrial module; the brief fixes the nominal domain at 24 V and states no supply tolerance window | brief |
| Isolation boundary | Logic/host side galvanically isolated from field wiring | brief |
| Input fault tolerance | Inputs should tolerate common wiring faults expected in a 24 V cabinet (which faults are not enumerated) | brief |
| Output loop compliance | At least 500 ohm loop load at nominal supply, qualified by "when practical" | brief |
| Host interface | An isolated host interface, either UART or USB — the choice between them is not fixed | brief |
| Calibration storage and status indication | Both required on-board; storage medium, LED count and LED meanings are not fixed | brief |
| Field protection placement | Protection kept at the connector edge (a placement constraint, not a part choice) | brief |
| Creepage and clearance | Isolation barrier maintained with explicit creepage/clearance; the distances themselves are not stated | brief |
| Precision sense node routing | Kelvin connections where applicable | brief |
| Likely layer count | 4 | metadata |
| Category / difficulty / brief detail | industrial-analog; difficulty 3/5; detail 4/5 | metadata |
| Primary stressors | precision current loop, 24V domains, protection, isolation | metadata |
| Board outline, size, mounting, and accuracy targets | Not fixed by the brief — design agent's choice, to be decided and documented | open |

The full split, with the verbatim brief text substantiating every fixed
requirement, is in [board/requirements.md](board/requirements.md) and
machine-readably in [board/requirements.json](board/requirements.json).

**Missing details are design freedom, not permission to fabricate unstated user
requirements.** A choice the brief left open is recorded as a decision, with its
reasoning — never promoted into a requirement.

## Benchmark position

| | |
|---|---|
| Benchmark id | 11 of 32 |
| Category | industrial-analog |
| Difficulty | 3 / 5 |
| Brief detail | 4 / 5 |
| Likely layer count | 4 |
| Primary stressors | precision current loop, 24V domains, protection, isolation |

At difficulty 3/5 with brief detail 4/5, this board tests whether a design agent can honour a genuinely specific analog brief without either dropping stated constraints or inflating them into invented ones. Its stressors — precision current loop, 24V domains, protection and isolation — collide in layout as much as in schematic: the isolation barrier, the connector-edge protection and the Kelvin sense routing are all placement requirements that a plausible-looking schematic can silently violate. The interesting failure mode here is a design that reads correct on paper but cannot substantiate its isolation spacing, its loop compliance headroom, or its accuracy claims.

This repository is one of thirty-two. The suite, the protocol and the results
live in [PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench).

## Repository layout

| Path | Contents |
|---|---|
| `BRIEF.md` | the supplied brief — authoritative, preserved byte for byte, never edited |
| `board/requirements.md` | what the brief fixes, what it leaves open, and where decisions get recorded |
| `board/requirements.json` | the same split, machine-readable, each fixed requirement bound to brief text |
| `board/manifest.template.json` | the toolkit's minimum manifest, pre-filled for this board |
| `board/toolchain.json` | where this board's build finds KiCad and the router |
| `benchmark/metadata.json` | the supplied catalogue entry — category, difficulty, detail, stressors |
| `docs/architecture.md` | the decisions this board must make, as questions, unanswered |
| `docs/sources.md` | the classes of evidence the design will have to cite |
| `docs/status.md` | what exists, what does not, and what is deliberately absent |
| `candidates/` | disposable search output, ignored by Git |
| `.claude/skills/` | the accountability-review skill [CLAUDE.md](CLAUDE.md) requires before a push |
| `tooling/PCBA_AutoDesignAndTest` | the shared verification/routing/release toolkit, as a pinned submodule |

## Getting the repository

The toolkit is a submodule and carries KiCad Routing Tools as a submodule of its
own, so clone recursively:

```bash
git clone --recursive https://github.com/pentolope/PCBA_4_20mA_IO.git
```

```bash
git submodule update --init --recursive
```

## Designing the board

Generic verification, routing and release logic is **not** written here. It is
consumed from `tooling/PCBA_AutoDesignAndTest`, which is board-agnostic by
construction and must stay that way; this repository owns the board and nothing
else. Start from
[the toolkit's onboarding guide](tooling/PCBA_AutoDesignAndTest/examples/onboarding.md),
and see [CLAUDE.md](CLAUDE.md) for the rules a design run works under.

```bash
python3 tooling/PCBA_AutoDesignAndTest/run.py preflight
```

## Brief integrity

`BRIEF.md` SHA-256 `7cf59b5f7204d3e280be2c89489fa2832001794b673967f96952d0f0d6f8157f`

Every quotation in `board/requirements.json` is bound to those exact bytes. If
the brief ever changes, the bindings are stale by construction — which is the
point of recording the digest.
