# Capítulo 1 — Antecedentes y objeto del proyecto

> Borrador v0.1 (noviembre 2026). Estructura según UNE 157001. Las referencias están
> en formato de trabajo y se normalizarán a UNE-ISO 690 en la versión final.

## 1.1 Antecedentes

El cultivo vertical —la producción de alimentos en capas apiladas, en interior y
con iluminación artificial— ha ganado protagonismo en los últimos años como una de
las vías para producir alimentos de forma local y controlada, con independencia del
clima exterior y del suelo disponible. La literatura es abundante en oportunidades:
mayor productividad por unidad de superficie, uso eficiente del agua, eliminación
prácticamente total de plaguicidas y aprovechamiento de espacios urbanos infrautilizados
[1]. No obstante, la misma literatura señala de forma reiterada un freno: la energía.
En una instalación de este tipo la luz artificial sustituye al sol, el aire se renueva
con ventilación forzada y el agua circula mediante bombas y sistemas de riego
controlado, todo ello a costa de electricidad.

Las cifras lo confirman. En un estudio de benchmarking reciente sobre la eficiencia
energética del cultivo vertical, Miserocchi y Franco sitúan el consumo específico
actual de la lechuga en el rango de 10 a 18 kWh/kg, con una intensidad de uso de
850 a 1150 kWh/m²·año, y estiman que un benchmark técnico realista se encuentra
entre 3,1 y 7,4 kWh/kg [2]. La energía supone en torno al 90 % de la huella de
carbono del producto. Por su parte, Keyvan y Roshandel, mediante un modelo horario
integrado energía–rendimiento–coste aplicado a un contenedor de cultivo en Teherán,
obtienen un consumo de 11,34 kWh/kg de lechuga y un coste unitario de 3,78 $/kg,
distribuido en un 78 % para iluminación y un 19 % para deshumidificación [3]. En
la misma línea, Ceccanti et al., a partir de 162 escenarios de simulación, muestran
que el consumo específico puede oscilar entre 5,05 y 23,8 kWh/kg según la
configuración, y que la densidad de flujo fotosintético (PPFD) es el factor dominante,
con correlaciones de 0,85 con la productividad y 0,73 con el consumo energético [4].

Estos trabajos comparten una consecuencia práctica: es imposible gestionar la energía
de un cultivo vertical sin medirla. Y no basta con una lectura mensual de un contador
general, porque los perfiles de consumo de las cargas son muy distintos entre sí —la
iluminación sigue ciclos diarios estrictos, mientras que bombas y sistemas de clima
varían según consignas y condiciones— y porque la resolución temporal importa: los
modelos de referencia trabajan con paso horario [3]. La monitorización por cargas
individuales, a nivel de enchufe, es además una línea consolidada en la gestión
energética de edificios: Tekler et al. demuestran en un estudio de campo de cinco
meses en una oficina universitaria que los plug loads pueden alcanzar el 30–50 % del
consumo en edificios eficientes, y que su gestión automática permite ahorros medios
del 51,7 % en los equipos controlados [5].

La tecnología para hacerlo existe y es asequible. Los smart plugs comerciales
permiten medir potencia activa, factor de potencia y energía acumulada de cada
equipo conectado, y su precisión está validada: Dhaou reporta precisiones superiores
al 99 % frente a medida de laboratorio en un smart plug de desarrollo propio [6].
Para instalaciones donde no se puede interrumpir el cableado —como es el caso de
una sala alimentada exclusivamente por tomas de corriente—, la medida no invasiva
por pinzas amperimétricas es una alternativa igualmente validada, como demuestran
Suhaimey et al. con su sistema de nodos ESP32 + PZEM-004T y pinzas CT [7]. En cuanto
al transporte de datos, los protocolos de mensajería ligera están justificados
cuantitativamente: Jara Ochoa et al. miden un ahorro del 6,03 % (QoS 0) y del 8,33 %
(QoS 1) de MQTT frente a HTTP en plataformas de monitorización [8].

En este contexto se sitúa el presente proyecto. La Escuela Superior de Ingeniería
de la Universidad de Cádiz dispone de una sala piloto de cultivo vertical de
aproximadamente 10 × 15 m, alimentada íntegramente mediante tomas Schuko de
pared, con equipamiento en crecimiento (bomba de riego con fuente de alimentación,
luces de germinación, y luces de crecimiento y una segunda bomba previstas). No
existe instalación de medida alguna: no hay contadores secundarios ni posibilidad
de actuar sobre el cuadro eléctrico, por lo que la única vía de medición disponible
es la de enchufe. A día de hoy, el consumo de la sala es una incógnita, y sin
medirlo no puede abordarse ninguna mejora energética con rigor.

