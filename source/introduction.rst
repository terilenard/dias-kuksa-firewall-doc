1. Introduction
===============

In order to use the current manual, there are several requirements that must be meet, in terms of hardware and software. Similarly to `Getting Started with Kuksa <https://dias-kuksa-doc.readthedocs.io>`_ , a in-vehicle setup is needed, together with a cloud part. 

1.1 Requirements
----------------

For the in-vehicle setup one of the following options can be used:

1. Raspberry Pi 3 Model B with Raspbian

2. Raspberry Pi 4 (recommended) with Rasbian

3. Ubuntu Virtual machine

As for the cloud setup:

1. Ubuntu Virtual machine

2. Subscription on `Bosch IoT Hub <https://docs.bosch-iot-suite.com/hub/getting-started/subscribe/>`_

The rest of the steps, were tested on Raspberry Pi's 3 and 4. If a Ubuntu VM is chosen as a in-vehicle setup, some configurations may differ, access to a physical CAN may not be available, thus only a virtual one could be used. This is not a issue since the modules described in the following are meant to work with virtual equivalents for: CAN interfaces (virtual CAN) and Trusted Platform Module (virtual TPM). 

1.1.2 CAN interface
-------------------

Two CAN (Controller Area Network) interfaces are required in order to run the Firewall and Intrusion Detection System described later.
The options here are:

1. Physical Hardware + Virtual Interface

2. Two Virtual Interfaces (recommended)


A guide describing how to setup both a physical connection to a CAN controller (available for Raspberry Pis), and one to a virtual CAN interface (available for Raspberry Pis and Ubuntu) can be found `here <https://github.com/terilenard/dias-kuksa-umfst/wiki/How-to-set-up-CAN-interfaces>`_ . 

For testing purposes, two virtual CAN interface are required. The steps to set up a virtual CAN can be found `in this section <https://github.com/terilenard/dias-kuksa-umfst/wiki/How-to-set-up-CAN-interfaces#how-to-set-up-virtual-can-interface>`_ . After following this steps, a virtual CAN *vcan0* should be visible after running *ifconfig* which can is used to simulate a single CAN bus. The previous steps should be repeated, by replacing *vcan0* with *vcan1*, to create the second virtual CAN interface *vcan1*

Additional information, for different hardware configurations can be found on the `Getting Started with Kuksa: Hardware Setup page <https://dias-kuksa-doc.readthedocs.io/en/latest/contents/hwsetup.html>`_ . 

