# MD YM3438 Adapter

![PCB Render](guide-img/pcb.png)

![Installed unit](guide-img/installed.jpeg)

# Status

V1.0 has been assembled and installed in a number of Megadrive units with positive results.

# Overview
This adapter facilitates the install of a YM3438 (OPN2C) in a Sega Mega Drive or Genesis console. Glue logic is present to solve status read bugs that invoke different behavior between the original YM2612 and the CMOS YM3438. In addition, a mixing and buffering circuit (courtesy of [the open source Triple Bypass PCB](https://github.com/tianfeng33/triple-bypass-Version-2)) to both handle the new YM3438 and also provide clean mixing for other signals. The buffer circuit also has provisions to output audio to the original signal path, so that the mono audio output and the headphone jack both work as designed.

These instructions were written using a Japanese VA0 unit as a reference, but principally can apply to any Megadrive or Genesis with a YM2612 in it.

# Kit Assembly Guide

If you have a pre-assembled PCB, you may skip to the installation section.

## Parts List

All SMD capacitors and resistors are of size 0805 (2012 metric).

- 2 x 12 machine pin header strips or 24 pin DIP header
- 1 x YM3438 IC (DIP24)
- 1 x 74HCT08 (SOIC-14)
- 1 x TL972 or similar dual op-amp (SOIC-8)
- 1 x Optional TL972 or similar dual op-amp (DIP-8)
- 2 x 47uF 50V electrolytic capacitor
- 1 x 10uf 16V electrolytic capacitor
- 2 x 10uF/16V SMD capacitor
- 6 x 1uF/16V SMD capacitor
- 2 x 150pF/50V SMD capacitor
- 2 x 330 ohm SMD resistor
- 4 x 10k ohm SMD resistor
- 4 x 100k ohm SMD resistor
- 6 x 210k ohm SMD resistor
- 2 x 300k ohm SMD resistor

## Assembly Process

Populate the components as labeled:

| Designator         | Part            |
|--------------------|-----------------|
| C1-C2              | 10uF / 16V      |
| C3-C8              | 1uF / 16V       |
| C9-C10             | 150pF / 50V     |
| C11                | 10uF/16V TH     |
| C12-C13            | 10uF / 16V TH   |
| C14-C15            | 47uF / 50V      |
| R8-R9, R22-R23     | 100k            |
| R10-R13, R14-R15   | 210k            |
| R16-R17            | 300k            |
| R20-R21            | 10k             |
| R18-R19            | 330             |
| U1                 | TL972           |
| U3                 | 74HCT08         |
| U4                 | YM3438 (OPN2C)  |

I recommend installing the two SMT ICs (TL972 and 74HCT08), followed by the SMT capacitors and resistors, and finally the through-hole parts.

You must install the 74HCT08 and at least the top pin strip before installing the YM3438, or you will not be able to access them. The YM3438 will not sit entirely flat, but this is normal.

# Installation Guide

With the adapter unit ready, some work must be done to the Megadrive motherboard.

## Motherboard Preparation

A few changes will be made to the Megadrive motherboard.

Desolder and remove the YM2612, and the column of capacitors below it (C40, C41, C42, C43, C44, C61, and C62).

![Motherboard top-side component removal diagram](guide-img/prep-topside.jpeg)

On the underside, remove the components marked in red (R34, R37, R40, R41, C45, C46, C47, C48). Remove the components marked in yellow (R53 and R43) and move them to the spot marked in yellow (R40 and R41). As there is no silkscreen on the underside of most revisions, the diagram will be a helpful reference. Install a link between the two pins of capacitors C41 and C43.

![Motherboard bottom-side SMT component removal diagram](guide-img/prep-underside.jpeg)

The new audio will enter through what used to be the MOL and MOR pins for the OPN2, at pins 21 and 20 respectively. The mixed stereo signals enter the original mixing circuit alone, where it then enters the headphone amp as well as the mono mixdown for the CXA-1145.

### Optional op-amp Upgrade

It is optional but recommended to remove the original LM324 op-amp (IC14) that buffers mono audio output with a better unit. Courtesy of [consolemods](https://consolemods.org/wiki/Genesis:Audio_Circuit_Mod) many options exist, but I'll quote TL974I or MC34074 as the first options on their list. This is a DIP8 package.

## Installation in Megadrive

Please be sure you have completed the Motherboard Preparation steps first.

Place the assembled YM3438 adapter unit in the position that once held the original YM2612, and solder it in place on the underside. On the top, five wires are necessary to feed in the various audio signals that compliment the FM sound source. The table below describes the positions shown in the annotated picture below.

| Pad           | Signal    | Motherboard location      |
|---------------|-----------|---------------------------|
| PSG           | PSG audio | C40 (negative pin)        |
| SL1           | Exp. L    | C42 (negative pin)        |
| SR1           | Exp. R    | C44 (negative pin)        |
| SL2           | Cart L    | C61 (negative pin)        |
| SR2           | Cart R    | C62 (negative pin)        |

![Signal wiring diagram](guide-img/wiring-topside.jpeg)

With everything installed, it's up to you how you want to route the audio out. The 'OUT' connector is present so you may run a stereo output to the back of the console, or to some other connector of your choosing. Stereo audio will be present via the headphone jack, and mono audio will be delivered out of the rear A/V connector.

The newly amplified audio is routed through the original signal path for the OPN2 that we replaced. So long as the other audio sources are removed from this path, and we bypass a few components, the original headphone jack and mono output can be made to work as they did in the original.
