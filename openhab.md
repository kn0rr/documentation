# Openhab

## Zigbee2MQTT

`configuration.yaml`: /opt/zigbee2mqtt/data$

After changes restart necessary

````bash
# Status Zibee2MQTT Service
serivce zigbee2mqtt status
# Restart Zibee2MQTT Service
serivce zigbee2mqtt restart
````
Example:

````bash
#Configuration.yaml

homeassistant: false
permit_join: true
mqtt:
  base_topic: zigbee2mqtt
  server: mqtt://localhost:1883
  user: openhabian
  password: ''
  client_id: Zigbee
  reject_unauthorized: true
  include_device_information: true
serial:
  port: /dev/ttyACM0
  disable_led: false
devices:
  '0x00158d0006b0fbc2':
    friendly_name: TempSensor1
  '0x00158d0006a04b6c':
    friendly_name: TempSensor2
  '0x00158d0006a0709b':
    friendly_name: TempBad
````

## Openhab Logging

`Logging Console`: ssh -p 8101 openhab@localhost

Logging via `log:tail`
