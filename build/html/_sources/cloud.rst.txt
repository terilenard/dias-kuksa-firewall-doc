5. Cloud Setup
==============

The cloud setup follows a similar approach to the one described in the `DIAS Kuksa setup, Step 3: Cloud Setup <https://dias-kuksa-doc.readthedocs.io/en/latest/contents/cloud.html>`_. MQTT data published by the mqtt client will be received in the Bosch IoT Hub, where a Hono entry point exists. A Hono consumer will read the data from the hub, and saves it into a InfluxDB table. After that, Grafana reads the data saved into the database, and displays its content.

5.1 Requirements
----------------

To follow this page, several things are required.

* A Bosch IoT Hub subscription. If you don't have one a detailed guide on how to obtain one can be found `here <https://dias-kuksa-doc.readthedocs.io/en/latest/contents/cloud.html#bosch-iot-hub-as-hono>`_.
* A secondary Raspberry Pi, or a Ubuntu Virtual Machine

5.2 InfluxDB Setup
------------------

5.3 Hono Consumer Setup
-----------------------

5.4 Grafana Setup
-----------------
