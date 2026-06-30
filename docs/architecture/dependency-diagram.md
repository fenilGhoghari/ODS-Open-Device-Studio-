# Dependency Rules

Dependencies must always flow downward.

Allowed:

Presentation
↓
Plugin Manager
↓
Service Manager
↓
Communication Layer
↓
Platform Layer
↓
Operating System

Not Allowed:

❌ UI → Operating System

❌ Plugin → QtSerialPort

❌ Plugin → SocketCAN

❌ Communication Layer → UI

❌ Services → UI

                         +----------------------+
                         |    Presentation      |
                         |  UI / QML / Widgets  |
                         +----------+-----------+
                                    |
                                    ▼
                         +----------------------+
                         |   Workspace Manager  |
                         +----------+-----------+
                                    |
                                    ▼
                         +----------------------+
                         |    Plugin Manager    |
                         +----------+-----------+
                                    |
                    +---------------+---------------+
                    |                               |
                    ▼                               ▼
          +-------------------+          +-------------------+
          |   Event Bus        |          |  Service Manager  |
          +-------------------+          +---------+---------+
                                                   |
                         +-------------------------+------------------------+
                         |                         |                        |
                         ▼                         ▼                        ▼
                +---------------+         +---------------+       +---------------+
                | Serial Service|         | MQTT Service  |       | CAN Service   |
                +-------+-------+         +-------+-------+       +-------+-------+
                        |                         |                       |
                        +-----------+-------------+-----------------------+
                                    |
                                    ▼
                        +---------------------------+
                        |  Communication Layer      |
                        | QtSerialPort / TCP / BLE |
                        +------------+--------------+
                                     |
                                     ▼
                        +---------------------------+
                        | Platform Abstraction      |
                        | Windows / Linux / macOS  |
                        +------------+--------------+
                                     |
                                     ▼
                        +---------------------------+
                        |     Operating System      |
                        +---------------------------+