# Voltage Controlled Amplifier

A Voltage Controlled Amplifier amplifies an audio signal based on the voltage control signal. Can be used to shape the incoming audio to an envelope or apply tremolo (envelope not included :).

The circuit here is based on the [Yusynth VCA](https://yusynth.net/Modular/EN/VCA/index.html) with minor tweaks to make it more Eurorack friendly. The changes I've made are thus:
* Selected resistors appropriate for +/-12V rails,
* Added polarity protection so that a backward power header doesn't fry anything (twin series schotty diodes: BAT54SL),
* Selected a modern dual NPN diode package for matched transistors,
* Full surface mount design.

The Yusynth page is a treasure trove of information about this circuit that I am too amateur to claim as my own; please read that outstanding page before using this circuit. The page provides many details and other implementations of this circuit that you may find suitable.

The KiCAD project here uses the library/footprints [found in my companion repo](https://github.com/thismatters/EurorackKiCAD).

## Width

6hp on a standard 3U rack.

## Inputs

Twin control voltage inputs, the left input (marked `cv 1`) is attenuated by the `control lvl` knob.
Likewise there are two audio signal inputs, the left of these (marked `in 1`) is attenuated by the `input lvl` knob. An LED near the `input lvl` knob indicates the level of the audio input signal.
The `gain` knob overrides both CV inputs to amplify the input.

## Outputs

Twin outputs. Audio signal.

## Fiddly bits

This module can be _either_ AC or DC coupled.
For the AC coupled version build the circuit as documented.

When assembling, be sure to trim your trimmer legs pretty short lest they short on the body of the potentiometer.

### DC Coupled Version

For the DC coupled version omit the capacitors C1 and C2; short the two pins with wire (you still totally need C3 and C4 though for power regulation!).
Also use linear taper potentiometers for RV1, RV2, and RV3 (still 100kOhm) (Tayda part number `A-2963`).

## Adjustment

You'll need a dual trace oscilloscope a digital volt meter and function generator.

### Input (Cl)amping

1. Turn the `input lvl` knob to maximum (fully clockwise).
1. Turn the `gain` knob to maximum (fully clockwise).
1. Connect your function generator to the leftmost audio input (marked `in 1`) and to one of the oscilloscope channels.
1. Set up your function generator to give a 1kHz sine at 4 volts (peak to peak).
1. Connect the other oscilloscope channel to one of the outputs.
1. Adjust RV4 until the two oscilloscope traces match exactly. (If your output has flat peaks or troughs then a little tweak to RV6 will smooth those out)
1. Turn the `gain` knob to minimum (fully counterclockwise, there must also be no control voltage plugged in).
1. Adjust RV6 until there is no signal output which appears on the oscilloscope.

### DC Offset

1. Disconnect all inputs.
1. Turn all knobs to minimum (fully counterclockwise).
1. Connect your voltmeter to TP1.
1. Adjust RV5 until the voltmeter reads 0V.

## Vendors

There are part numbers in the [BOM](vca.csv) for many of the parts (not for basic passives though) at the following vendors:

* [Mouser](https://www.mouser.com): Needs no introduction. Get your ICs from here (or [digikey](https://www.digikey.com)).
* [Tayda Electronics](https://www.taydaelectronics.com/): Good supplier for passive components; audio jacks, and potentiometers. Their audio jacks are slightly smaller than the thonkiconn from thonk.
* [Love My Switches](https://lovemyswitches.com/): Has [really good knobs](https://lovemyswitches.com/anodized-aluminum-knob-the-lo-fi-1-4-smooth-shaft-12-5mm-od/) to go on those potentiometers!
* [OSHPark](https://oshpark.com/): Fast and (relatively) cheap PCB manufacturer. The [V1 circuit](https://oshpark.com/shared_projects/VmwAFYtq) works well.


## Changelog

### V2

- [x] Switched to NPN for driving LED
- [x] Updated design language (redid board layout too!)
- [x] Switched to SMD discrete transistors
