# A5 — Limpieza y descriptivos de CASEN

Autor: Francisca Quezada
Fecha: 2026-11-17

## Contenido
- `scripts/tarea_a5.do`: do-file comentado.
- `output/tarea_a5.log`: log de la corrida completa.
- `data/raw/casen_reducido.csv`: datos (60 personas).

## Qué hace el do-file
- Carga los datos y crea `experiencia` (Mincer), `mujer`, `alta_educ` y `tramo_edad`.
- Etiqueta variables y valores.
- Revisa los missing de `ingreso` y explica por qué filtrar sin `!missing()` cuenta mal.
- Calcula descriptivos (`summarize`, `tabulate`, `correlate`) y guarda un resultado con `scalar`.

## Cómo correrlo
1. Abrir Stata y ajustar la línea `cd` a la carpeta del proyecto.
2. Ejecutar el do-file completo.

## Declaración de autoría y uso de IA
- Herramienta utilizada: Claude
- Para qué la usé: como apoyo para corregir los descriptivos y entender como funcionan los missing
- Qué hice yo: realice el codigo en base a los guiones de la semana 13, generé el .log, interpreté 
resultados y subí los archivos a GitHub.
- Verificación: confirmo que entiendo y puedo explicar todo lo que entrego.
