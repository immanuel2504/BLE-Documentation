This document describes the BLE API for the Zebra FXR90 fixed RFID reader. Use this reference to configure BLE advertisement scanning, view the current configuration, start or stop scanning, and monitor BLE scan status through REST or MQTT.

## Overview

Bluetooth Low Energy (BLE) devices broadcast short advertisement packets that can identify nearby devices, beacons, tags, or sensors. The FXR90 reader can scan for these BLE advertisements and report detected beacon data while supporting RFID inventory workflows.

BLE scanning on the FXR90 is controlled by the BLE configuration stored on the reader. The configuration enables or disables BLE scanning and defines optional filters that determine which advertisements are reported. Filters can apply across all BLE advertisements, such as RSSI and service UUID filters, or to specific beacon protocols.

## Supported beacon protocols

| Protocol | Description |
|---|---|
| **iBeacon** | Apple proximity beacon format. Filter by UUID, major, minor, and TX power. |
| **AltBeacon** | Open beacon format. Filter by manufacturer ID, beacon ID, major, minor, and reference RSSI. |
| **Eddystone** | Google beacon format. Filter by frame type, including URL, UID, EID, and TLM. |
| **Generic BLE** | Standard BLE advertisements. Filter by MAC address, address type, device name, or alias. |

## Interfaces

The FXR90 reader supports both REST and MQTT for BLE control.

| Interface | Use when | Command style |
|---|---|---|
| **REST** | Your application communicates directly with the reader over HTTPS. | Send HTTP requests to `/cloud/...` endpoints. |
| **MQTT** | Your application controls the reader through the configured MQTT command topic. | Publish command messages such as `set_bleConfig`, `start`, and `stop`. |

## REST workflow

Use this workflow when you manage BLE scanning through HTTPS requests.

1. **Get an access token:** Send `GET /cloud/localRestLogin`, and then include the returned token in the `Authorization` header for each REST request.
2. **Save BLE configuration:** Send `PUT /cloud/ble-config` with `ble.enable` set to `true`. Include optional scan interval, RSSI filters, service UUID filters, or protocol-specific filters as needed.
3. **View the current configuration:** Send `GET /cloud/ble-config` and confirm that `ble.enable` is `true`.
4. **Start BLE scanning:** Send `PUT /cloud/start` with `scanType: ["ble"]`.
5. **Monitor scanning:** Send `GET /cloud/status` to confirm that `ble.scanState` is `running` and to review BLE advertisement counts.
6. **Stop BLE scanning:** Send `PUT /cloud/stop` with `scanType: ["ble"]`.

## MQTT workflow

Use this workflow when you manage BLE scanning through the reader's MQTT command topic.

1. **Save BLE configuration:** Publish `set_bleConfig` with `payload.ble.enable` set to `true`. Include optional scan interval, RSSI filters, service UUID filters, or protocol-specific filters as needed.
2. **View the current configuration:** Publish `get_bleConfig` and confirm that `payload.ble.enable` is `true`.
3. **Start BLE scanning:** Publish `start` with `scanType: ["ble"]`.
4. **Monitor scanning:** Publish `get_status` to confirm that `payload.ble.scanState` is `running` and to review BLE advertisement counts.
5. **Stop BLE scanning:** Publish `stop` with `scanType: ["ble"]`.
