**Description:**
Describes the BLE data events that the reader publishes after BLE scanning starts.

**Usage:**
Start BLE scanning with the `start` command or `PUT /cloud/start`. After scanning starts, the reader publishes detected BLE advertisements to the data endpoints configured for the reader, such as WebSocket, MQTT, Azure, or AWS.

The start command response only confirms that scanning started. Detected tags and beacons are delivered separately as BLE data events.

Each BLE data event uses `type: "BLE_DATA"` and includes the detected device information, RSSI, beacon protocol, protocol-specific fields, and event timestamp.

**Event delivery:**

- **WebSocket:** BLE events are sent through the configured WebSocket data connection.
- **MQTT:** BLE events are published to the configured MQTT data topic.
- **Azure or AWS:** BLE events are forwarded to the configured cloud endpoint.

**Payload fields:**

- **type**: Event type. For BLE advertisement data, the value is `BLE_DATA`.
- **timestamp**: Time when the reader generated the event.
- **data**: BLE advertisement details reported by the reader.
- **data.Address**: BLE device address.
- **data.AddressType**: BLE address type, such as `public` or `random`.
- **data.RSSI**: Received signal strength indicator, in dBm.
- **data.UUIDs**: Service UUIDs advertised by the device.
- **data.beaconType**: Detected beacon protocol or frame type.
- **data.eddystone**: Eddystone-specific fields, when the detected advertisement is an Eddystone frame.
