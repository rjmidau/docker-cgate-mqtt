# cgate-mqtt
MQTT interface for Clipsal C-Bus, written in Node.js, wrapped in a Docker container.

This is a fork of the great work of the1laz and natemason.

## Install:
### Docker
```bash
docker create \
    --name cgate-mqtt \
    -v path/to/config.js:/usr/src/app/config.js \
    --restart unless-stopped \
    rjmidau/cgate-mqtt:$TAG
```

### Docker Compose
```yaml
---
version: '2.1'
services:
  cgate:
    image: rjmidau/cgate-mqtt:$TAG
    container_name: cgate-mqtt
    volumes:
      - path/to/config.js:/usr/src/app/config.js
    restart: unless-stopped
```

## Usage

Detailed guides and supporting articles are on the1laz' blog: https://blog.addictedtopi.com/category/project/cbus/

### Updates get published on these topics:

 - `cbus/read/#1/#2/#3/state` - ON/OFF gets published to these topics if the light is turned on/off

 - `cbus/read/#!/#2/#3/level` - The level of the light gets published to these topics

### Publish to these topics to control the lights:

 - `cbus/write/#1/#2/#3/switch` - Publish ON/OFF to these topics to turn lights on/off

 - `cbus/write/#1/#2/#3/ramp` - Publish a % to ramp to that %. Optionally add a comma then a time (e.g. 50,4s or 100,2m). Also, INCREASE/DECREASE ramp by 5% up or down and ON/OFF turns on/off.

### This requests an update from all lights:

 - `cbus/write/#1/#2//getall` - current values get published on the cbus/read topics

 #1, #2, and #3 should be replaced by your c-bus network number, application number, and the group number.

Requesting an update on start or periodic updates can be set in the settings file.

### This requests the network tree:

 - `cbus/write/#1///gettree` - result gets published as JSON on cbus/read/#1///tree

## Other notes:
* This assumes the default C-Gate ports

