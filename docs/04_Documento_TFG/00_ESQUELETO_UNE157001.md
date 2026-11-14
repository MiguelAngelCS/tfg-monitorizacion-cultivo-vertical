# Esqueleto del documento del TFG — UNE 157001 (v0.1)

Estructura orientativa según UNE 157001:2014 (Información y documentación. Documentos de proyectos
de ingeniería). Se ajustará al modelo concreto que use la ESI (pendiente confirmar si hay plantilla).

## Elementos preliminares
- Portada externa (Anexo I del reglamento)
- Portada interna (Anexo I)
- Resumen (español) + Abstract (si procede) + 5 palabras clave
- Índices (general, de figuras, de tablas)
- (Declaración de autoría / originalidad — según plantilla UCA)

## Cap. 1 — Antecedentes y objeto del proyecto
- Contexto: cultivo vertical, laboratorio, planta piloto UCA
- Motivación y finalidad (viabilidad energética, estudio de consumos)
- Alcance (MVP: monitorización de consumos; ampliaciones futuras)
- Antecedentes y estado del arte (aquí o capítulo independiente según plantilla)
- Justificación (técnica, económica, formativa)

## Cap. 2 — Condiciones de partida / requisitos
- Descripción de la instalación (sala, bandejas, tomas, cuadro) *[pendiente de confirmar]*
- Normativa aplicable (REBT RD 842/2002, UNE aplicables, RGPD si aplica, normas UCA)
- Restricciones y requisitos del tutor/UCA (red, presupuesto)

## Cap. 3 — Definición del sistema
- Requisitos funcionales y no funcionales (p. ej.: resolución de medida, frecuencia de muestreo, disponibilidad)
- Arquitectura general del sistema (capas: captura → transporte → almacenamiento → visualización)
- Justificación de tecnologías (Shelly vs alternativas; Raspberry Pi; stack software open source)

## Cap. 4 — Diseño del sistema
- Diseño eléctrico/de medida: esquema de conexión de sensores en tomas, unifilar simplificado
- Diseño de red y comunicaciones (MQTT/HTTP, Wi-Fi, etc.)
- Diseño del software: módulos, diagramas de flujo, esquema de base de datos, API/visualización
- Presupuesto (BOM) y plan de adquisición

## Cap. 5 — Implementación y pruebas
- Montaje en sala (documentado con fotos)
- Desarrollo del software (repositorio GitHub: estructura, control de versiones)
- Plan de pruebas y resultados
- Periodo de medición y análisis de datos obtenidos

## Cap. 6 — Conclusiones
- Conclusiones técnicas
- Cumplimiento de objetivos
- Trabajo futuro

## Bibliografía
- Única, al final de la memoria (UNE-ISO 690), con enlace a la fuente de cada referencia. Las citas en el texto enlazan con su publicación (DOI).

## Anexos
- Manual de usuario del software (obligatorio por Art. 17.b)
- Fichas técnicas de equipos
- Planos (draw.io)
- Repositorio GitHub (URL + release)
- Presupuesto detallado

---
## Notas de redacción
- Idioma: español (pendiente confirmar).
- Formato final: Markdown plano por capítulos → maquetación posterior por el alumno con plantilla UCA.
- Figuras y tablas numeradas, bibliografía con citas verificadas.
