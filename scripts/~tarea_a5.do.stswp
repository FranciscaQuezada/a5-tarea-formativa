
* ============================================================
* A5 — Limpieza y descriptivos de CASEN
* Autor: Francisca Quezada Fecha: 2026-11-17
* ============================================================
clear all
set more off
capture mkdir "output"
capture log close
log using "output/tarea_a5.log", replace text

pwd 
cd "C:\Users\franc\OneDrive\Documentos\Programación\a5-tarea-formativa"

** 2. Cargar Datos
import delimited "data/raw/casen_reducido.csv", clear varnames(1) encoding("utf-8")
describe
summarize

** 3. Crea variables con `generate` y `replace`
* Experiencia potencial de MINCER: edad - educ - 6, con piso en 0
generate experiencia = max(edad - educ - 6, 0)

* Indicadores, genero es texto por eso se compara con "F"
generate mujer     = (genero == "F")
generate alta_educ = ( educ >= 13)   // 13 o mas años de educacion

* generate + replace por tramo de edad (1 = <30. 2 = 30-49, 3 = +50)
generate tramo_edad = 1
replace  tramo_edad = 2 if edad >= 30
replace  tramo_edad = 3 if edad >= 50

** 4. Etiqueta (la cultura de Stata)
label variable experiencia "Experiencia potencial (años)"
label variable mujer       "Mujer (1 = si)"
label variable alta_educ   "Educacion alta (13+ años)"
label variable tramo_edad  "Tramo de edad (1 = <30, 2 = 30,49, 3 = 50+)"

* Etiquetas de valores de los indicadores
label define sino 0 "No" 1 "Si"
label values alta_educ sino

** 5. Cuidado con los missing
count if missing(ingreso)     // 5 
* ¿Por qué `summarize ingreso` no se equivoca con los missing, pero `count
* if ingreso > 500000` **sí** puede equivocarse?
* Respuesta: summarize excluye automaticamente los missing de sus calculos, 
* asi que la media y el N solo usan a quienes tienen dato. En cambio, en
* STATA el missing es mayor que cualquier numero, asi que la condicion
* "ingreso < 500000" tambien es verdadera para los missing, y count los 
* cuenta como si fueran ingresos altos. Hay que excluirlos:

count if ingreso > 500000 // incorrecto porque incluye missing, serian 46
count if ingreso > 500000 & !missing(ingreso) // correcto, son 41

** 6. Descriptivos

* 6.1 Variables numéricas (lista en una macro: se cambia en un solo lugar)
local numericas "ingreso educ edad experiencia"
summarize `numericas'
summarize ingreso, detail

* 6.2 Tabulación de una categórica
tabulate sector

* 6.3 Tabulación cruzada y summarize por grupo
tabulate sector alta_educ
foreach g in F M {
    display _newline "--- Ingreso, genero = `g' ---"
    summarize ingreso if genero == "`g'"
}

* 6.4 Correlaciones (correlate usa solo filas completas)
correlate ingreso educ experiencia

* 6.5 Guardar un resultado con scalar ANTES de que r() se sobrescriba, pero scalar se conserva
summarize ingreso
scalar media_ingreso = r(mean)
scalar n_ingreso     = r(N)
summarize educ                     // este comando sobrescribe r()...
display "Media de ingreso (guardada): $" %9.0fc media_ingreso " pesos, N = " n_ingreso

** 7. Cierra la bitácora e interpreta
log close

* Interprete
* De las 60 personas, 55 tienen ingreso y el ingreso medio mensual es de
* aprox. $655.000, con mediana cercana a $672.000. El ingreso se asocia
* positivamente con la educación. La correlación entre ingreso y educación
* es de 0,6767 y la de ingreso con experiencia potencial es de -0,0875,
* una asociacion practicamente nula. Esto describe asociaciones en una
* muestra pequeña de 55 personas con dato de ingreso; no permite afirmar
* que la educación cause mayores ingresos.

** Declaración de autoría y uso de IA
* Herramienta utilizada: Claude
* Para qué la usé: como apoyo para corregir los descriptivos y entender 
* como funcionan los missing
* Qué hice yo: realice el codigo en base a los guiones de la semana 13,
* generé el .log, interpreté mis propios resultados y subí 
* los archivos a GitHub.
* Verificación: confirmo que entiendo y puedo explicar todo lo que entrego.
