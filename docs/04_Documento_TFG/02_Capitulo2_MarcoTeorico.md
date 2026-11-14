# Capítulo 2 — Marco teórico y estado del arte

> Borrador v0.1 (noviembre 2026). Numeración de referencias continua con el
> Capítulo 1. Las citas [n] enlazan directamente con su publicación (DOI);
> la lista completa se unifica en el capítulo de bibliografía final.

## 2.1 El cultivo vertical y su problema energético

El cultivo vertical indoor sustituye la radiación solar por iluminación artificial,
el clima exterior por ventilación forzada y el riego por gravedad por bombeo
controlado. La consecuencia directa es que la energía eléctrica pasa a ser el
principal recurso de producción y, al mismo tiempo, su principal coste. La
revisión de Kalantari et al. ya identificaba en 2018 el coste energético y
económico como la barrera principal de la sostenibilidad de estas instalaciones
[[1]](https://doi.org/10.1515/jlecol-2017-0016), y casi una década después la situación no ha cambiado cualitativamente:
Aborujilah, en una revisión sistemática PRISMA de 52 artículos publicados entre
2014 y 2024, constata que el ahorro energético depende de cada cultivo, clima y
diseño de instalación, y señala como barrera transversal la **falta de datos
reales de campo y de métricas estandarizadas** [[10]](https://doi.org/10.3390/su17188142).

Las cifras disponibles confirman la magnitud del problema. Miserocchi y Franco
sitúan el consumo específico actual de la lechuga entre 10 y 18 kWh/kg y proponen
como benchmark técnico realista el intervalo 3,1–7,4 kWh/kg [[2]](https://doi.org/10.1016/j.tsep.2024.103165). Keyvan y
Roshandel, con un modelo horario integrado energía–rendimiento–coste, obtienen
11,34 kWh/kg y 3,78 $/kg en un contenedor de cultivo, con un reparto del 78 %
para iluminación y el 19 % para deshumidificación [[3]](https://doi.org/10.1016/j.compag.2024.108809). Ceccanti et al. amplían la
perspectiva a un benchmark multidimensional (energía, agua, coste y carbono) sobre
162 escenarios, encontrando consumos entre 5,05 y 23,8 kWh/kg según la
configuración de temperatura, PPFD y CO₂ [[4]](https://doi.org/10.1016/j.enconman.2025.120646). En todos los casos, la iluminación
domina el consumo y su densidad de flujo fotosintético es la variable de diseño
más influyente [[4]](https://doi.org/10.1016/j.enconman.2025.120646).

Una línea reciente de la literatura propone gestionar el cultivo de forma
dinámica, adaptando el entorno (PPFD, CO₂, temperatura) tanto a la fisiología de
la planta como al precio horario de la electricidad [[9]](https://doi.org/10.3389/fsci.2024.1411259). Esta línea confirma un
punto esencial para este proyecto: **cualquier optimización exige conocer primero
el consumo real con resolución temporal suficiente**. Los modelos de referencia
trabajan con paso horario [[3]](https://doi.org/10.1016/j.compag.2024.108809), lo que fija un requisito mínimo de resolución para
el sistema de medida.

## 2.2 Monitorización energética: medida intrusiva y por enchufe

La monitorización de energía en edificios se clasifica habitualmente en
intrusiva (ILM), con sensores instalados por carga o circuito, y no intrusiva
(NILM), que infiere cargas a partir de una única medida agregada. Para este
proyecto la opción relevante es la ILM por tomas de corriente (plug loads), por
tres razones: la sala solo tiene acceso por enchufe, el número de cargas es
reducido y la medida directa no requiere modelos de inferencia.

La relevancia de los plug loads está bien documentada. Tekler et al., en un
estudio de campo de cinco meses en una oficina universitaria con smart plugs
gestionados por ocupación, reportan ahorros medios del 51,7 % en los equipos
controlados y una reducción del 7,5 % del consumo total del edificio, con los
plug loads alcanzando entre el 30 y el 50 % del consumo en edificios eficientes
[[5]](https://doi.org/10.1016/j.buildenv.2022.109472). La precisión de la medida por enchufe también está validada: Dhaou obtiene
precisiones superiores al 99 % frente a medida de laboratorio en un smart plug de
desarrollo propio [[7]](https://doi.org/10.1049/icp.2026.2504). En paralelo, la medida no invasiva por pinzas
amperimétricas queda validada como alternativa para líneas no accesibles por
enchufe, con precisiones del orden del ±1 % en corriente en el sistema
residencial de Suhaimey et al. [[8]](https://doi.org/10.3390/s23104896). Lee y Yang, por su parte, proponen una
arquitectura distribuida de smart plugs con gateway inteligente que anticipa la
arquitectura por capas adoptada en este proyecto (medida → concentrador →
visualización) [[12]](https://doi.org/10.1177/1550147717718462).

## 2.3 Comunicaciones: el protocolo MQTT

El transporte de datos de los sensores al concentrador puede hacerse mediante
peticiones HTTP o mediante protocolos de mensajería ligera tipo publish/subscribe.
La comparación experimental de Jara Ochoa et al. cuantifica el beneficio de la
segunda opción: MQTT con QoS 0 consume un 6,03 % menos energía que HTTP, y con
QoS 1 un 8,33 % menos, diferencia que se traduce en horas significativas de
autonomía en dispositivos IoT [[8]](https://doi.org/10.3390/s23104896). Además del ahorro energético, el patrón
publish/subscribe desacopla sensores del resto del sistema: un sensor nuevo solo
necesita publicar en un tema del broker para integrarse, sin cambios en el
recolector. Esta propiedad, junto con el comportamiento demostrado de
reconexión automática ante cortes de red [[8]](https://doi.org/10.3390/s23104896), hace de MQTT la elección natural
para el nivel de comunicaciones.

## 2.4 Arquitecturas de referencia y bases de datos temporales

Los sistemas de monitorización energética de desarrollo propio descritos en la
literatura comparten una arquitectura común: nodos de medida que publican por
MQTT, un concentrador que aloja el broker y el almacenamiento, y una capa de
visualización. Suhaimey et al. validan exactamente este esquema con una Raspberry
Pi 5 como hub central (broker Mosquitto y visualización en Home Assistant) y
nodos ESP32 con PZEM-004T [[8]](https://doi.org/10.3390/s23104896). En instalaciones de pequeña escala comparables a
la planta piloto, Nikolov et al. demuestran además la viabilidad de monitorizar
variables de proceso (temperatura, humedad, pH) con sensores de bajo coste y
software abierto [[11]](https://doi.org/10.3390/agriculture13061191).

El almacenamiento de series temporales exige una base de datos adecuada al
patrón de escritura (muchas inserciones, consultas agregadas por rangos). Las
opciones dominantes en el ámbito abierto son InfluxDB y TimescaleDB (PostgreSQL
extendido), y la visualización mediante Grafana, estándar de facto en
monitorización de infraestructuras. La decisión definitiva entre ambas se
documentará en el capítulo de diseño; ambas satisfacen los requisitos de
resolución temporal y retención del proyecto.

## 2.5 Variables ambientales: contextualización del consumo

Medir la electricidad por sí sola describe el *qué*; contextualizarla explica el
*por qué* y habilita el benchmarking. Dos familias de variables ambientales son
relevantes para esta instalación:

- **Exteriores (gratuitas, sin hardware):** temperatura e irradiancia solar
  horarias pueden obtenerse de APIs meteorológicas abiertas (AEMET OpenData,
  Open-Meteo) sin coste ni instalación. La irradiancia es especialmente
  interesante: permite contrastar el consumo de iluminación de la sala con la
  luz solar disponible en el exterior, dato clave para valorar en trabajo futuro
  el potencial de fotovoltaica (Keyvan y Roshandel estiman que hacen falta 4,7
  m² de paneles por m² de cultivo vertical para el autoconsumo [[3]](https://doi.org/10.1016/j.compag.2024.108809)) y para
  interpretar la estacionalidad del consumo.
- **Interiores (bajo coste):** temperatura y humedad ambiente de la sala con
  sensores tipo SHT31 (~5 €), que describen el entorno en el que operan las
  cargas y sirven de base a futuras ampliaciones hacia control de clima.

Estas variables no modifican el alcance del sistema de medida eléctrica (que
sigue siendo el núcleo del proyecto), sino que se añaden como canal paralelo en
el mismo datalogger y base de datos. Su coste es prácticamente nulo y su valor
para el análisis y el benchmarking con la literatura —donde el PPFD y la
temperatura son los factores dominantes del consumo [[4]](https://doi.org/10.1016/j.enconman.2025.120646)— es considerable. Se
incluyen por tanto como objetivo complementario, pendiente de validación con el
tutor.

## 2.6 Síntesis y posicionamiento del proyecto

Del estado del arte se desprende una conclusión directa: existe abundante
literatura sobre modelos y benchmarks de consumo en cultivo vertical, y existe
literatura sobre sistemas de monitorización energética por enchufe en edificios,
pero son escasos los trabajos que aportan **datos reales de campo de una
instalación de pequeña escala**, necesidad explícitamente señalada por la
revisión sistemática de Aborujilah [[10]](https://doi.org/10.3390/su17188142). Este proyecto aporta exactamente eso:
un sistema de medida desagregada, permanente y de código abierto sobre una
planta piloto real, cuyos datos podrán contrastarse con los benchmarks del estado
del arte (3,1–7,4 kWh/kg como horizonte técnico [[2]](https://doi.org/10.1016/j.tsep.2024.103165)) en trabajo futuro. La
arquitectura elegida (smart plugs comerciales con medida + MQTT + Raspberry Pi +
base de datos temporal + Grafana) está validada por la literatura [[7]](https://doi.org/10.1049/icp.2026.2504)[[8]](https://doi.org/10.3390/s23104896),
es reproducible con presupuesto inferior a 200 € y no requiere modificar la
instalación eléctrica de la sala.
