2. Firewall and IDS Setup
=========================

The Firewall and IDS (Intrusion Detection System) basically function on the same **Rule Processing Engine** (denoted in the following as RPE). Depending on how the rules are written in it's associated **rule file**, the RPE will function as a Stateful Firewall, analyzing CAN frames based on their identifier field, or as a Intrusion Detection System, by performing a byte-level inspection in the CAN frame data field.

This means, that the Firewall/IDS is mainly composed in a single process capable of acting in a specific way, depending on it's configuration.

2.1 Installation
----------------

The Firewall/IDS can be install in two separate ways. Manually, by cloning the source code, install the dependencies and run the build bash script. And secondly, and more convenient, as a Debian package.

For the manual installation the README.md should be followed from the `git repository <https://github.com/terilenard/dias-firewall>`_ .

For the Debian package, the following .deb file must pe downloaded and installed:

.. code-block:: bash

   wget https://github.com/terilenard/dias-firewall

and 

.. code-block:: bash

   sudo dpkg -i dias-firewall.deb   

2.2 Helper processes
--------------------


2.3 Configuration file
----------------------

A configuration file is used by the Firewall/IDS process to store a set of parameters. The configuration file is name *diasfw.cfg*, and can be found in */etc/...*. It contains the followings:

* *ruleFile* : the location of the XML file, containing the Firewall/IDS set of rules.
* *secureLog* : boolean value under the form of a string. If *"true"* the process will leverage the Secure Logging process to generate signed logs. Else, if it is *"false"* the logs are sent to stdout (file logging, syslog?).
* *canPipe*: path to a named piped used to communicate with a helper process that reads and preprocesses CAN frames. 
* *tpmPipe*: path to a named pipe used to communicate with the Secure Logging process.