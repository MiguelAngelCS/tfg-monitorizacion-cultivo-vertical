# Propuesta de TFG — Sistema de monitorización energética para planta piloto de cultivo vertical

> Borrador v0.1 (reconstruido el 2026-11-14; original redactado la semana del
> 10-11-2026 y subido a la plataforma ESI). Verificar contra la versión subida.

- **Titulación:** Grado en Ingeniería en Tecnologías Industriales
- **Escuela:** Escuela Superior de Ingeniería, Universidad de Cádiz
- **Alumno:** Miguel Ángel Castillo Sánchez
- **Tutor propuesto:** Salvador Cañas Moreno (Departamento de Ingeniería Eléctrica — TEP-940 Robótica Aplicada)

## 1. Título del proyecto

Sistema de bajo coste para la monitorización energética de una planta piloto de
cultivo vertical basado en hardware y software de código abierto.

## 2. Motivación

La sala piloto de cultivo vertical de la ESI (~10 × 15 m) se alimenta
exclusivamente mediante tomas Schuko de pared y no dispone de ningún sistema de
medida. La literatura sitúa el consumo específico del cultivo vertical de lechuga
entre 10 y 18 kWh/kg (Miserocchi & Franco, 2025) y muestra que la iluminación
representa el 65–90 % del consumo. Sin medición desagregada por cargas no es
posible caracterizar el consumo real de la instalación ni proponer mejoras con
rigor. Se propone por tanto un sistema de monitorización de bajo coste, de
desarrollo propio y publicado en abierto, que mida por tomas de corriente y
almacene y visualice los datos de forma permanente.

## 3. Objetivos

**Objetivo general:** diseñar, implementar y validar un sistema de monitorización
energética de bajo coste para la sala piloto de cultivo vertical de la ESI, que
proporcione medidas fiables y permanentes de las cargas eléctricas presentes y
futuras.

**Objetivos específicos:**

1. Analizar el estado del arte en monitorización energética aplicada al cultivo
   vertical y a las cargas de enchufe (plug loads).
2. Definir la arquitectura del sistema: sensores de medida, datalogger, base de
   datos temporal y visualización, justificando cada decisión técnica.
3. Desarrollar el software de adquisición, almacenamiento y visualización como
   proyecto de código abierto.
4. Desplegar el sistema en la sala piloto y verificar la calidad de las medidas
   (continuidad, razonabilidad, resolución temporal).
5. Caracterizar el consumo real de las cargas instaladas como primera evidencia
   empírica de la planta.
6. *(Opcional)* Integrar medida no invasiva por pinzas amperimétricas (CT) para
   la línea general o cargas no accesibles por enchufe.

## 4. Alcance

**Dentro:** medición por tomas de corriente de todas las cargas accesibles;
almacenamiento en base de datos temporal; visualización con cuadros de mando;
software libre documentado; despliegue y verificación en sala; caracterización
del consumo medido.

**Fuera:** actuación sobre las cargas (sin control ni automatización); análisis
de línea base o auditoría energética formal (trabajo futuro); modificaciones de
la instalación eléctrica existente.

## 5. Metodología

Trabajo incremental por fases: (1) estado del arte; (2) definición conceptual del
sistema; (3) desarrollo del software; (4) despliegue en planta y verificación;
(5) caracterización y redacción final. Todo el desarrollo se gestiona en
repositorios GitHub públicos bajo licencia abierta, con documentación en
Markdown y diagramas en formato editable (draw.io).

## 6. Planificación (resumen)

| Fase | Periodo |
|---|---|
| Estado del arte y diseño conceptual | nov–dic 2026 |
| Visita a sala y levantamiento de datos | dic 2026 |
| Desarrollo del software | ene–feb 2027 |
| Instalación en sala y periodo de medición | ene–feb 2027 |
| Redacción de capítulos 2–5 | dic 2026–mar 2027 |
| Resultados y conclusiones | mar 2027 |
| Revisión final y entrega | abril 2027 (límite: 5 mayo 2027) |
| Defensa | 17–21 mayo 2027 |

## 7. Presupuesto orientativo

Inferior a 200 €: smart plugs con medida (estimación 5–8 unidades), sensorica
auxiliar de bajo coste y material de red/cableado. Se reutiliza la Raspberry Pi
ya instalada en la sala como datalogger. El software empleado es íntegramente de
código abierto (coste cero).

## 8. Entregables

1. Sistema instalado y operativo en la sala piloto.
2. Repositorio público con el software, la documentación y los diagramas
   (licencia abierta).
3. Memoria del TFG según estructura UNE 157001.
4. Manual de usuario y de mantenimiento del sistema (anexo de la memoria).

## 9. Riesgos y mitigación

1. **Retraso de la visita a la sala** → trabajar con hipótesis documentadas hasta
   el levantamiento de datos.
2. **Instalación eléctrica desconocida** → ninguna compra definitiva antes de la
   visita.
3. **Datos de medida insuficientes** → escenario B: validación en laboratorio
   propio y simulación de datos declarada como tal.
4. **Restricciones de red de la universidad** → arquitectura con broker local;
   la publicación de datos se hace desde el propio datalogger.

## 10. Ampliaciones previstas (a valorar con el tutor — posible v0.2)

- Incorporación de **variables ambientales auxiliares** (temperatura y humedad
  interior; temperatura e irradiancia exterior mediante API meteorológica
  gratuita) para contextualizar el consumo y facilitar el benchmarking con la
  literatura.
- Extensión futura hacia **control** de cargas y análisis de línea base
  (identificadas como trabajo futuro, fuera del alcance de este TFG).
