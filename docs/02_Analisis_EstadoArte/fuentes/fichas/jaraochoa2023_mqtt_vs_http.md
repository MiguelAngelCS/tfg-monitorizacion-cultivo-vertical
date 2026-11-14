# Jara Ochoa et al. (2023) — Consumo energético: MQTT vs HTTP

- **Tipo:** artículo de revista, revisado por pares.
- **PDF local:** `papers/jaraochoa2023_mqtt_vs_http.pdf` (repo de trabajo).
- **Referencia (borrador):** Jara Ochoa, H. J.; Peña, R.; Ledo Mezquita, Y.; Gonzalez, E.; Camacho-Leon, S. (2023). Comparative Analysis of Power Consumption between MQTT and HTTP Protocols in an IoT Platform Designed and Implemented for Remote Real-Time Monitoring of Long-Term Cold Chain Transport Operations. *Sensors*, 23(10), 4896. https://doi.org/10.3390/s23104896

## Qué aporta
- **Justificación cuantitativa de elegir MQTT** frente a HTTP en el transporte de datos del sistema.
- Plataforma IoT real (NodeMCU) con pruebas de larga duración y distintos niveles de QoS.

## Datos clave
- MQTT **QoS 0** ahorra un **6.03 %** de energía y **QoS 1** un **8.33 %** frente a HTTP.
- El ahorro se traduce en muchas horas extra de autonomía de batería en dispositivos IoT.

## Dónde usarlo
- **Cap. 4 (diseño de red y comunicaciones):** argumento técnico para MQTT como protocolo de transporte.
