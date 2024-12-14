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
| (optional) battery jack                | 2        | 2-pin JST PH e.g. [S2B-PH-K-S](https://www.digikey.com/en/products/detail/jst-sales-america-inc./S2B-PH-K-S/926626)                                |
| battery                                | 2        | [301230 lipo](https://github.com/joric/nrfmicro/wiki/Batteries#301230) recommended for ease of tucking under mcu                                   |
| (optional) FFC connector               | 2        | 12 pin, 0.5mm pitch [example](https://www.lcsc.com/product-detail/FFC-FPC-Connectors_SHENZHEN-ATOM-TECH-FPC05012-09200_C479750.html)               |

## Build order

This is the order (and location) in which I like to install the components:

1. **Diodes**: install these on the *bottom* of the PCB. The line on the diode should be closer to the pad enclosed by a silkscreen marking. If this is unclear, please check the [build tips](#diode-orientation) section below.
2. **Hotswap sockets**: install on the *bottom* of the PCB
3. **Power switch**: install on the *top* of the PCB. You may install it on the bottom if you prefer, but you will then have to adjust the case
4. **Controller**: install on the *top* of the PCB. It is strongly recommended to socket your controller with sufficiently tall sockets so you can put the battery between the controller and the PCB. Be sure to align the labeled pins -- this means that on the left, the MCU will have the components on top, and on the right, the components will be facing down. If you are not confident in determining the controller orientation, I suggest reviewing the [build tips](#mcu-orientation).
5. **Reset button**: install on *top* of the PCB. You may install it on the bottom if you prefer, but you will then have to adjust the case
6. **Battery jack**: install on *top* of the PCB. Note that you will only use 2 of the 3 through holes at any given time. Align the positive (+, conventionally red) terminal of your battery with the *center* hole of the footprint. Check the [build tips](#battery-jack-orientation) for more detailed info. You may install this on the bottom if you prefer, etc etc
7. **FFC connector**: this footprint is only available on one side, so you don't have much of a choice 😅 

> [!NOTE]
> The power switch's ON position is when it is toggled closer to the side with only one pad.
> This means that if you follow the suggestion to install the power switches on the top of the PCB, then the ON positon will correspond to toggling the switch to the LEFT.  
> Yes, this is kind of counter-intuitive and regrettable.  
> No, I did not think of this when designing it.

![power-switch](img/power-switch.jpg)

## Build tips

If you are new to building keyboards or soldering, this section contains some tips, additional details, and visuals that should help.
If anything from that abbreviated build order is unclear, expand the section below:

<details>

<summary> Expand for general soldering tips</summary>

### Soldering SMD (surface mount) components

Via the [Kimiko build guide from keycapsss](https://keycapsss.com/help/kimiko/buildguide_en):

![smd-soldering](img/smd-soldering.png)

Basically:

1. tin one pad (heat and apply a little solder)
2. place the component while heating that pre-tinned side
3. once satisfied with placement and alignment, solder the other side

For self-guiding parts, like hotswap sockets which have plastic housings that fit into holes on the PCB, pre-tinning one side is not as critical -- you can just place the component and solder it in place.

### Soldering THT (through hole) components

Again, via the [Kimiko build guide from keycapsss](https://keycapsss.com/help/kimiko/buildguide_en):

![tht-soldering](img/tht-soldering.png)

Basically:

1. place your component, and tape it in place if necessary
2. flip the board so you can access the pins poking through the plated holes
3. heat the pin **and** the hole
4. feed solder to the heated pin/hole *not* directly to the iron -- this helps to make sure you adequately heated the part, to prevent a cold joint

### Socketing a controller

filterpaper's [guide to socketing microcontrollers](https://filterpaper.github.io/socket-mcu.html) is nice and to the point. In a nutshell:

1. Solder the sockets to the PCB
2. Cover the sockets with kapton tape
3. Insert pins by piercing through the tape
4. Solder the MCU (be **very** careful to verify the MCU orientation at this point). See the [MCU orientation](#mcu-orientation) tip section if you are not sure how to determine this.
5. Remove the MCU, remove the tape, then re-place the MCU in the sockets

For step (1), a common challenge is making sure that the sockets are well aligned, vertically (i.e. pointing straight out of the hole, and not diagonally slanted).
While tape can help, it isn't always sufficient or reliable.  
I like to either use an extra set of sockets placed perpendicularly, or if you have one, an already-socketed MCU is great to force that vertical alignment:

![socket-helper](img/socket-helper.jpg)

### Drag soldering fine pitch components

I've never actually done this yet! Maybe soon I will have tips based on first hand experience, but my general understanding is:

1. Apply a flux to the pins
2. Apply a blob of solder to the first pin
3. Drag the blob across the pins
4. Clean up any bridges

</details>

<details>

<summary>Expand for menura-specific build tips and info</summary>

### Parts overview

Before getting started, here is a quick visual overview of the parts you should have ready to go:

![parts-overview](img/parts-overview.jpg)

###  Diode orientation

The side of the diode with the line corresponds to the pad enclosed by a box on the silkscreen

![diode-orientation](img/diode-orientation.jpg)

### Battery jack orientation

> [!WARNING]
> I assume that red on your battery corresponds to (+) based on common conventions, but this is not guaranteed.
> Before doing anything with your battery, you should [check the battery polarity with a multimeter](https://electronics.stackexchange.com/a/104377), and reverse the instructions below if necessary.

The 3-holed footprint for the 2-pin component is to provide flexiblity in battery jack orientation.
The red (+) wire of your battery will **always** go to the center hole, then you place the black (-) wire to whichever outer hole provides the most convenient orientation for you.  
For example, for my left and right sides, I orient the jack as follows:

![jst-left](img/jst-left.jpg)
![jst-right](img/jst-right.jpg)

### MCU orientation

To verify the MCU orientation, use the labeled pins like GND, RST and VCC as reference points, and ensure that they will be aligned between the MCU and PCB.
Adhering to this simple constraint will guarantee that you install it correctly, rather than trying to remember or interpret "face up", "components down" or some other phrase.

I always like to use the consecutive ground pins as my reference point.
Cross reference with the [nice!nano pinout diagram](https://nicekeyboards.com/docs/nice-nano/pinout-schematic/) to make sure you're reading the pin labels on your MCU correctly:

![mcu-correct-components-up](img/mcu-correct-components-up.jpg)
![mcu-correct-components-down](img/mcu-correct-components-down.jpg)
![mcu-incorrect-flipped](img/mcu-incorrect-flipped.jpg)
![mcu-incorrect-misaligned](img/mcu-incorrect-misaligned.jpg)

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
