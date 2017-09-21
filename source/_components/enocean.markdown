---
layout: page
title: "EnOcean"
description: "Connect EnOcean devices to Home Assistant"
date: 2016-05-25 23:39
sidebar: true
comments: false
sharing: true
footer: true
logo: enocean.png
ha_category: Hub
ha_release: 0.21
ha_iot_class: "Local Push"
---

The [EnOcean](https://en.wikipedia.org/wiki/EnOcean) standard is supported by many different vendors. There are switches and sensors of many different kinds, and typically they employ energy harvesting to get power such that no batteries are unnecessary.

The `enocean` component adds support for some of these devices. You will need a controller like the [USB300](https://www.enocean.com/en/enocean_modules/usb-300-oem/) in order for it to work.

There is currently support for the following device types within Home Assistant:

- [Sensor](/components/sensor.enocean/)
- [Light](/components/light.enocean/)
- [Switch](/components/switch.enocean/)

However, only a few devices have been confirmed to work. These are:

- Eltako FUD61 dimmer
- Eltako FSR61 switch
- Eltako FHF window handle
- Eltako FT55 battery-less wall switch

Other devices will most likely need some changes in the Home Assistant code in order to work.


To integrate an EnOcean controller with Home Assistant, add the following section to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
enocean:
  device: /dev/ttyUSB0
```

Configuration variables:

- **device** (*Required*): The port where your device is connected to your Home Assistant host.


Base ID:

Every EnOcean adapter uses a unique Base ID. Starting from the Base ID the next 128 IDs can be used as sender IDs when sending telegrams to other devices like switches or dimmers.
The Base ID of the adapter is requested during startup and visible in the logfile and also in a state called enocean.xxxxxxxx

Teach In

The component provides a service to send teahc in telegrams to devices. The device needs to be before the teach in service can be used. The only parameters for the service is the entity_id of the target device.
