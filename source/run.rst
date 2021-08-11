3. Simulation 
=============

3.1 Requirements
----------------

In order to run and test that the FW/IDS run accordingly, there are several requirements that must be present:

* The FW/IDS process should be installed (see previous step).
* The FW/IDS *pycan* process should be installed (see previous step). The FW/IDS can run without SecureLogging, if it is specified in config file.
* Two virtual CAN interface (e.g., vcan0 and vcan1) should be present. A physical CAN controller connection is not a must to run the FW/IDS.
* A CAN trace file (recommended the one, or similar to the one used in `Getting Started with Kuksa <https://dias-kuksa-doc.readthedocs.io/>`_).
* A replay script, that sends the CAN trace file on to the CAN bus. 
Recommended the *canplayer* player tool which comes from *can-utils* (*can-utils* was installed in the previous steps).

3.2 Simulating the CAN
----------------------

In order to simulate real CAN traffic we will be using *canplayer* to replay an existing trace on the the first CAN interface (VCAN0 if two virtual interfaces were chosen or CAN0 if a phisical interface was chosen).

*can player* only works with .log files, if the trace file is .asc we can use the asc2log_channel_separator.py, found `here <https://github.com/junh-ki/dias_kuksa/tree/master/utils/canplayer>`_ and `addition information here: <https://dias-kuksa-doc.readthedocs.io/en/latest/contents/sim.html#asc2log-conversion>`_
 
 When converting to .log set the parameter *-can* to VCAN0 if a virtual interface is used and CAN0 if a physical interface is used.
 

Once we have the log file we can proceed to replaying the traffic as follows:

* Open another ssh session to the RPI and navigate to the trace file.
* Run canplayer 

.. code-block:: bash

  canplayer -I logfilename.log
* At this point the Pycan module should capture and forward the traffic to the Firewall. This can be observed in the log files for both modules.


3.3 Capturing events
--------------------

3.4
