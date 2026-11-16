# Propuesta de TFG — Sistema de monitorización energética para planta piloto de cultivo vertical

- **Titulación:** Grado en Ingeniería en Tecnologías Industriales
- **Escuela:** Escuela Superior de Ingeniería, Universidad de Cádiz
- **Alumno:** Miguel Ángel Castillo Sánchez
- **Tutor propuesto:** Salvador Canas Moreno (UCA — TEP-940 Robótica Aplicada)

## 1. Título del proyecto

Sistema de bajo coste para la monitorización energética de una planta piloto de
cultivo vertical basado en hardware y software de código abierto.

## 2. Motivación

La planta piloto de cultivo vertical de la ESI, alojada en una sala de laboratorio
de ~10 × 15 m, se alimenta exclusivamente mediante tomas Schuko de pared y no
dispone de ningún sistema de medida. La literatura sitúa el consumo específico del
cultivo vertical de lechuga entre 10 y 18 kWh/kg (Miserocchi & Franco, 2025) y
muestra que la iluminación representa el 65–90 % del consumo. Sin medición
desagregada por cargas no es posible caracterizar el consumo real de la instalación
ni proponer mejoras con rigor. Se propone por tanto un sistema de monitorización de
bajo coste, de desarrollo propio y publicado en abierto, que mida por tomas de
corriente y almacene y visualice los datos de forma continua.

## 3. Objetivos

**Objetivo general:** diseñar, implementar y validar un sistema de monitorización
energética de bajo coste para la planta piloto de cultivo vertical de la ESI, que
proporcione medidas fiables de las cargas eléctricas presentes y futuras.

**Objetivos específicos:**

1. Analizar el estado del arte en monitorización energética aplicada al cultivo
   vertical y a las cargas de enchufe (plug loads).
2. Definir la arquitectura del sistema: sensores de medida, datalogger, base de
   datos temporal y visualización, justificando cada decisión técnica.
3. Desarrollar el software de adquisición, almacenamiento y visualización como
   proyecto de código abierto.
4. Validar el sistema en laboratorio y documentar su despliegue en la planta
   piloto (guía de instalación para el montaje por personal de la ESI), verificando
   la calidad de las medidas (continuidad, razonabilidad y resolución temporal).
5. Caracterizar el consumo de cargas reales disponibles en laboratorio y —si el
   despliegue en la planta piloto se produce durante el curso, con acceso remoto
   a los datos— también de la propia planta, como evidencia empírica del consumo.
6. *(Opcional)* Integrar medida no invasiva por pinzas amperimétricas (CT) para
   la línea general o cargas no accesibles por enchufe.

## 4. Alcance

**Dentro:** medición por tomas de corriente de todas las cargas accesibles;
almacenamiento en base de datos temporal; visualización con cuadros de mando;
software libre documentado; validación en laboratorio y despliegue documentado en
la planta piloto; caracterización del consumo medido.

**Fuera:** actuación sobre las cargas (sin control ni automatización); análisis
de línea base o auditoría energética formal (trabajo futuro); modificaciones de
la instalación eléctrica existente.

## 5. Metodología

Trabajo incremental por fases: (1) estado del arte; (2) definición conceptual del
sistema; (3) desarrollo del software; (4) despliegue en planta y verificación;
(5) caracterización y redacción final. Todo el desarrollo se gestiona en
repositorios GitHub públicos bajo licencia abierta, con documentación en
Markdown y diagramas en formato editable (draw.io).

## 6. Entregables

1. Sistema de monitorización diseñado, implementado y validado en laboratorio,
   listo para su instalación en la planta piloto, junto con la guía de instalación
   y despliegue para su montaje por personal de la ESI.
2. Repositorio público con el software, la documentación y los diagramas
   (licencia abierta).
3. Memoria del TFG según estructura UNE 157001.
4. Manual de usuario y de mantenimiento del sistema (anexo de la memoria).

## 7. Riesgos y mitigación

1. **Retraso del levantamiento de datos en sala** (pendiente de confirmar) →
   trabajar con hipótesis documentadas hasta entonces.
2. **Instalación eléctrica desconocida** → definir el material de medida tras el
   levantamiento de datos; la adquisición la gestiona la UCA.
3. **No se produce el despliegue en la planta piloto durante el curso** →
   escenario B: validación en laboratorio propio con cargas reales y despliegue
   documentado en la memoria. El TFG emplea únicamente datos reales (laboratorio
   y/o planta piloto).
4. **Restricciones de red de la universidad** → arquitectura con broker local;
   la publicación de datos se hace desde el propio datalogger.

## 8. Ampliaciones previstas (a valorar con el tutor — posible v0.2)

- Incorporación de **variables ambientales auxiliares** (temperatura y humedad
  interior; temperatura e irradiancia exterior mediante API meteorológica
  gratuita) para contextualizar el consumo y facilitar el benchmarking con la
  literatura.
- Extensión futura hacia **control** de cargas y análisis de línea base
  (identificadas como trabajo futuro, fuera del alcance de este TFG).
