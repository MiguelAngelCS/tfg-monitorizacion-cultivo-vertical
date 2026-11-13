# Estado del arte — v0.1 (borrador de trabajo)

> Documento vivo. Las referencias proceden del buscador académico (sesión 2026-10-31); cada CSV
> completo está en `fuentes/`. Las entradas marcadas con ★ son las prioridades de lectura.
> Regla: nada de esto va al TFG hasta leer el paper completo y extraer el dato concreto.

## Tema 1 — Consumo energético en agricultura vertical (justificación del TFG)

Mensaje clave de la literatura: **la iluminación artificial y la climatización dominan el consumo**
de las plantas de cultivo vertical, y la viabilidad económica depende de medir y optimizar ese consumo.

- ★ Miserocchi & Franco (2025), *Benchmarking energy efficiency in vertical farming: Status and prospects*, Thermal Science and Engineering Progress. — Revisión del consumo específico de energía (kWh/kg) en VF. Citas: 67.
- ★ Kaiser et al. (2024), *Vertical farming goes dynamic: optimizing resource use efficiency, product quality, and energy costs*, Frontiers in Science. — 163 citas; optimización dinámica según coste de energía.
- ★ Keyvan & Roshandel (2024), *An integrated energy-yield-cost model to evaluate clean energy solutions for vertical farms*, Computers and Electronics in Agriculture. — Modelo horario de demanda: iluminación, refrigeración.
- Ceccanti et al. (2026), *Beyond yield: integrating energy, water, cost, and carbon to benchmark indoor vertical farming viability*, Energy Conversion and Management. — Benchmark multidimensional con arXiv abierto.
- Kalantari et al. (2018), *Opportunities and challenges in sustainability of vertical farming: A review*, J. of Landscape Ecology. — Clásico (621 citas); coste energético como barrera de la VF.
- Arcasi et al. (2023), *Assessment of the energy consumption of indoor farming for different climates and lighting system intensity*, J. Physics: Conf. Series. — PDF abierto.
- Aborujilah (2025), *Towards sustainable vertical farming: A systematic review of energy return on investment*, Sustainability (MDPI, abierto).

**Hipótesis de trabajo para nuestro caso:** en una planta piloto pequeña (bandejas, sala de laboratorio)
esperamos perfil de carga dominado por LED + ventilación/clima; la medición por circuitos/equipos
permitirá descomponer el consumo — exactamente lo que pide el tutor para estudiar viabilidad.

## Tema 2 — Monitorización de cargas mediante enchufes inteligentes (smart plugs)

Base técnica de usar sensores tipo Shelly en tomas: hay literatura sólida sobre smart plugs
para medida y gestión de cargas en edificios.

- ★ Tekler et al. (2022), *Plug-Mate: An IoT-based occupancy-driven plug load management system in smart buildings*, Building and Environment. — 166 citas; gestión de cargas enchufables en edificios inteligentes.
- ★ Dhaou (2023), *Design and implementation of an internet-of-things-enabled smart meter and smart plug for home-energy-management system*, Electronics (MDPI, abierto). — Distingue medida intrusiva (por carga) vs NILM.
- Suryadevara & Biswal (2019), *Smart plugs: Paradigms and applications in the smart city-and-smart grid*, Energies (MDPI, abierto). — Revisión de paradigmas smart plug.
- Lee & Yang (2017), *An intelligent power monitoring and analysis system for distributed smart plugs sensor networks*, Int. J. Distributed Sensor Networks (PDF abierto). — Arquitectura gateway + red de smart plugs (análogo a nuestra Raspberry Pi + Shellys).
- Oh (2020), *IoT-based smart plug for residential energy conservation: An empirical study based on 15 months' monitoring*, Energies. — Valida medida a largo plazo con smart plugs.
- Yeboah et al. (2026), *Development of an IoT-enabled smart plug for intelligent energy monitoring*, J. of Electrical Engineering & Technology (PDF abierto).

**Nota:** la literatura usa smart plugs mayoritariamente para hogar/edificios; la aplicación a
*descomposición de consumos de una planta de cultivo vertical* es el ángulo original de este TFG
(junto con la viabilidad energética). Esto refuerza la contribución académica del trabajo.

## Tema 3 — Arquitectura IoT de bajo coste: MQTT + Raspberry Pi + visualización open source

- ★ Suhaimey et al. (2025), *Real-time IoT-based energy monitoring system for residential applications*, IET Smart Cities Conference. — Publica métricas a MQTT broker alojado en Raspberry Pi: arquitectura tipo la nuestra.
- ★ Jara Ochoa et al. (2023), *Analysis of power consumption between MQTT and HTTP protocols in an IoT platform for remote real-time monitoring*, Sensors (MDPI, abierto). — Justifica MQTT vs HTTP (ahorro energético).
- Kumar & Jasuja (2017), *Air quality monitoring system based on IoT using Raspberry Pi*, IEEE conf. — Node-RED + MQTT en RPi (339 citas).
- Baig et al. (2022), *A low-cost, open-source peer-to-peer energy trading system ... using IoT, blockchain and HTTP*, Energies. — Servidor en Raspberry Pi, bajo coste.
- Arigela et al. (2024), *Remote based home automation with MQTT: ESP32 nodes and Node-RED on Raspberry Pi*, IEEE I-SMAC. — Stack muy cercano al candidato (ESP32/Shelly → MQTT → Node-RED/Grafana en RPi).

