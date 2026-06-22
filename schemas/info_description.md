MQTT and REST API for configuring and controlling Bluetooth Low Energy (BLE) scanning on the Zebra FXR90 fixed RFID reader.

## Overview

The FXR90 reader supports passive BLE advertisement scanning alongside RFID inventory. Configure BLE first, verify the saved configuration, and then start scanning when the reader is ready to collect BLE advertisements.

## REST workflow

Use REST when you integrate directly with the reader over HTTPS.

1. **Configure BLE scanning.** Send `PUT /cloud/ble-config` with `ble.enable` set to `true`. This request saves the BLE configuration. It does not start scanning.
2. **Verify the configuration.** Send `GET /cloud/ble-config` and confirm that `ble.enable` is `true`.
3. **Start BLE scanning.** Send `PUT /cloud/start` with `scanType: ["ble"]`.
4. **Collect BLE events.** The reader publishes BLE advertisement events as it detects beacons.
5. **Stop BLE scanning.** Send `PUT /cloud/stop` with `scanType: ["ble"]`.

## MQTT workflow

Use MQTT when you send commands through the reader's command topic.

1. **Configure BLE scanning.** Send `set_bleConfig` with `payload.ble.enable` set to `true`. This command saves the BLE configuration. It does not start scanning.
2. **Verify the configuration.** Send `get_bleConfig` and confirm that `payload.ble.enable` is `true`.
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
