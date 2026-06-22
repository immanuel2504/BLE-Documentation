**Description:**
Configures the Bluetooth Low Energy (BLE) scanner on the reader.

**Usage:**
Send this command before you start BLE scanning. Set `ble.enable` to `true` to turn on BLE scanning in the reader configuration. You can also include optional settings such as scan interval, RSSI filters, service UUID filters, and protocol-specific filters for iBeacon, AltBeacon, Eddystone, and generic BLE devices. This command saves the BLE configuration but does not start scanning.

**Parameters (MQTT & REST):**

- **ble.enable** (boolean): Set to `true` to enable BLE scanning in the reader configuration. Set to `false` to disable BLE scanning.
- **ble.scanIntervalSec** (integer, optional): Scan interval in seconds. The minimum value is `1`.
- **ble.additionalFilters** (object, optional): Filters that apply across BLE advertisements, such as RSSI and service UUID filters.
- **ble.protocols** (object, optional): Protocol-specific filters for iBeacon, AltBeacon, Eddystone, and generic BLE devices.

<div class="endpoint-block"><div class="ep-heading ep-mqtt">MQTT Endpoint Details</div><table class="endpoint-table"><tbody><tr><td>Command</td><td><code>set_bleConfig</code></td></tr></tbody></table></div>

<div class="endpoint-block"><div class="ep-heading ep-rest">REST Endpoint Details</div><table class="endpoint-table"><tbody><tr><td>Method</td><td><span class="ep-method ep-method-put">PUT</span></td></tr><tr><td>Path</td><td><code>/cloud/ble-config</code></td></tr><tr><td>Request URL</td><td><code>https://&lt;device-ip&gt;/cloud/ble-config</code></td></tr><tr><td>Content-Type</td><td><code>application/json</code></td></tr></tbody></table></div>
