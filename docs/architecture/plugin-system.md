# Plugin System

## Overview

Open Device Studio uses a plugin-based architecture. Every major feature, such as the Serial Terminal, MQTT Explorer, BLE Scanner, or CAN Analyzer, is implemented as a plugin.

The core application is responsible only for loading, managing, and communicating with plugins.

---

# Plugin Lifecycle

Application Start

↓

Load Plugin Folder

↓

Find Plugins

↓

Read Metadata

↓

Load Library

↓

Create Plugin Instance

↓

Initialize Plugin

↓

Register Services

↓

Plugin Ready

↓

Running

↓

Shutdown

↓

Unload Plugin

---

# Plugin Discovery

The application scans the `plugins/` directory on startup.

Example:

plugins/
├── serial-terminal/
├── mqtt-explorer/
├── ble-scanner/
└── can-analyzer/

Each plugin contains:

- Shared Library (.dll / .so / .dylib)
- plugin.json
- Resources

---

# Plugin Metadata

Every plugin must provide a metadata file.

Example:

{
    "id": "serial-terminal",
    "name": "Serial Terminal",
    "version": "1.0.0",
    "author": "Open Device Studio",
    "description": "Serial communication terminal",
    "dependencies": []
}

---

# Plugin Interface

Every plugin must implement the IPlugin interface.

Responsibilities

- initialize()
- shutdown()
- name()
- version()

---

# Plugin Communication

Plugins never communicate directly with each other.

Communication flow:

Plugin

↓

Event Bus

↓

Service Manager

↓

Other Plugins

---

# Dependency Rules

Plugins may depend on:

✔ Plugin SDK

✔ Interfaces

✔ Core Services

Plugins must NOT depend on:

❌ QtSerialPort

❌ SocketCAN

❌ BLE Libraries

❌ Operating System APIs

---

# Plugin States

Discovered

↓

Loaded

↓

Initialized

↓

Running

↓

Stopped

↓

Unloaded


---

# Plugins interact

                   +------------------+
                   | Plugin Manager   |
                   +--------+---------+
                            |
            +---------------+---------------+
            |               |               |
            ▼               ▼               ▼
     Serial Plugin    MQTT Plugin    BLE Plugin
            |               |               |
            +---------------+---------------+
                            |
                            ▼
                      Event Bus
                            |
                            ▼
                     Service Manager

---

# Future Support

The plugin system is designed to support:

- Hot Loading
- Hot Unloading
- Plugin Marketplace
- Third-party Plugins
- Version Compatibility
- Digital Signatures