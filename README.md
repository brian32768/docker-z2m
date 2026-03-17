# docker-z2m

This is my Docker set up for zigbee2mqtt and mosquitto.
I used them with Home Assistant, also running in Docker.

Zigbee needs to have a device, like the Sonoff USB dongle,
which it sees on a serial port on Linux. Not sure what
use you'd have therefore running this project without that.

Currently the serial device setting is nailed down in compose.yaml.

I think the files in the mosquitto and z2m folders are 
generated and maintained by the containers, so I don't
currently check them into github.

## Backups

The files here are backed up by the backup.sh script in ../homeassistant/

## MQTT Broker

I chose Mosquitto because it's very minimal and well supported in HA.

I wanted to try RabbitMQ, but let's face it, MQTT is just not that interesting.
I am sticking with Mosquitto and moving along to other things.

2021-09-28 -- I had to add "allow_anonymous true" to  mosquitto.conf
to get rid of an error message that popped up in the log about auth from HA.

### Mosquitto passwords

Let mosquitto create its config volume then fix its permissions

    docker compose up mosquitto
    ^C
    sudo chmod 660 mosquitto_config/

Copy the template mosquitto.conf file into mosquitto_conf and customize it.

Create a new password file using the password entry you put in config/configuration.yml

To create credential pairs, use the mosquitto_passwd command to create a new file and put a password for homeassistant in it.

   docker run -it --rm -v mosquitto_config:/mosquitto/config eclipse-mosquitto:latest mosquitto_passwd -c /mosquitto/config/passwd homeassistant

To create additional credentials, leave off the -c. For example, 

   docker run -it --rm -v mosquitto_config:/mosquitto/config eclipse-mosquitto:latest mosquitto_passwd /mosquitto/config/passwd wemos

## Note on project naming convention

The github project is "docker-homeassistant" but normally I check it out to ~/docker/homeassistant/

For example, "cd ~/docker/ && git clone https://github.com/brian32768/docker-homeassistant z2m"

## Note on project naming convention

The github project is "docker-z2m" but normally I check it out to ~/docker/z2m/

For example, "cd ~/docker/ && git clone https://github.com/brian32768/docker-z2m z2m"
