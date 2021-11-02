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
  user: <user>
  password: '<password>'
  client_id: Zigbee
  reject_unauthorized: true
  include_device_information: true
serial:
  port: /dev/ttyACM0
  disable_led: false
devices:
  '<DeviceID 1>':
    friendly_name: TempSensor1
  '<DeviceID 2>':
    friendly_name: TempSensor2
  '<DeviceID 3>':
    friendly_name: TempBad
````

## Openhab Logging

`Logging Console`: ssh -p 8101 openhab@localhost

Logging via `log:tail`
