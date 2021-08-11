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

   wget https://github.com/terilenard/dias-firewall/blob/main/Deb/DIASFirewall_1.0-1_armhf.deb

and 

.. code-block:: bash

   dpkg -i ./DIASFirewall_1.0-1_armhf.deb
   
   sudo apt -f install
   

2.2 Helper processes
--------------------

The Firewall/IDS process uses two additional helper processes. 

1. CanHandler: a process that listens to a CAN interface (e.g. vcan0, /dev/can0), reading incomming frames, extracting their ID and DATA field, and then forwarding the preprocessed data, via a named pipe, to the Firewall/IDS process. The named location of the named pipe can be set in the configuration file, described in the next section.
2. Secure Logging: a additional process, that can be enabled if there is support for a physical or virtual Trusted Platform Module (TPM). This process will only be used by the Firewall/IDS only if in the configuration file is specified to do so. 


2.3 Configuration file
----------------------

A configuration file is used by the Firewall/IDS process to store a set of parameters. The configuration file is name *diasfw.cfg*, and can be found in */etc/...*. It contains the followings:

* *ruleFile* : the location of the XML file, containing the Firewall/IDS set of rules.
* *secureLog* : boolean value under the form of a string. If *"true"* the process will leverage the Secure Logging process to generate signed logs. Else, if it is *"false"* the logs are sent to stdout (file logging, syslog?).
* *canPipe*: path to a named piped used to communicate with a helper process that reads and preprocesses CAN frames. 
* *tpmPipe*: path to a named pipe used to communicate with the Secure Logging process.

2.4 Using the service
---------------------
