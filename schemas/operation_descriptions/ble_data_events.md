## BLE Data Events

After BLE scanning starts, the reader publishes detected tag and beacon data to the data endpoints configured for the reader, such as WebSocket, MQTT, Azure, or AWS.

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
