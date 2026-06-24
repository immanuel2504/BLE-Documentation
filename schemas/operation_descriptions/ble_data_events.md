**Description:**
Explains how BLE tag and beacon data is reported after BLE scanning starts.

**Usage:**
Start BLE scanning with the `start` command or `PUT /cloud/start`. After scanning starts, the reader publishes detected BLE advertisements to the data endpoints configured for the reader, such as WebSocket, MQTT, Azure, or AWS.

The start command response only confirms that scanning started. Detected tags and beacons are delivered separately as BLE data events.

Each BLE data event uses `type: "BLE_DATA"` and includes the detected device information, RSSI, beacon protocol, protocol-specific fields, and event timestamp.

**Where BLE data is received:**

- **WebSocket:** BLE events are sent through the configured WebSocket data connection.
- **MQTT:** BLE events are published to the configured MQTT data topic.
- **Azure or AWS:** BLE events are forwarded to the configured cloud endpoint.

**Example BLE data event:**

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
