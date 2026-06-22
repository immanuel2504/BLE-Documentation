# BLE API Reference Documentation

MQTT and REST API documentation for Bluetooth Low Energy (BLE) scanning on the Zebra FXR90 fixed RFID reader.

## Overview

The FXR90 reader supports passive BLE advertisement scanning alongside RFID inventory. Four beacon protocols are supported: **iBeacon**, **AltBeacon**, **Eddystone** (URL, UID, EID, TLM), and **generic BLE** devices.

## Operations

| Operation | REST | MQTT | Description |
|---|---|---|---|
| getBleConfig | `GET /cloud/ble-config` | `get_bleConfig` | Retrieve current BLE scanner configuration |
| setBleConfig | `PUT /cloud/ble-config` | `set_bleConfig` | Configure the BLE scanner |
| start | `PUT /cloud/start` | `start` | Start BLE scanning |
| stop | `PUT /cloud/stop` | `stop` | Stop BLE scanning |

## Project Structure

```
BLE-Documentation/
├── docs/
│   ├── rest_openapi.yaml       REST OpenAPI 3.0 specification
│   ├── openapi_md.json         Generated MQTT/viewer spec (run scripts to build)
│   └── rest_artifacts.json     Bundled REST artifacts (run scripts to build)
├── rest api/
│   ├── getBleConfig/           REST request/response schemas and examples
│   ├── setBleConfig/
│   ├── start/
│   └── stop/
├── schemas/
│   ├── commands/               MQTT command schemas (with x-tag for viewer)
│   │   ├── ble/                  get_bleConfig, set_bleConfig
│   │   └── control/              start, stop
│   ├── response/               MQTT response schemas
│   │   ├── ble/
│   │   └── control/
│   ├── operation_descriptions/ Markdown descriptions (used by viewer)
│   ├── tag_descriptions/       Tag/group descriptions for the viewer sidebar
│   ├── error_codes.json        Error code reference
│   ├── tag_config.json         Operation grouping and ordering
│   └── info_description.md     API overview shown in the viewer
└── scripts/
    ├── bundle_rest_artifacts.py        Bundle rest api/ JSON into docs/rest_artifacts.json
    └── generate_openapi_tags_md.py     Generate docs/openapi_md.json from schemas/
```

## Build

Run from the project root after editing any source file:

```bash
python scripts/bundle_rest_artifacts.py
python scripts/generate_openapi_tags_md.py
```

The `rest api/` and `schemas/` directories are the single source of truth. The files in `docs/` are generated outputs.

## Workflow

1. **Configure BLE scanning** — Turn on the BLE scanner in the reader configuration by sending `PUT /cloud/ble-config` with `{ "ble": { "enable": true } }`. This step saves the configuration. It doesn't start scanning.
2. **Start** — `PUT /cloud/start` with `{ "scanType": ["ble"] }`.
3. **Collect** — BLE tag data events are published as advertisements are detected.
4. **Stop** — `PUT /cloud/stop` with `{ "scanType": ["ble"] }`.
5. **Verify** — `GET /cloud/ble-config` at any time to inspect the current configuration.
