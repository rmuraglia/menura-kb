This is more of a personal archival note to document how I did this case design, and isn't really intended for external consumption, but you're welcome to browse it.

# General case shape

Overall, my starting point for building understanding on fusion 360 and case design were:

- [Sadek Baroudi's case design guide](https://github.com/sadekbaroudi/keyboard-guides/tree/master/cases)
- [Hazel's bad wings v1 original case](https://github.com/hazels-garage/bad-wings/tree/master/v1/cases/original), and the minor tinkering I did in that case
- The (unpublished, but shared privately) fusion design file for the [vulpes minora case](https://github.com/sadekbaroudi/vulpes-minora/tree/master/case).

My general approach was going to follow the same general case design composed of:

- a flat bottom plate
- a top switch plate, with offset walls to "reach down" to the plate, and hollowed out areas to provide clearance for top-of-pcb components like the MCU

## Measurements

Base measurements:

- PCB and plate thickness: 1.6mm
- hotswap socket: 1.8mm
- switch bottom to housing to top of clip point: 5mm (from [cherry switch diagram](https://www.cherry.de/en-gb/gaming/developer))
- PCB bottom to USB top: 10mm (on left side, where USB is taller -- this is the tallest component which will determine the overall height)

In general, this integrated plate design suggests that using the bottom of the switch plate as the vertical "origin" from which we will determine relative measurements makes sense.

Derived measurements:

- switch plate top to usb top: 3.4 (10 - 1.6 - 5)
- switch plate bottom to usb top: 5 (3.4 + 1.6)
- mcu hollowed out area: 5.4 (5 + 0.4 buffer) to 7 (+1.6 wall thickness)
    - important +7 is the max height
- switch plate top to bottom of sockets: 6.8 (5 - 1.6 (housing minus plate thickness) + 1.6 (pcb) + 1.8 (sockets))
    - note: Sadek's case guide suggests 8 mm as a safe height for MX hotswap

## Shadow line

This [hackaday article](https://hackaday.com/2023/08/07/enhance-your-enclosures-with-a-shadow-line/) gives a good overview of shadow lines, but the concept is that you use mating pieces, such that on the inside, the parts are flush, but on the outside there is a small gap -- this gap, backed by the flush pieces gives a better appearance of uniformity at the seam, compared to just attempted to get the outermost walls flush with each other.

![shadow-line](img/shadow-line.png)

I rotated and annotated it, to suit my desire to have the top create the gap with an overhang, rather than the bottom reaching up.  
For ease of FDM printing, I was advised to choose measurements in multiples of the nozzle and layer height, so 0.4mm was selected. Some discussion in discord on the topic: [link](https://discord.com/channels/989552667330228374/1104037399517986947/1306638628612739103).

The measurements I ended up choosing were as follows:

- total wall thickness (A): 3mm
- inner wall thickness (C): 1.2mm
- horizontal gap: 0.6 (3 - 1.2 - 1.2 for even wall thicknesses)
    - implies B (outer wall offset) is 1.8 (1.2 + 0.6)
- vertical gap (E): 0.4
- vertical mating notch (D): 1.2 (0.4 gap + 0.8 step)

To minimize repeated manual work in fusion (offsetting curves in sketches), I added outlines for these additional wall thicknesses to my ergogen config (see `(board|shadow)_(inner|outer)_wall`).  
These outlines are all generated with no fillet, to help fusion import gapless DXFs that require minimal fixing.

# Fusion

With all of those measurements in place, we can do the basic extrudes in fusion that give the case its general shape:

## Sketch modifications

Before extruding, I did do some minor sketch modifications to make the extruding easier:

1. I sectioned off the hollow areas, so it can be treated as a different face for extrusion. This generally means extending some lines:
    1. bottom pinky bottom edge to the left wall
    2. tucky thumb tucky edge to bottom wall
    3. reachy thumb reachy edge to bottom wall
    4. vik top and bottom edges to right wall
2. I also cleaned up some leftover, internal lines that did not meaningfully contribute to the outline:
    1. bottom of power switch
    2. bottom left mounting hole
    3. vik and jst overlap
3. Last to provide a wall to connect the raised, hollow areas with switchplate-height part of the case, I added some offsets around the mcu and vik connector.

## Extrudes

1. Bottom going up:
    1. main pcb area: 1.6 baseline thickness
    2. inner ring: 1.6 base + 0.4 gap + 0.8 step = 2.8
    3. middle and outer ring: 1.6 baseline thickness
2. Top going down (from switch plate bottom):
    1. inner + middle wall: 6.8 (meet the 1.2 extra height of the inner ring from the bottom to make a flush 8mm height)
    2. outer ring: 7.6 (6.8 + 0.8 step, leave a 0.4mm shadow line gap)
3. Top going up (from switch plate bottom):
    1. switch plate and thumb cutout: 1.6 baseline thickness
    2. solid max height area (e.g. connecting walls to hollow areas, areas between switches and outer edge of case): 7mm (previously determined max height)
    2. mcu hollowed out area: 5.4 - 7

At this point, I also add the m2 countersunk holes at all the mounting points. 
Note that the outer diameter of the countersunk screw head clearance is 4.4mm.

## Component cutouts

Next we need to add cutouts or windows for all the components.
Luckily, the ergogen config already has these rendered in the sketch, so all we have to do is *project* a relevant line from that sketch onto the desired plane, then draw around that as a reference.

### USB port

### Power switch

### Reset button

### Vik cable

## Magnet holes

6.9 magnet midpoint from top ((7+6.8)/2)
chamfer good
extra space at bottom not needed (undercut)
8mm magnet -> 7.95mm hex https://discord.com/channels/939959680611020840/1054306614158557214/1308157606388437072

## Cosmetics

Fillet, chamfer

# Center wedge