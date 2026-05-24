---
title: "CNC controller retrofit"
date: 2026-05-15
designation: "OP-005"
---

Replaced the original Fanuc 0-M controller on a 1994 Takisawa lathe with a LinuxCNC setup running on a Mesa 7i76e. The old controller had been intermittently faulting on the Z-axis encoder for months and replacement boards are either unavailable or priced like they contain precious metals.

## Background

The lathe itself is mechanically sound — ballscrews are tight, ways are in good shape, spindle bearings were replaced four years ago. The only weak point was the control electronics. Rather than hunting for NOS Fanuc boards or paying for a Fanuc-compatible retrofit kit (which is mostly what you're paying for: Fanuc compatibility you don't need), I went with LinuxCNC.

{{< img src="cnc-original-cabinet.png" alt="Original Fanuc 0-M control cabinet before teardown" >}}

The original cabinet. Everything above the transformer shelf got removed. The servo drives stayed — they accept ±10V analog command signals, which the Mesa card outputs natively.

## Hardware

The control stack is:

- **PC:** Minisforum UM790 Pro (AMD 7940HS). Overkill for CNC but cheap, fanless with the right case, and the integrated GPU handles a large LinuxCNC UI without issues.
- **Interface card:** Mesa 7i76e. Ethernet-connected, handles step/dir or analog servo outputs, 32 I/O, encoder inputs. This is the standard serious-LinuxCNC-build card.
- **Breakout/isolation:** Mesa 7i76e has built-in field I/O isolation. Added a relay board for spindle control and coolant.

{{< img src="cnc-new-controller.png" alt="New controller mounted in the original cabinet" >}}

New controller installed in the same cabinet space. The Mesa card and PC mount on a DIN rail shelf where the Fanuc CPU rack used to live. Wiring runs to the existing terminal strips — the servo drives and I/O didn't change, only what's talking to them.

## Wiring

The messiest part. The Fanuc used a proprietary connector for each axis servo drive. I made adapter cables from the Fanuc connectors to terminal blocks, then ran new signal wires from the terminal blocks to the Mesa card.

{{< img src="cnc-wiring-detail.png" alt="Wiring detail showing adapter cables from Fanuc connectors to new terminal blocks" width="600" >}}

Encoder wiring was the most critical. The original encoders are 1024-line differential, which the Mesa card reads natively — no conversion needed. Just had to get the pinout right (Fanuc uses a non-standard connector but the signals are standard differential RS-422).

## LinuxCNC config

The HAL and INI configuration took about a week of evenings to get right. Main challenges:

- **Tuning the servo loops.** The original Fanuc drives run in velocity mode with the CNC controller closing the position loop. Same topology with LinuxCNC — Mesa card closes position loop, drives follow velocity commands. But the PID tuning took time because I had no documentation on the drive gains.
- **Spindle speed control.** Original spindle drive takes 0-10V for speed command. Mapped to a Mesa analog output. Added an encoder on the spindle for rigid tapping (the one feature the Fanuc actually couldn't do).
- **Tool turret.** The turret uses a grey-code position sensor and a hydraulic advance/clamp solenoid. Wrote a custom HAL component to handle the sequencing.

## Result

Machine runs. Positioning accuracy is within 0.005mm repeatability on both axes (measured with a test indicator over 50 repeated moves). Spindle speed holds within ±2 RPM under load. Rigid tapping works. The whole retrofit cost about $800 in parts plus the time.

The UI runs on a 15" touchscreen mounted where the original Fanuc MDI panel was. Using a modified GMOCCAPY interface with a dark theme. Might write up the UI customisation separately — it's relevant to the HMI design thoughts I've been writing about.
