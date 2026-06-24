**Description:**
Starts BLE scanning on the reader.

**Usage:**
Send this command after you save the BLE configuration with `set_bleConfig`. Set `scanType` to `["ble"]` to start BLE scanning only. Set `scanType` to `["ble", "rfid"]` to start BLE scanning and RFID inventory together. If BLE is not enabled in the saved configuration, the reader does not scan for BLE advertisements.

**BLE data events:**
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

**Parameters (MQTT & REST):**

- **scanType** (array): Scan modes to start. Use `["ble"]` for BLE only, or `["ble", "rfid"]` for combined BLE and RFID scanning.

<div class="endpoint-block"><div class="ep-heading ep-mqtt">MQTT Endpoint Details</div><table class="endpoint-table"><tbody><tr><td>Command</td><td><code>start</code></td></tr></tbody></table></div>

<div class="endpoint-block"><div class="ep-heading ep-rest">REST Endpoint Details</div><table class="endpoint-table"><tbody><tr><td>Method</td><td><span class="ep-method ep-method-put">PUT</span></td></tr><tr><td>Path</td><td><code>/cloud/start</code></td></tr><tr><td>Request URL</td><td><code>https://&lt;device-ip&gt;/cloud/start</code></td></tr><tr><td>Content-Type</td><td><code>application/json</code></td></tr></tbody></table></div>
