# Dhaou (2023) — Smart meter y smart plug IoT para gestión energética en el hogar

- **Tipo:** artículo de revista, revisado por pares.
- **PDF local:** `papers/dhaou2023_smart_meter_plug_iot.pdf` (repo de trabajo).
- **Referencia (borrador):** Dhaou, I. B. (2023). Design and Implementation of an Internet-of-Things-Enabled Smart Meter and Smart Plug for Home-Energy-Management System. *Electronics*, 12(19), 4041. https://doi.org/10.3390/electronics12194041

## Qué aporta
- Arquitectura de medida **DIY con Raspberry Pi**: el smart plug (Arduino) mide RMS de corriente, frecuencia, factor de potencia y potencia activa/react; envía por Zigbee al smart meter, que ejecuta TinyML para identificar electrodomésticos.
- Alternativa de desarrollo propio frente a los smart plugs comerciales (Shelly, etc.).

## Datos clave
- Precisión: **>99 %** en el smart plug y **>97 %** en el smart meter (frente a medida de laboratorio).
- El smart meter es una **Raspberry Pi 3 Model B** (600 MHz); inferencia del árbol de decisión en 1.59 μs.
- Programa de demand response por horas: reduce el coste de potencia ≈ **30 %**.

## Dónde usarlo
- **Cap. 1 (estado del arte):** trabajos de medida energética con RPi y smart plugs DIY.
- **Cap. 3 (definición del sistema):** comparativa de opciones de medida (DIY vs comercial) en la justificación de tecnologías.
