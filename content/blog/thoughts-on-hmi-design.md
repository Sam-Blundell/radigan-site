---
title: "Thoughts on industrial HMI design"
date: 2026-05-20
designation: "LOG-008"
---

I've been staring at HMI panels for years now and I have opinions. Most industrial touchscreen interfaces are bad in ways that are completely avoidable. Not bad because the hardware is limited — bad because nobody designing them has thought about the person standing in front of them at 2am during a fault condition.

## The problem with most panels

The default approach seems to be: cram every possible reading onto one screen, use bright colours for everything, and make all the buttons the same size. The result is something that looks busy when things are fine and indistinguishable from normal when things are broken.

{{< img src="hmi-panel-old.png" alt="Typical overloaded HMI panel with too many elements competing for attention" >}}

This is a composite of the kind of thing I see constantly. Every value is displayed at the same visual priority. Alarm states use the same red as decorative borders. Navigation is scattered across all four edges of the screen. There's no hierarchy — your eye has nowhere to land.

## What actually works

The best panels I've used share a few traits:

- **Dark backgrounds.** Not because it looks cool (though it does), but because it gives you a wider range of visual contrast to work with. Light-on-dark text and indicators pop against a dark field in a way that dark-on-light simply can't match in a high-ambient-light environment.
- **Colour means something.** Every colour used on the panel should encode exactly one piece of information. If green means "running," green should never appear for any other reason. No green decorative lines, no green labels, no green backgrounds.
- **Hierarchy by size and position.** The thing that matters most right now should be the largest element. During normal operation, that's probably an overview. During a fault, the fault state should dominate the screen.

{{< img src="hmi-panel-new.png" alt="Redesigned panel with clear visual hierarchy and purposeful use of colour" >}}

## Colour study

I did a small exercise pulling palettes from high-stakes interfaces — aviation, nuclear, military — and comparing them to typical industrial SCADA defaults.

{{< img src="hmi-colour-study.png" alt="Colour palette comparison between aviation interfaces and typical SCADA defaults" width="600" >}}

The aviation palettes use fewer colours and assign rigid semantic meaning to each one. SCADA palettes tend to use colour decoratively (borders, fills, gradients) which dilutes the signal value of any one colour.

## The Death Stranding connection

Kojima's UI team understood this instinctively. The HUD in Death Stranding uses an extremely restrained palette — mostly monochrome with orange as the single accent colour. Information appears only when relevant. When BTs are nearby the entire visual language shifts. You never have to hunt for the important thing because the interface is designed around the assumption that most of the time, most information should be invisible.

That's the principle. Show less. Mean more.
