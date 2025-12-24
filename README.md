# z2m

This is my Docker set up for zigbee2mqtt and mosquitto.
I used them with Home Assistant, also running in Docker.


Zigbee needs to have a device, like the Sonoff USB dongle,
which it sees on a serial port on Linux. Not sure what
use you'd have therefore running this project without that.

Currently the serial device setting is nailed down in compose.yaml.

I think the files in the mosquitto and z2m folders are 
generated and maintained by the containers, so I don't
currently check them into github.

## Note on project naming convention

The github project is "docker-z2m" but normally I check it out to ~/docker/z2m/
