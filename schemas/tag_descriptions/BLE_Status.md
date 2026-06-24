## BLE data events

The start operation starts BLE scanning. It does not return detected tag or beacon data in the command response. After scanning starts, the reader publishes BLE data events to the data endpoints configured for the reader, such as WebSocket, MQTT, Azure, or AWS.

Each BLE data event uses `type: "BLE_DATA"` and includes the detected device information, RSSI, protocol type, protocol-specific fields, and event timestamp.

Example BLE data event:

```json
[
  {
    "data": {
      "Adapter": "/org/bluez/hci0",
      "Address": "52:93:9E:6A:EA:DE",
      "AddressType": "random",
      "Alias": "52-93-9E-6A-EA-DE",
      "Blocked": false,
      "Connected": false,
      "LegacyPairing": false,
      "Paired": false,
      "RSSI": -65,
      "ServicesResolved": false,
      "Trusted": false,
      "UUIDs": [
        "0000feaa-0000-1000-8000-00805f9b34fb"
      ],
      "beaconType": "EDDYSTONE_URL",
      "eddystone": {
        "frameType": "URL",
        "txPower": -18,
        "url": "https://google.com"
      }
    },
    "timestamp": "2026-06-17T21:45:24.045Z",
    "type": "BLE_DATA"
  }
]
```

Read the reader's operational status to confirm the BLE scanner state (`scanState`), when the current scan started (`scanStartTime`), and advertisement counts per protocol (`beaconCounts`). The status response also includes general reader health such as uptime, temperature, CPU, RAM, antenna, and radio state.
