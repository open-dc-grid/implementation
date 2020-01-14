# Devices and Appliances

The following chapters describe ideas for actual implementation of devices or the nanogrid controller.

## Grid controller power stage

The following image shows the implementation of the DC/DC power stage that could be integrated in a device connected directly to the grid.

![Grid controller DC/DC power stage](./images/grid-controller-power-stage.svg)

Grid switching and current measurement should be implemented on the high-side in order to provide a consistent ground path.

## Node types

### Solar Home System (SHS)

* Retrofit to existing SHS
* Dedicated grid-connected household
    * Without battery / PoL converter
    * With small battery as buffer (easier control)

### Battery

Ideally 12 V or 24 V batteries to remain below the grid voltage and allow use of simple synchronous buck converters.

### Solar

PV modules can be connected directly to the grid or to a battery acting as a buffer.
