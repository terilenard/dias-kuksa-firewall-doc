3. Simulation 
=============

3.1 Requirements
----------------

In order to run and test that the FW/IDS run accordingly, there are several requirements that must be present:

* The FW/IDS process should be installed (see previous step).
* The FW/IDS *pycan* process should be installed (see previous step). The FW/IDS can run without SecureLogging, if it is specified in config file.
* Two virtual CAN interface (e.g., vcan0 and vcan1) should be present. A physical CAN controller connection is not a must to run the FW/IDS.
* A CAN trace file (recommended the one, or similar to the one used in `Getting Started with Kuksa <https://dias-kuksa-doc.readthedocs.io/>`_).
* A replay script, that sends the CAN trace file on to the CAN bus. Recommended the *canplayer* player tool which comes from *can-utils*.

3.2 Simulating the CAN
----------------------

3.3 Capturing events
--------------------

3.4
