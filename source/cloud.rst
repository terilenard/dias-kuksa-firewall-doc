5. Cloud Setup
==============

The cloud setup follows a similar approach to the one described in the `DIAS Kuksa setup, Step 3: Cloud Setup <https://dias-kuksa-doc.readthedocs.io/en/latest/contents/cloud.html>`_. MQTT data published by the mqtt client will be received in the Bosch IoT Hub, where a Hono entry point exists. A Hono consumer will read the data from the hub, and saves it into a InfluxDB table. After that, Grafana reads the data saved into the database, and displays its content.

5.1 Requirements
----------------

To follow this page, several things are required:

* A Bosch IoT Hub subscription. If you don't have one a detailed guide on how to obtain one can be found `here <https://dias-kuksa-doc.readthedocs.io/en/latest/contents/cloud.html#bosch-iot-hub-as-hono>`_.
* A secondary Raspberry Pi, or a Ubuntu Virtual Machine.

5.2 InfluxDB Setup
------------------

For the present use case, InfluxDB will be used to 

Ubuntu setup:

.. code-block:: bash
    
    sudo apt install curl

    curl -s https://repos.influxdata.com/influxdb.key | gpg --dearmor > /etc/apt/trusted.gpg.d/influxdb.gpg

    export DISTRIB_ID=$(lsb_release -si); export DISTRIB_CODENAME=$(lsb_release -sc)
    
    echo "deb [signed-by=/etc/apt/trusted.gpg.d/influxdb.gpg] https://repos.influxdata.com/${DISTRIB_ID,,} ${DISTRIB_CODENAME} stable" > /etc/apt/sources.list.d/influxdb.list

    sudo apt-get update && sudo apt-get install influxdb

    sudo systemctl enable influxdb

    sudo systemctl start influxdb

Raspberry Pi setup:

.. code-block:: bash

    wget -qO- https://repos.influxdata.com/influxdb.key | sudo apt-key add -

    echo "deb https://repos.influxdata.com/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/influxdb.list

    sudo apt update

    sudo apt install influxdb

    sudo systemctl unmask influxdb

    sudo systemctl enable influxdb

    sudo systemctl start influxdb

5.3 Hono Consumer Setup
-----------------------

5.4 Grafana Setup
-----------------

Ubuntu setup of Grafana can be found `here <https://dias-kuksa-doc.readthedocs.io/en/latest/contents/cloud.html>`_ . The same steps are listed below for convenience:


.. code-block:: bash

    sudo apt-get install -y apt-transport-https
    
    sudo apt-get install -y software-properties-common wget

    wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -

    echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

    sudo apt-get update

    sudo apt-get install grafana



Raspberry Pi setup:

.. code-block:: bash

    wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -

    echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

    sudo apt update
    
    sudo apt install grafana

    sudo systemctl enable grafana-server

    sudo systemctl start grafana-server

Grafana can be access via a web browser on http://<local-ip>:3000. The default login username is *admin* and default login password is *admin* .


