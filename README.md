# Home Assistant DobissCAN

Home Assistant custom component for Dobiss via CAN bus controls.

This project is tested with the Waveshare RS485 CAN HAT and a Dobiss Ambiance Pro system without a CAN programmer present.

The integration currently only supports lights. In theory this should be easy to adjust to more general toggleable devices, or even dimmers.

## Hardware

The project requires that your Home Assistant installation has a functional CAN bus interface connected to the CAN bus of your Dobiss installation.

When using a Raspberry Pi I recommend either a USB to CAN adapter or a CAN HAT.

The CAN bus goes over the black RJ12 connector in the center of the unit, make sure you disable the terminator resistor if you add a cable. You can use an RJ11 (telephone) cable as well, since you only need 3 conductors and the outermost pins are not used.

This is the pinout for an RJ12 cable:

3. CAN H
4. GND (don't forget!)
5. CAN L

In my setup, I connected these via an unshielded hand twisted cable to the CAN screw terminals of a RS485/CAN HAT from Waveshare + I tried to ground to one of the GND pins of the Pi's GPIO connector.

The CAN bus speed is 125kbit/s (sometimes known as "low speed can").
You must set up your Pi's OS to configure the bus correctly. As CAN is a network protocol, there are a few options but this generally works:

```
# ip link set can0 type can bitrate 125000
# ifconfig can0 txqueuelen 1000
# ifconfig can0 up
```

These steps must be run every reboot, so I suggest adding them to a script that runs at startup time.

<!-- TODO: describe script --> 

The Dobiss protocol is explained more [here](https://gist.github.com/dries007/436fcd0549a52f26137bca942fef771a).

## Software

This is an addon for Home Assistant in the form of a custom component that can be installed via [HACS](https://hacs.xyz/).


