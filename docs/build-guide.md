
# Building the PCB

## BOM

| Part                                   | Quantity | Notes                                                                                                                                              |
| -------------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| menura PCB                             | 2        | PCB is reversible. Fabrication files can be found in the [releases](https://github.com/rmuraglia/menura-kb/releases) section.                      |
| controller                             | 2        | [nice!nano](https://nicekeyboards.com/nice-nano) or [suitable alternative](https://github.com/joric/nrfmicro/wiki/Alternatives#supermini-nrf52840) |
| (optional) controller sockets and pins | 48       | e.g. [sockets](https://github.com/joric/nrfmicro/wiki/Sockets)                                                                                     |
| diode                                  | 44       | SOD-123 1N4148W [example](https://www.lcsc.com/product-detail/Switching-Diode_GOODWORK-1N4148W_C909967.html)                                       |
| hotswap socket                         | 44       | MX                                                                                                                                                 |
| reset button                           | 2        | through hole 2 pin 3x6mm, e.g. [MJTP1243](https://www.digikey.com/en/products/detail/apem-inc/MJTP1243/1798039)                                    |
| power switch                           | 2        | PCM12-like, e.g. [MSK12C02](https://www.lcsc.com/product-detail/Toggle-Switches_SHOU-HAN-MSK12C02_C431540.html)                                    |
| battery jack                           | 2        | 2-pin JST PH e.g. [S2B-PH-K-S](https://www.digikey.com/en/products/detail/jst-sales-america-inc./S2B-PH-K-S/926626)                                |
| battery                                | 2        | [301230 lipo](https://github.com/joric/nrfmicro/wiki/Batteries#301230) recommended for ease of tucking under mcu                                   |
| (optional) FFC connector               | 2        | 12 pin, 0.5mm pitch [example](https://www.lcsc.com/product-detail/FFC-FPC-Connectors_SHENZHEN-ATOM-TECH-FPC05012-09200_C479750.html)               |

## Build order

This is the order (and location) in which I like to install the components:

1. **Diodes**: install these on the *bottom* of the PCB. The line on the diode should be closer to the pad enclosed by a silkscreen marking. If this is unclear, please check the [build tips](#build-tips) section below.
2. **Hotswap sockets**: install on the *bottom* of the PCB
3. **Power switch**: install on the *top* of the PCB. You may install it on the bottom if you prefer, but you will then have to adjust the case
4. **Controller**: install on the *top* of the PCB. It is strongly recommended to socket your controller with sufficiently tall sockets so you can put the battery between the controller and the PCB.
5. **Reset button**: install on *top* of the PCB. You may install it on the bottom if you prefer, but you will then have to adjust the case
6. **Battery jack**: install on *top* of the PCB. Note that you will only use 2 of the 3 through holes at any given time. Align the positive (+, conventionally red) terminal of your battery with the *center* hole of the footprint. Check the [build tips](#build-tips) for more detailed info. You may install this on the bottom if you prefer, etc etc
7. **FFC connector**: this footprint is only available on one side, so you don't have much of a choice 😅 

Note on power switch on/off positions

## Build tips

If you are new to building keyboards or soldering, this section contains some tips, additional details, and visuals that should help.
If anything from that abbreviated build order is unclear, expand the section below:

<details>

<summary>Expand for additional build tips and info</summary>

###  Diode orientation

Picture

### Battery jack orientation

Picture, explanation, why 3 holes?

### Socketing a controller

Tip from duet, tape trick for pins

### Soldering SMD (surface mount) components

Tin one side, place while heating, do other side.
For self-guiding parts like hot swap sockets, no need to pre-tin

### Soldering THT (through hole) components

Tape, solder

### Drag soldering fine pitch components

I've never actually done this lmao

</details>

# Assembling the keyboard

## BOM

| Part                           | Quantity | Notes                                                                                                                           |
| ------------------------------ | -------- | ------------------------------------------------------------------------------------------------------------------------------- |
| built menura pcb               | 2        |                                                                                                                                 |
| menura bottom plate            | 2        | all layouts share one common bottom plate                                                                                       |
| menura top plate               | 2        | choose the top plate corresponding to your layout (e.g. 3x5_3, 3x5_2 or 23332_2)                                                |
| MX switches                    | 30-36    |                                                                                                                                 |
| MX keycaps                     | 30-36    |                                                                                                                                 |
| m2 screws                      | 16       | countersunk, 5mm works, other lengths are probably fine too                                                                     |
| m2 spacers                     | 8        | 8mm                                                                                                                             |
| rubber feet                    | 8+       | e.g. 3M bumpons, SKUF rubber feet, adhesive neoprene etc                                                                        |
| (optional) menura center wedge | 1        | choose a wedge corresponding to your desired distance and angle between halves when in unibody mode                             |
| (optional) magnets             | up to 20 | 8x2mm round [example](https://www.amazon.com/gp/product/B09BB1VT4J/), tune magnet count to match desired strength of connection |

## Assembly

> [!WARNING]
> Before installing the PCB into a case, it is highly recommended to [flash a test firmware](#studio) and verify that everything is working as expected

1. Insert a few (4-ish) switches into the top plate. I usually use the switches in the corners.
2. Insert the switch pins from that assembly into the PCB's hotswap sockets
3. Ensure that all the switches look well aligned
4. Insert the rest of the switches into the plate and PCB
5. From the bottom, insert the spacers through the PCB's mounting holes
6. From the top, screw in a set of screws to hold the spacers in place
7. Align the bottom plate with the spacers, and screw in the second set of screws
8. If inserting magnets, press fit them into the holes
    1. double check the magnet orientation before insertion
    2. the hole's tolerance may be slightly off -- you may need to either scrape the hole with a blade to make more room, or use a dot of glue to hold the magnet in place
9. Stick on a set of rubber feet
10. Install keycaps

# Flashing firmware

## Studio

Default firmware ships with ZMK studio so you can make changes in the fly from a UI, but...
together they have a combo to unlock studio
each half has a combo to access the bootloader

https://github.com/rmuraglia/zmk-keyboards-menura/blob/main/boards/shields/menura/menura.keymap

## ZMK config

If you want to roll your own config...
