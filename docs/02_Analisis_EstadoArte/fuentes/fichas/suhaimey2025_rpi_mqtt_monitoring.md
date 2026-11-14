# Suhaimey et al. (2025) — Sistema IoT de monitorización energética con MQTT y Raspberry Pi

- **Tipo:** ponencia de congreso (9th IET Smart Cities Symposium, SCS 2025), indexada en IEEE Xplore.
- **PDF local:** `papers/suhaimey2025_rpi_mqtt_monitoring.pdf` (repo de trabajo).
- **Referencia (borrador):** Suhaimey, M. Z.; Muhamad Amin, M. R. R.; Abd Ghaffar, A. N. (2025). Real-Time IoT-Based Energy Monitoring System for Residential Applications. *9th IET Smart Cities Symposium (SCS 2025)*, Bahréin. IET. https://doi.org/10.1049/icp.2026.2504

## Qué aporta
- **Validación de la arquitectura que usamos**: nodos de medida → MQTT → Raspberry Pi → dashboard open source.
- Sistema real de monitorización energética por circuitos: ESP32 + PZEM-004T + pinzas CT de diseño propio (PCB y carcasa 3D), comunicación MQTT y visualización en Home Assistant.

## Datos clave
- La **Raspberry Pi 5 es el hub central**: aloja el broker Mosquitto (MQTT) y Home Assistant (secciones 3.2–3.3 del paper).
- Granularidad por circuito, integración open source, modularidad y bajo coste.
- El firmware Tasmota de los nodos incluye reconexión automática ante cortes de red (continuidad de datos).

## Dónde usarlo
- **Cap. 1 (estado del arte):** sistemas IoT de monitorización energética de desarrollo propio.
- **Cap. 3 (definición del sistema):** validación del stack MQTT + RPi + visualización open source elegido.
