# Capítulo 3 — Definición del sistema (v0.1 provisional)

> Borrador provisional (noviembre 2026). Todo lo marcado como **[hipótesis]** depende
> del levantamiento de datos en sala (pendiente de confirmar) y quedará
> fijado en la v1.0 cuando se realice.

## 3.1 Requisitos

**Funcionales:**

- RF1. Medición de potencia activa, energía acumulada y factor de potencia de
  cada carga accesible por toma de corriente.
- RF2. Adquisición continua con resolución temporal de 1 min o mejor (la
  literatura de referencia trabaja con paso horario [3], así que 1 min sobra con
  margen).
- RF3. Almacenamiento permanente en base de datos temporal con retención
  indefinida.
- RF4. Visualización en cuadros de mando: potencia instantánea por carga,
  energía diaria/semanal/mensual, históricos.
- RF5. Registro de variables ambientales auxiliares (temperatura/humedad
  interior si se instalan; temperatura/irradiancia exterior vía API meteorológica).
- RF6. Recuperación automática ante cortes de red y de alimentación
  (comportamiento validado en la literatura [8]).

**No funcionales:**

- RNF1. Bajo coste: presupuesto total inferior a 200 €.
- RNF2. Sin modificación de la instalación eléctrica existente (solo enchufes).
- RNF3. Software íntegramente de código abierto y publicado en repositorio público.
- RNF4. Desplegable y mantenible por personal no especializado (manual de
  usuario como entregable).
- RNF5. **[hipótesis]** Conectividad: la sala dispone de Wi-Fi; si la red
  universitaria impide el tráfico local MQTT, el broker se configura en modo
  aislado con la Raspberry Pi como punto de acceso dedicado.

## 3.2 Arquitectura provisional

El sistema sigue la arquitectura por capas validada en la literatura [8][12]:

1. **Capa de medida.** Smart plugs con medida integrada (tipo Shelly Plug S,
   16 A Schuko) entre cada carga y su toma. **[hipótesis]** número de unidades:
   5–8 según inventario definitivo de la sala. Como ampliación opcional, pinzas
   amperimétricas no invasivas (tipo SCT-013) para la línea general [8].
2. **Capa de comunicaciones.** Los smart plugs publican sus medidas por MQTT
   (vía firmware de fabricante o Tasmota) sobre la red Wi-Fi local. Elección
   justificada por el menor consumo frente a HTTP [8] y por el desacoplo
   publish/subscribe.
3. **Capa de concentración y almacenamiento.** Raspberry Pi (reutilizando la
   instalada en la sala **[hipótesis a confirmar: modelo y disponibilidad]**)
   alojando: broker Mosquitto, recolector de datos (Telegraf o script propio) y
   base de datos temporal. Decisión pendiente: **InfluxDB** vs **TimescaleDB** —
   criterio: facilidad de mantenimiento y copias de seguridad.
4. **Capa de visualización.** Grafana sobre la misma Raspberry Pi (o acceso web
   remoto según permita la red universitaria), con cuadros de mando por carga y
   agregados.
5. **Canal ambiental.** Servicio en el datalogger que consulta periódicamente
   una API meteorológica abierta (AEMET OpenData u Open-Meteo) para temperatura e
   irradiancia exterior, y —si se aprueba— sensores interiores de
   temperatura/humedad conectados a la Raspberry Pi.

## 3.3 Justificación de decisiones tecnológicas

- **Medida comercial frente a desarrollo propio (DIY).** La alternativa DIY
  (ESP32 + PZEM-004T, precisión >99 % [7]) ofrece control total pero exige
  fabricación, calibración y mantenimiento de cada nodo. Los smart plugs
  comerciales con API local y medida integrada reducen el riesgo de despliegue
  y mantienen el presupuesto; la precisión de la medida por enchufe está
  validada en la literatura [7]. La comparativa detallada de modelos (Shelly,
  Sonoff, Tapo) se documentará en este capítulo antes de la compra.
- **MQTT frente a HTTP.** Justificado experimentalmente por el ahorro energético
  y el desacoplo (sección 2.3) [8].
- **InfluxDB frente a TimescaleDB.** Ambas satisfacen los requisitos; la
  decisión se tomará en la fase de desarrollo con una comparativa operativa
  (consumo de recursos en la Raspberry Pi, facilidad de backup).
- **Raspberry Pi como concentrador.** Validada como hub central en sistemas
  equivalentes [8]; reutiliza hardware ya instalado (coste cero).

## 3.4 Variables y resolución temporal

| Variable | Origen | Resolución |
|---|---|---|
| Potencia activa (W) | Smart plug | 1 min |
| Energía acumulada (kWh) | Smart plug | 1 min |
| Factor de potencia | Smart plug | 1 min |
| Temperatura/humedad interior | Sensor SHT31 (opcional) | 5 min |
| Temperatura/irradiancia exterior | API meteorológica | 1 h |

## 3.5 Presupuesto preliminar **[hipótesis]**

| Partida | Estimación |
|---|---|
| 5–8 smart plugs con medida (15–20 €/ud) | 75–160 € |
| Sensores interiores temp/humedad (2 ud) | ~10 € |
| Material de red/cableado | ~10 € |
| Raspberry Pi | 0 € (reutilizada) |
| Software | 0 € (open source) |
| **Total** | **~95–180 €** (límite: 200 €) |

## 3.6 Decisiones pendientes de confirmar

1. Inventario definitivo de cargas, marcas y potencias (número de smart plugs).
2. Modelo y estado de la Raspberry Pi instalada; posibilidad de usarla como datalogger.
3. Cobertura Wi-Fi, política de red de la universidad y posibilidad de acceso remoto.
4. Número y tipo de tomas disponibles; posibilidad de medida no invasiva en línea general.
5. Existencia o no de climatización en la sala (no consta en el inventario actual).
