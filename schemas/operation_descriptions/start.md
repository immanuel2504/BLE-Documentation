**Description:**
Starts BLE scanning on the reader.

**Usage:**
Send this command after you save the BLE configuration with `set_bleConfig`. Set `scanType` to `["ble"]` to start BLE scanning only. Set `scanType` to `["ble", "rfid"]` to start BLE scanning and RFID inventory together. If BLE is not enabled in the saved configuration, the reader does not scan for BLE advertisements.

**Parameters (MQTT & REST):**

- **scanType** (array): Scan modes to start. Use `["ble"]` for BLE only, or `["ble", "rfid"]` for combined BLE and RFID scanning.

<div class="endpoint-block"><div class="ep-heading ep-mqtt">MQTT Endpoint Details</div><table class="endpoint-table"><tbody><tr><td>Command</td><td><code>start</code></td></tr></tbody></table></div>

<div class="endpoint-block"><div class="ep-heading ep-rest">REST Endpoint Details</div><table class="endpoint-table"><tbody><tr><td>Method</td><td><span class="ep-method ep-method-put">PUT</span></td></tr><tr><td>Path</td><td><code>/cloud/start</code></td></tr><tr><td>Request URL</td><td><code>https://&lt;device-ip&gt;/cloud/start</code></td></tr><tr><td>Content-Type</td><td><code>application/json</code></td></tr></tbody></table></div>
