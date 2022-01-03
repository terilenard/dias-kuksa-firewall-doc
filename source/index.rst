.. DIAS Firewall How To documentation master file, created by
   sphinx-quickstart on Mon Aug  9 11:39:36 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to DIAS UMFST How To's documentation!
=============================================

The current page serves as the official documentation developed by UMFST (University of Medicine, Pharmacy, Science and Technology of Targu Mures), as part of the 
DIAS (Diagnostic Anti-Tampering Systems) H2020 project.

This documentation is a follow up to `Getting Started with Kuksa <https://dias-kuksa-doc.readthedocs.io>`_ describing how to install, configure and use, UMFST's Firewall, Intrusion Detection System, and Secure Logging solutions (in the future), in conjunction with the Kuksa setup described in the previous mentioned link. As the project progresses, the current documentation and source codes used here may suffer changes. 

The reader is advised to follow the sections below in sequence, since there are dependencies between a step, and a previous one. For example, the Firewall requires a physical or virtual CAN (Controller Area Network) interface from where it can read CAN frames. Similarly to use the Secure Logging, a physical or virtual TPM (Trusted Platform Module) must be configured.
 
.. toctree::
   :maxdepth: 2
   :caption: Contents:
   
   introduction
   setup
   run
   rules
   cloud

Research
---------

Teri Lenard and Roland Bolboaca. 2021. A Statefull Firewall and Intrusion Detection System Enforced with Secure Logging for Controller Area Network. European Interdisciplinary Cybersecurity Conference. Association for Computing Machinery, New York, NY, USA, 39–45. DOI:https://doi.org/10.1145/3487405.3487650


Acknowledgement
---------------

This work was funded by the European Union’s Horizon 2020 Research and Innovation Programme through DIAS project under Grant Agreement No. 814951. 
This document reflects only the author’s view and the Agency is not responsible for any use that may be made of the information it contains

Authors
-------

Authors can be found and contacted on: **https://nislab.umfst.ro/**
