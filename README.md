# M5StackSolar2MQTT
measure solar panel voltage and current on M5Stack, transmit via MQTT to Node Red

## Hardware / BOM
* Solar Panel with Controller (and USB output)
* [M5Stack](https://shop.m5stack.com/collections/m5-core/products/grey-development-core)
* [Voltmeter Unit (ADS1115)](https://shop.m5stack.com/collections/m5-unit/products/voltmeter-unit-ads1115)
* [Ammeter Unit (ADS1115)](https://shop.m5stack.com/collections/m5-unit/products/ammeter-unit-ads1115)
* [Grove-T Connector](https://shop.m5stack.com/collections/m5-accessory/products/grove-t-connector-5pcs-a-pack)
* [Grove Cable](https://shop.m5stack.com/collections/m5-accessory/products/4pin-buckled-grove-cable)

## High-Level flow

* Solar panel 
  * Ammeter wired in line between solar panel and controller
  * Voltmeter wired in parallel to the solar panel
* Solar Controller
  * M5Stack plugged into USB output of solar controller
* M5Stack
  * connect to Wifi & MQTT
  * measure voltage and current every couple of seconds and display on screen
  * transmit via MQTT every 20 seconds as a JSON object on topic "SolarPanel"
* Node-Red
  * receive and parse the JSON object on topic "SolarPanel"
  * calculate power and convert units
  * upload resulting data to InfluxDB
* Grafana
  * load data from InfluxDB and display it
  
## Installation
* Install and configure
  * [Node-Red](https://nodered.org/) plus this node:
    * node-red-contrib-influxdb
  * [InfluxDB](https://www.influxdata.com/products/influxdb-overview/)
  * [Grafana](https://grafana.com/)
  * I used [DietPi](https://dietpi.com/) to conveniently install all on a Raspberry Pi
* Create a database in InfluxDB
* Import M5Stack project to [UIFlow](https://flow.m5stack.com/), adjust your MQTT details and upload to M5Stack
* Import Flow to Node-Red, configure MQTT and InfluxDB details and deploy
* Import Panel to Grafana and configure InfluxDB details

## Images
![solar panel](/images/solarpanel.jpg)
![M5Stack wiring](/images/m5stack.jpg)
![Grafana](/images/grafana.jpg)
  
