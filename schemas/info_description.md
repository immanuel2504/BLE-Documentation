MQTT and REST API for configuring and controlling Bluetooth Low Energy (BLE) scanning on the Zebra FXR90 fixed RFID reader.

## Overview

The FXR90 reader supports passive BLE advertisement scanning alongside RFID inventory. Configure BLE first, verify the saved configuration, and then start scanning when the reader is ready to collect BLE advertisements.

## REST workflow

Use REST when you integrate directly with the reader over HTTPS.

1. **Configure BLE scanning.** Send `PUT /cloud/ble-config` to save how the reader should scan. Set `ble.enable` to `true` (required) to allow BLE scanning, and add any optional settings in the same request: `scanIntervalSec` for how often the reader collects results, `additionalFilters` for cross-protocol RSSI and service-UUID filters, and `protocols` for per-protocol filters (iBeacon, AltBeacon, Eddystone, generic). This request only saves the configuration — it does not start scanning. Scanning begins in step 3.
2. **Verify the configuration.** Send `GET /cloud/ble-config` and confirm that `ble.enable` is `true` and your filters were saved as expected.
3. **Start BLE scanning.** Send `PUT /cloud/start` with `scanType: ["ble"]`.
4. **Collect BLE events.** The reader publishes BLE advertisement events as it detects beacons.
5. **Stop BLE scanning.** Send `PUT /cloud/stop` with `scanType: ["ble"]`.

## MQTT workflow

Use MQTT when you send commands through the reader's command topic.

1. **Configure BLE scanning.** Send `set_bleConfig` to save how the reader should scan. Set `payload.ble.enable` to `true` (required) to allow BLE scanning, and add any optional settings in the same command: `scanIntervalSec` for how often the reader collects results, `additionalFilters` for cross-protocol RSSI and service-UUID filters, and `protocols` for per-protocol filters (iBeacon, AltBeacon, Eddystone, generic). This command only saves the configuration — it does not start scanning. Scanning begins in step 3.
2. **Verify the configuration.** Send `get_bleConfig` and confirm that `payload.ble.enable` is `true` and your filters were saved as expected.
3. **Start BLE scanning.** Send `start` with `scanType: ["ble"]`.
4. **Collect BLE events.** The reader publishes BLE advertisement events as it detects beacons.
5. **Stop BLE scanning.** Send `stop` with `scanType: ["ble"]`.

## Authentication

All REST endpoints require a Bearer token. Send `GET /cloud/localRestLogin` to get a token, and then include the token in each REST request:

```
Authorization: Bearer <token>
```

MQTT commands are published to the reader's command topic using the established MQTT session credentials.

## Supported beacon protocols

| Protocol | Description |
|---|---|
| **iBeacon** | Apple proximity beacon standard. Filter by UUID, major, minor, and TX power. |
| **AltBeacon** | Open beacon format. Filter by manufacturer ID, beacon ID, major, minor, and reference RSSI. |
| **Eddystone** | Google beacon format. Filter by frame type such as URL, UID, EID, or TLM, and use frame-specific fields. |
| **Generic BLE** | Standard BLE device advertisements. Filter by MAC address, address type, device name, or alias. |
