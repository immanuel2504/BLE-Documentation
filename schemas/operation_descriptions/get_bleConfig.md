**Description:**
Retrieves the current Bluetooth Low Energy (BLE) scanner configuration stored on the reader.

**Usage:**
Send this command with an empty payload to check the current BLE configuration. Use the response to confirm that BLE scanning is enabled, review scan interval and filter settings, or verify the result of a previous `set_bleConfig` command.

**Parameters (MQTT & REST):**

_No parameters required._

<div class="endpoint-block"><div class="ep-heading ep-mqtt">MQTT Endpoint Details</div><table class="endpoint-table"><tbody><tr><td>Command</td><td><code>get_bleConfig</code></td></tr></tbody></table></div>

<div class="endpoint-block"><div class="ep-heading ep-rest">REST Endpoint Details</div><table class="endpoint-table"><tbody><tr><td>Method</td><td><span class="ep-method ep-method-get">GET</span></td></tr><tr><td>Path</td><td><code>/cloud/ble-config</code></td></tr><tr><td>Request URL</td><td><code>https://&lt;device-ip&gt;/cloud/ble-config</code></td></tr><tr><td>Content-Type</td><td><code>application/json</code></td></tr></tbody></table></div>
