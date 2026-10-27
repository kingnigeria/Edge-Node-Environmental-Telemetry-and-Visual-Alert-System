# Edge-Node-Environmental-Telemetry-and-Visual-Alert-System
CS450 Project

Official Project Title: Edge Node Environmental Telemetry and Visual Alert System

Application Category (Ex: Industrial Telemetry, Environmental Control, Security Monitor, Custom CPS): Environmental Control / Custom CPS

Project Purpose Statement:
This project implements a lightweight edge monitoring and remote alerting system designed for industrial server racks or equipment enclosures. The Sense HAT edge node continuously samples ambient temperature, humidity, and physical joystick inputs, transmitting telemetry across the local LAN to an HMI monitoring station. The HMI console visualizes live sensor metrics on a touchscreen display and allows an operator to send manual or threshold-driven alarm signals back to the edge node's LED matrix. Persistent telemetry records are logged directly to a Dockerized MQTT broker. This system provides real-time situational awareness and physical alerting while maintaining network hygiene and auditability across distributed nodes.

•	HMI Pi Role (Services hosted, UI role, data processing): Hosts a Tkinter touchscreen GUI for displaying live metrics, runs a Dockerized Mosquitto MQTT broker for persistent data logging, and issues alert commands to the edge Pi.

•	Sense HAT Pi Role (Sensors/actuators polled, daemons hosted): Polls onboard temperature and humidity sensors, reads the hardware joystick, updates its 8x8 LED matrix based on received commands, and runs client socket scripts

•	Remote Storage / Infrastructure Role (NAS Database, MQTT Broker, or SFTP/SCP Server): Dockerized Mosquitto MQTT broker running on unprivileged port 1883 with local file persistence

•	Optional Additional Nodes (Other Sandbox Table Pis or PLCs—note table consultation if applicable): None (strictly confined to Table 7 hardware)

•	Out-of-Scope Boundaries (List 1–2 features your team is intentionally excluding to ensure completion by Week 15): Hardware fan/relay control and cloud database integration are excluded to guarantee delivery by Week 15.
