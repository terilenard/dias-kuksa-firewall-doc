2. Firewall and IDS Setup
=========================

The Firewall (FW) and IDS (Intrusion Detection System) basically function on the same **Rule Processing Engine** (denoted in the following as RPE). Depending on how the rules are written in it's associated **rule file**, the RPE will function as a Stateful Firewall, analyzing sequences of CAN frames based on their identifier field, or as a Intrusion Detection System, by performing a byte-level inspection in the CAN frame data field.

This means, that the FW/IDS is mainly composed in a single process capable of acting in a specific way, depending on it's configuration.

2.1 Installation
----------------

The FW/IDS can be install in two separate ways. Manually, by cloning the source code, install the dependencies and run the build bash script. And secondly, and more convenient, as a Debian package.

For the manual installation the README.md should be followed from the `git repository <https://github.com/terilenard/dias-firewall>`_ .

For the Debian package, the following .deb file must pe downloaded and installed:

.. code-block:: bash

   wget https://github.com/terilenard/dias-firewall/raw/main/Deb/DIASFirewall_1.0-1_armhf.deb

and 

.. code-block:: bash

   dpkg -i ./DIASFirewall_1.0-1_armhf.deb
   
   sudo apt -f install
   

2.2 Helper processes
--------------------

The Firewall/IDS process uses two additional helper processes. 

1. Pycan: a process that listens to a CAN interface (e.g. vcan0, /dev/can0), reading incomming frames, extracting their ID and DATA field, and then forwarding the preprocessed data, via a named pipe, to the Firewall/IDS process. The named location of the named pipe can be set in the configuration file, described in the next section. Furthermore, the recieved frames are forworded to another CAN interface (e.g. vcan1, /dev/can1).
2. Secure Logging: a additional process, that can be enabled if there is support for a physical or virtual Trusted Platform Module (TPM). This process will only be used by the Firewall/IDS only if in the configuration file is specified to do so. 


2.3 Configuration files
-----------------------

2.3.1 Firewall/IDS
------------------

A configuration file is used by the Firewall/IDS process to store a set of parameters. The configuration file named *diasfw.cfg*, and can be found in */etc/diasfw/*. It contains the followings:

* *ruleFile* : the location of the XML file, containing the Firewall/IDS set of rules.
* *secureLog* : boolean value under the form of a string. If *"true"* the process will leverage the Secure Logging process to generate signed logs. Else, if it is *"false"* the logs are saved  (file logging, syslog?).
* *canPipe*: path to a named piped used to communicate with a helper process that reads and preprocesses CAN frames. 
* *tpmPipe*: path to a named pipe used to communicate with the Secure Logging process.

2.3.2 Pycan
-----------

The pycan configuration file *config.py* is located in */etc/diasfw/*. The parameters of interest are the following:

* *PIPE_PATH* : path to a named piped used to communicate with the Firewall/IDS
* *CAN_CHANNEL_REC* : the process will listen for CAN interface on this interface. If a combination of physical interface and virutal interface was chosen than the value for this parameter should be the physical interface (e.g., CAN0). 
* *CAN_CHANNEL_SEND* : the process will forward the incomming frames to this interface. For the current demo those frames will not be used. If a combination of physical interface and virutal interface was chosen than the value for this parameter should be the virtual interface (e.g., VCAN0), else if a combination of two  virutal interfaces was chosen than the value for this parameter should be VCAN1.
* *LOGFILE* : the location of the pycan log file.

2.4 Using the service
---------------------

After installing the *deb* package, two services will be created, namely *diasfw* and *pycan*. Starting/stopping/restarting the services can be done using *systemctl* (e.g., systemctl start pycan, systemctl start diasfw).

The two services are configured to start in the follwing order: pycan, diasfw. To set them to start at boot-up run the following:

.. code-block:: bash

   systemctl enable pycan
   systemctl enable diasfw

For demo purposes you can start them manually, after installing the *deb* package, by running the following:

.. code-block:: bash

   systemctl start pycan
   systemctl start diasfw
   
At this point we recommend opening two additional terminals and tailing the log files.

* new terminal 1 (pycan)

.. code-block:: bash

   tail -f /var/log/diasfw/pycan.log

* new terminal 2 (firewall)

.. code-block:: bash

   tail -f /var/log/diasfw/fwoutput.log