## 1.2 Objetivos

El objetivo general del proyecto es:

> Diseñar, implementar y validar un sistema de monitorización energética de bajo
> coste para la sala piloto de cultivo vertical de la ESI, que proporcione medidas
> fiables y permanentes de las cargas eléctricas presentes y futuras.

A partir de él, se definen los siguientes objetivos específicos:

1. Analizar el estado del arte en monitorización energética aplicada al cultivo
   vertical y a los plug loads, identificando tecnologías de medida, protocolos
   de comunicación y arquitecturas de referencia.
2. Definir la arquitectura del sistema: sensores de medida, datalogger, base de
   datos temporal y visualización, justificando cada decisión técnica.
3. Desarrollar el software de adquisición, almacenamiento y visualización de datos
   como proyecto de código abierto.
4. Desplegar el sistema en la sala piloto y verificar la calidad de las medidas
   (continuidad, razonabilidad y resolución temporal).
5. Caracterizar el consumo real de las cargas instaladas como primera evidencia
   empírica de la planta.
6. *(Opcional)* Integrar medida no invasiva por pinzas amperimétricas para la
   línea general o cargas no accesibles por enchufe.

## 1.3 Alcance

**Dentro del alcance.** Medición por tomas de corriente de todas las cargas
accesibles; almacenamiento en base de datos temporal; visualización mediante
cuadros de mando; software desarrollado en abierto y documentado; despliegue y
verificación en la sala piloto; caracterización del consumo medido.

**Fuera del alcance.** El sistema no actúa sobre las cargas (no hay control ni
automación); no se realiza análisis de línea base ni auditoría energética formal,
que queda identificada como trabajo futuro; no se modifica la instalación eléctrica
existente ni se instala equipamiento en el cuadro.

## 1.4 Metodología

El proyecto sigue una metodología incremental organizada en fases: análisis del
estado del arte, definición conceptual del sistema, desarrollo del software,
despliegue en planta y verificación, y redacción final. Todos los desarrollos se
gestionan en repositorios públicos de GitHub bajo licencia abierta, de modo que
el resultado sea reproducible y sirva de referencia a otras instalaciones con
restricciones similares. La planificación detallada por semanas se presenta en
el capítulo correspondiente.

## Referencias (borrador)

[1] Kalantari, F.; Mohd Tahir, O.; Akbari Joni, R.; Fatemi, E. (2018). Opportunities
and challenges in sustainability of vertical farming: A review. *Journal of
Landscape Ecology*, 11(1), 35–60. https://doi.org/10.1515/jlecol-2017-0016

[2] Miserocchi, L.; Franco, A. (2025). Benchmarking energy efficiency in vertical
farming: Status and prospects. *Thermal Science and Engineering Progress*, 58,
103165. https://doi.org/10.1016/j.tsep.2024.103165

[3] Keyvan, P.; Roshandel, R. (2024). An integrated Energy-Yield-Cost model to
evaluate clean energy solutions for vertical farms. *Computers and Electronics in
Agriculture*, 219, 108809. https://doi.org/10.1016/j.compag.2024.108809

[4] Ceccanti, F.; Bischi, A.; Desideri, U.; Baccioli, A. (2026). Beyond yield:
Integrating energy, water, cost, and carbon to benchmark indoor vertical farming
viability. *Energy Conversion and Management*, 348, 120646.
https://doi.org/10.1016/j.enconman.2025.120646

[5] Tekler, Z. D.; Low, R.; Yuen, C.; Blessing, L. (2022). Plug-Mate: An IoT-based
occupancy-driven plug load management system in smart buildings. *Building and
Environment*, 223, 109472. https://doi.org/10.1016/j.buildenv.2022.109472

[6] Dhaou, I. B. (2023). Design and Implementation of an Internet-of-Things-Enabled
Smart Meter and Smart Plug for Home-Energy-Management System. *Electronics*,
12(19), 4041. https://doi.org/10.3390/electronics12194041

[7] Suhaimey, M. Z.; Muhamad Amin, M. R. R.; Abd Ghaffar, A. N. (2025). Real-Time
IoT-Based Energy Monitoring System for Residential Applications. *9th IET Smart
Cities Symposium (SCS 2025)*, Bahréin. https://doi.org/10.1049/icp.2026.2504

[8] Jara Ochoa, H. J.; Peña, R.; Ledo Mezquita, Y.; Gonzalez, E.; Camacho-Leon, S.
(2023). Comparative Analysis of Power Consumption between MQTT and HTTP Protocols
in an IoT Platform Designed and Implemented for Remote Real-Time Monitoring of
Long-Term Cold Chain Transport Operations. *Sensors*, 23(10), 4896.
https://doi.org/10.3390/s23104896
