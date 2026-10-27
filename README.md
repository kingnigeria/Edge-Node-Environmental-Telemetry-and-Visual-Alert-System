# Edge Node Environmental Telemetry and Visual Alert System
CS450 Project

## Section 1: Project Title, Purpose, and Scope

### Project Title
Edge Node Environmental Telemetry and Visual Alert System

### Purpose
This project develops a lightweight environmental monitoring and alerting system for industrial or enclosure-based edge computing environments. The system is designed to continuously monitor conditions such as temperature and humidity, provide visual feedback to local operators, and support remote communication through a distributed MQTT-based architecture.

The goal is to create a simple yet effective edge solution that can detect abnormal environmental conditions in real time and alert users using both local visual indicators and a user-friendly interface.

### Scope
The project focuses on monitoring environmental conditions using Raspberry Pi-based edge hardware and the Sense HAT sensor module. The system includes:
- Collection of temperature and humidity data
- Local display and status monitoring via a touchscreen interface
- MQTT-based communication between system components
- Visual alerting using the Sense HAT LED matrix
- Persistent local logging for environmental telemetry

The system is intended for use in a compact deployment environment such as an industrial server rack or enclosed equipment cabinet, where rapid monitoring and local operator awareness are important.

### Application Category
Environmental Control / Custom CPS

### Project Context
This project is implemented as a small-scale cyber-physical system that combines sensing, communication, and operator feedback in a single edge-based monitoring platform. It emphasizes low-cost hardware integration, practical system design, and reliable monitoring for constrained industrial environments.

## Section 3: Non-Functional Requirements Specification

Non-functional requirements define how the system must operate in terms of reliability, security, networking, auditability, and startup behavior.

### 3.1 GitHub Version Control
- GitHub Repository: https://github.com/kingnigeria/Edge-Node-Environmental-Telemetry-and-Visual-Alert-System
- All project files shall be stored in the shared GitHub repository.
- Development shall use `main` as the protected release branch and `dev` or short feature branches for day-to-day work.
- Both team members must commit regularly with descriptive messages.
- Direct pushes to `main` are not allowed; changes must be merged via pull request.
- At the end of each lab session, each Raspberry Pi must run `git add`, `git commit`, and `git push`.
- No project code shall remain only on SD card storage; all work must be recoverable from GitHub.

### 3.2 Unprivileged Socket Port Allocation
- All project sockets shall use unprivileged ports in the range 1025–65535.
- Assigned ports:
  - 5001, 5002, 5003, 5004, 5005 for application services
  - 1883 for Mosquitto
- No project service shall bind to a privileged port below 1024.
- Port numbers shall be defined as fixed constants in configuration files and documented in the README.
- Services shall run as the normal `pi` user; no root privileges are required.

### 3.3 Network Interface Management
- The project shall not modify default routes, IP configuration, netplan settings, or NetworkManager settings.
- Services shall bind explicitly to the Raspberry Pi’s eth0 address and shall not use `0.0.0.0`.
- wlan0 shall remain unused unless explicitly required for backup management.
- No interface bridging or route changes shall be introduced that would disrupt SSH access or classroom network operation.

### 3.4 Classroom LAN Confinement
- All traffic shall remain within the classroom LAN subnet `192.168.5.0/24`.
- Communication shall be limited to the project nodes at `192.168.5.72` and `192.168.5.73`.
- The system shall not broadcast, port-scan, or probe outside the project subnet.

### 3.5 Live Linux CLI Auditability
- The final demonstration shall verify running services using standard Linux networking tools.
- Required verification commands:
  ```bash
  sudo ss -tulpn | grep -E ":(5001|5002|5003|5004|5005|1883)\b"
  sudo lsof -nP -i :5001,5002,5003,5004,5005,1883
  ip -br addr
  ip route show
  ping -c 3 192.168.5.73
  ethtool eth0
  sudo tcpdump -i eth0 -n "udp port 5002"
