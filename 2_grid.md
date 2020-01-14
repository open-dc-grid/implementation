# Grid Infrastructure

## Wire thickness

- Wire thickness 1.5 mm² minimum for each connection, thicker cross-section for high current paths (e.g. to battery) recommended
- Current: 20A max, i.e. max. 1 kW per line / daisy chain (something around 10 households in a row)

## Grid ramp-up

How to restart the grid after a an overload condition? What if the load remains too high for the grids modules to restart, how to disconnect the "dead link" from the rest of the grid in a cost effective way?

*Ideas:* In the AC grid, the grid code defines how inverters should behave after full voltage loss, and in cases of sudden voltage drops. Maybe we can do something comparable, e.g. define a ramp with a defined time constant. As for the question on how to isolate the dead links, it depends a lot on the grid topology - a grid where the controller can measure and switch several outputs individually has nice options. Can a single controller detect if there is a grid failure? When the fault has a relatively high resistance, we can't use the voltage or current, as it might not be obvious compared to normal operation, which is also a problem when we want to use basic concepts with fuses, as they might not trip.

## Grounding

*Idea:* Floating system with GND between bus positive and negative using diodes (SELV). This should prevent unintended ground currents as much as possible.

IEEE working group suggests solid negative GND.

Switching should be on the high side in any case as otherwise secondary ground paths could create issues.

## Protection

### Overcurrent and short circuit

Normal fuses and MCBs not suitable in weak voltage environments (no direct battery connection with low impedance). Current sources (i.e. DC/DC converters) would need to be overdimensioned to provide enough fuse tripping current.

Result: Active switching / electronic fuses necessary. Reliable detection of short circuit and overcurrent conditions t.b.d..

### Reverse polarity (at grid side)

- Fuse + Diode: Not suitable because grid impedance might not be high enough to provide enough current to blow the fuse.
- MOSFET
    - High-side: Difficult because gate to source pull-down resistor is outside the circuit to be protected and "sees" the reverse polarity. The driver circuit must prevent pulling up the gate and switching on the MOSFET.
    - Low-side: Straightforward implementation. Possible issues to be checked.
    - General issue: For a device containing several ports to the grid, the MOSFET Vds must be at least twice the grid voltage if it should protect against reverse polarity of hot-plugged previously separate nanogrid parts.

### Arcing

Stable arcs can be generated already at currents as low as 3A and basically at any voltage above 24V. Arcs can build up during intended or unintended disconnection under load, e.g. via a connector or in case of a broken wire. Capacitors on both grid and load side help to minimize the risk of stable arcs.

Open questions:

* How often will the grid be disconnected?
* Is the probability to get stable arcs really that high?
* How high is the risk that the arcs cause a fire?

#### Detection and prevention

The voltage drop created by the arc can only be detected at the load side. Every load must be smart and switch off quickly as soon as it detects a sudden voltage drop.

### Lightning

ToDo