**Pila técnica candidata (a justificar en Cap. 3):** Shelly (medida por toma) → MQTT → Raspberry Pi
(broker + ingesta en Python) → base de datos (InfluxDB o PostgreSQL/TimescaleDB) → Grafana.
Toda la cadena es open source y replicable en el GitHub del TFG.

## Tema 4 — Monitorización ambiental en cultivo vertical (ampliación futura)

Para la fase 2 (si el tutor la pide): sensores T/HR/CO₂/luz en VF e hidroponía.

- Kaur et al. (2023), *Comparative analysis of IoT-based controlled environment ... for hydroponic indoor vertical farm*, Environmental Research (94 citas).
- Dutta et al. (2023), *Evaluation of growth responses of lettuce and energy efficiency of ... smart hydroponics cropping system*, Sensors (106 citas).
- Nikolov et al. (2023), *Design of a small-scale hydroponic system for indoor farming of leafy vegetables*, Agriculture (MDPI, abierto) — pequeña escala, como nuestra planta piloto.
- Dávila et al. (2026), *Automated system with ESP32 for monitoring vertical hydroponic farming and air quality*, EEI (PDF abierto).

## Referencias seleccionadas (borrador, formato a normalizar con norma UNE/ISO 690)

1. Miserocchi, L.; Franco, A. (2025). Benchmarking energy efficiency in vertical farming: Status and prospects. *Thermal Science and Engineering Progress*. https://www.sciencedirect.com/science/article/pii/S2451904924007832
2. Kaiser, E.; Kusuma, P.; Vialet-Chabrand, S.; Folta, K. et al. (2024). Vertical farming goes dynamic... *Frontiers in Science*. https://www.frontiersin.org/journals/science/articles/10.3389/fsci.2024.1411259/full
3. Keyvan, P.; Roshandel, R. (2024). An integrated energy-yield-cost model to evaluate clean energy solutions for vertical farms. *Computers and Electronics in Agriculture*. https://www.sciencedirect.com/science/article/pii/S016816992400200X
4. Ceccanti, F.; Bischi, A.; Desideri, U.; Baccioli, A. (2026). Beyond yield... *Energy Conversion and Management*. arXiv: https://arxiv.org/pdf/2507.18419
5. Kalantari, F.; Tahir, O. M.; Joni, R. A.; Syed Zakaria, S. Z. F. (2018). Opportunities and challenges in sustainability of vertical farming: A review. *Journal of Landscape Ecology*.
6. Tekler, Z. D.; Low, R.; Yuen, C.; Blessing, L. (2022). Plug-Mate... *Building and Environment*. https://www.sciencedirect.com/science/article/pii/S036013232200703X
7. Dhaou, I. B. (2023). Design and implementation of an internet-of-things-enabled smart meter and smart plug for home-energy-management system. *Electronics*, 12(19), 4041. https://www.mdpi.com/2079-9292/12/19/4041
8. Suryadevara, N. K.; Biswal, G. R. (2019). Smart plugs: Paradigms and applications in the smart city-and-smart grid. *Energies*, 12(10), 1957. https://www.mdpi.com/1996-1073/12/10/1957
9. Lee, S. H.; Yang, C. S. (2017). An intelligent power monitoring and analysis system for distributed smart plugs sensor networks. *Int. J. Distributed Sensor Networks*.
10. Jara Ochoa, H. J. et al. (2023). Analysis of power consumption between MQTT and HTTP protocols... *Sensors*, 23(10), 4896. https://www.mdpi.com/1424-8220/23/10/4896
11. Suhaimey, M. Z. et al. (2025). Real-time IoT-based energy monitoring system for residential applications. *IET Smart Cities Conference*.
12. Kaur, G.; Upadhyaya, P.; Chawla, P. (2023). Comparative analysis of IoT-based controlled environment... *Environmental Research*. https://www.sciencedirect.com/science/article/pii/S0013935123001056
13. Nikolov, N. V. et al. (2023). Design of a small-scale hydroponic system for indoor farming of leafy vegetables. *Agriculture*, 13(6), 1191. https://www.mdpi.com/2077-0472/13/6/1191

## Próximos pasos (estado del arte)
- [ ] Leer (al menos abstract + conclusiones + datos clave) los 5 marcados con ★
- [ ] Extraer cifras concretas: % iluminación sobre consumo total, kWh/kg lechuga, etc.
- [ ] Buscar 2-3 referencias normativas: UNE 157001 (estructura), REBT (intalación eléctrica), y medida de energía (IEC 62053 / clase de contadores de los Shelly)
- [ ] Añadir línea sobre monitorización energética en invernaderos/agricultura (término "greenhouse energy monitoring") para reforzar el estado del arte aplicado
