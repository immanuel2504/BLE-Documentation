**Description:**
Stops BLE scanning on the reader.

**Usage:**
Send this command with `scanType` set to `["ble"]` to stop BLE scanning only. Set `scanType` to `["ble", "rfid"]` to stop both BLE scanning and RFID inventory. Always wait for the success response before you change BLE configuration or start scanning again.

**Parameters (MQTT & REST):**

- **scanType** (array): Scan modes to stop. Use `["ble"]` for BLE only, or `["ble", "rfid"]` for both BLE and RFID.

<div class="endpoint-block"><div class="ep-heading ep-mqtt">MQTT Endpoint Details</div><table class="endpoint-table"><tbody><tr><td>Command</td><td><code>stop</code></td></tr></tbody></table></div>

<div class="endpoint-block"><div class="ep-heading ep-rest">REST Endpoint Details</div><table class="endpoint-table"><tbody><tr><td>Method</td><td><span class="ep-method ep-method-put">PUT</span></td></tr><tr><td>Path</td><td><code>/cloud/stop</code></td></tr><tr><td>Request URL</td><td><code>https://&lt;device-ip&gt;/cloud/stop</code></td></tr><tr><td>Content-Type</td><td><code>application/json</code></td></tr></tbody></table></div>
