**Description:**
Retrieves operational status and runtime statistics from the reader, including the BLE scanner state and beacon counts.

**Usage:**
Send this command with an empty payload to read the reader's current status. For BLE, use the `ble` section of the response to confirm whether scanning is active (`ble.scanState`), when the current scan started (`ble.scanStartTime`), and how many advertisements have been observed per protocol (`ble.beaconCounts`). The `ble` section is present only when BLE is supported and its status is available. The response also reports general reader health such as uptime, temperature, CPU, RAM, antenna, and radio status.

**BLE status fields:**

- **ble.scanState** (string): Current BLE scanner state — `running` or `stopped`.
- **ble.scanStartTime** (string, date-time): ISO 8601 timestamp of when the BLE scan was last started.
- **ble.beaconCounts** (object): Advertisement counts for the current scan window — `total`, `iBeacon`, `altBeacon`, `eddystone`, and `generic`.

<div class="endpoint-block"><div class="ep-heading ep-mqtt">MQTT Endpoint Details</div><table class="endpoint-table"><tbody><tr><td>Command</td><td><code>get_status</code></td></tr></tbody></table></div>

<div class="endpoint-block"><div class="ep-heading ep-rest">REST Endpoint Details</div><table class="endpoint-table"><tbody><tr><td>Method</td><td><span class="ep-method ep-method-get">GET</span></td></tr><tr><td>Path</td><td><code>/cloud/status</code></td></tr><tr><td>Request URL</td><td><code>https://&lt;device-ip&gt;/cloud/status</code></td></tr><tr><td>Content-Type</td><td><code>application/json</code></td></tr></tbody></table></div>
