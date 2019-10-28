# Homebridge Relays

Controls 4 channel relays with a Raspberry Pi using HomeKit.

# Hardware

The hardware is quite simple to construct.

1. Raspberry Pi 3 Model B
2. 4-relay module pins are connected to 4 GPIO pins (GPIO-17, 27, 22, 05). 

The raspberry pi can then control the state of the relays

# Installation

1. Install homebridge using: `sudo npm install --unsafe-perm -g homebridge`
2. Install this plugin using: `sudo npm install -g --unsafe-perm homebridge-relays`
3. Update your configuration file. See `config-sample.json` in this repository for a sample.

# Sample Configuration

    {
      "bridge": {
        "name": "RelayServer",
        "username": "CC:22:3D:E3:CE:FA",
        "port": 51826,
        "pin": "031-45-155"
      },

      "description": "4 Channel Relay",

      "accessories": [
        {
          "accessory": "Relay",
          "name": "Relay-1",
          "pin": 11
          "invert": true,
	  "read_pin": 12,
	  "read_invert": true,
          "default_state": false,
          "duration": 1000
        },
        {
          "accessory": "Relay",
          "name": "Relay-2",
          "pin": 13
          "invert": false,
          "default_state": false,
          "duration": 3600000
        },
        {
          "accessory": "Relay",
          "name": "Relay-3",
          "pin": 15
        },
        {
          "accessory": "Relay",
          "name": "Relay-4",
          "pin": 29
        }
      ],

      "platforms": []
    }

# Accessory Configuration Options

Name             | Meaning
---------------- | ------------------------------------------------
`accessory`      | Accessory type. `Relay` (REQUIRED)
`name`           | Default name for the accessory. (REQUIRED)
`pin`            | Which output pin number to use for this accessory. (REQUIRED)
`invert`         | If true, output on `pin` is inverted; `LOW` for `ON`, and `HIGH` for `OFF`. (Default: false)
`read_pin`       | If given, specifies an alternate pin to read the current state from.  (Default: same as `pin`)
`read_invert`    | If true, input from `read_pin` is inverted; `LOW` for `ON` and `HIGH` for `OFF`.  (Default: false)
`default_state`  | State to set on start of homebridge.  `true` for `ON`, `false` for `OFF`.  (Default: `false`/`OFF`)
`duration_ms`    | If given, accessory will stay ON for this many milliseconds, then turn OFF.  Timer resets if accessory is turned ON again while it is still ON. (Default: 0/None)


