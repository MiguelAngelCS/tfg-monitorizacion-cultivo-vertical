# Notas de extracción de papers — v0.1 (datos concretos ya verificados)

> Solo aparece aquí lo que se ha leído realmente del paper (texto completo o abstract oficial).
> Formato: dato + página/sección + uso previsto en el TFG.

## 1. Ceccanti et al. (2026) — Benchmark de viabilidad de VF (Energy Conversion and Management; arXiv:2507.18419)
- Análisis de **162 escenarios** combinando temperatura, densidad de flujo fotónico (PPFD) y CO₂ en 3 localidades (Trondheim, Shanghái, Dubai).
- **La iluminación (PPFD) es el factor dominante del crecimiento (correlación 0,85) y el principal motor del consumo energético (correlación 0,73).** El HVAC + deshumidificación mantienen la productividad óptima con independencia del clima externo.
- Consumo específico mínimo: 55 kg/m² (coincide con la menor productividad).
- Configuración más rentable: 24 °C, 250 µmol/m²·s, 1400 ppm CO₂, con aislamiento → 102 kg/m².
- Conclusión: solo sistemas energéticos descarbonizados hacen sostenible la VF frente a lechuga importada.
- **Uso en TFG:** justificar en cap. 1 que la iluminación domina el consumo y que medirla por separado es prioritaria → nuestro sistema de medición por circuitos.

## 2. Dhaou (2023) — Smart meter + smart plug HEMS (Electronics 12(19):4041) — LEÍDO COMPLETO
- Arquitectura fog computing: smart plugs (Arduino) → Zigbee → smart meter (Raspberry Pi) con TinyML para identificación de cargas.
- El smart plug mide: Irms, Vrms, frecuencia, factor de potencia, P, Q, S.
- **Precisión smart plug >99 %, smart meter >97 %** (frente a medidas de laboratorio).
- Distinción clave: **ILM (medida intrusiva, un medidor por carga) vs NILM (un medidor + desagregación por algoritmos)** → nuestro enfoque por tomas (Shelly) es ILM comercial de bajo coste; citable como justificación.
- En RPi 3B, inferencia de árbol de decisión: 1,59 µs; reducción de reloj a 600 MHz para ahorrar energía.
- TOU demand-response: ahorro ~30 % en factura en el caso de estudio.
- **Uso en TFG:** cap. 2 (estado del arte smart plugs), cap. 3 (justificación de magnitudes medidas y clase de precisión), posible apartado de precisión/validación de nuestros sensores.

## 3. Jara Ochoa et al. (2023) — MQTT vs HTTP (Sensors 23(10):4896) — ABSTRACT
- Comparativa de consumo energético MQTT vs HTTP en plataforma IoT de monitorización en tiempo real (NodeMCU).
- Confirma cuantitativamente el menor consumo de MQTT (pub/sub) frente a HTTP.
- **Uso en TFG:** justificación de MQTT como protocolo de transporte en cap. 3/4.

## Pendiente de lectura (próxima iteración)
- [ ] Miserocchi & Franco (2025) — cifras de consumo específico por cultivo (kWh/kg) **[PRIORIDAD 1 — es la cifra estrella del cap. 1]**
- [ ] Kaiser et al. (2024) — optimización dinámica según coste de energía
- [ ] Keyvan & Roshandel (2024) — modelo horario iluminación/refrigeración
- [ ] Tekler et al. (2022) — plug loads en edificios (Building and Environment, acceso por suscripción)
- [ ] Suhaimey et al. (2025) — arquitectura MQTT+RPi real (IEEE, acceso por suscripción)

> Nota: Elsevier/IEEE/IOP bloquean la descarga directa. Para esos: abstract + ResearchGate / repositorios institucionales, o lectura en universidad (acceso UCA a ScienceDirect/IEEE Xplore).
