# Interfaces

## Overview

Open Device Studio uses interface-driven architecture to ensure plugins remain independent from concrete implementations.

Plugins never communicate directly with hardware or protocol libraries. Instead, they interact through abstract interfaces provided by the Core.

---

# Architecture

```text
Plugin
   │
   ▼
Interface
   │
   ▼
Service
   │
   ▼
Communication Layer
   │
   ▼
Operating System
```

---

# Why Interfaces?

Interfaces provide:

- Loose coupling
- Easy testing
- Better maintainability
- Cross-platform support
- Ability to replace implementations without changing plugins

---

# Example

+----------------------+
|   Serial Plugin      |
+----------+-----------+
           |
           v
+----------------------+
|  ISerialService      |
+----------+-----------+
           |
           v
+----------------------+
| QtSerialService      |
+----------+-----------+
           |
           v
+----------------------+
| QtSerialPort         |
+----------+-----------+
           |
           v
+----------------------+
| Operating System     |
+----------------------+

---

# Core Interfaces

## IPlugin

Responsible for plugin lifecycle.

Responsibilities

- Initialize plugin
- Shutdown plugin
- Register services
- Provide metadata

---

## ISerialService

Responsible for serial communication.

Responsibilities

- Connect
- Disconnect
- Read
- Write
- Configure port

---

## IMqttService

Responsible for MQTT communication.

Responsibilities

- Connect
- Subscribe
- Publish
- Disconnect

---

## ICanService

Responsible for CAN communication.

Responsibilities

- Open interface
- Send frame
- Receive frame
- Apply filters

---

## ISettingsService

Responsible for application settings.

Responsibilities

- Read settings
- Write settings
- Save workspace

---

## ILoggingService

Responsible for logging.

Responsibilities

- Info
- Warning
- Error
- Debug

---

# Dependency Rule

Plugins must depend only on interfaces.

Plugins must never depend on:

- QtSerialPort
- SocketCAN
- MQTT Library
- Platform-specific APIs

---

# Future Interfaces

- IBluetoothService
- IFirmwareService
- IDeviceService
- IWorkspaceService
- INotificationService
- IThemeService