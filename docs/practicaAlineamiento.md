# Práctica de Alineamiento de Secuencias con Biopython

Esta práctica tiene como objetivo explorar diferentes métodos de alineamiento de secuencias utilizando Biopython y la clase PairwiseAligner.
A lo largo de los ejercicios se estudian tanto alineamientos de ADN como de proteínas, analizando cómo influyen los parámetros y las matrices de sustitución en el alineamiento final.

La práctica está dividida en tres ejercicios principales:

## Ejercicio 1. Implementación de Needleman–Wunsch

En este primer ejercicio se implementa desde cero el algoritmo Needleman–Wunsch, utilizando una matriz de puntuación, penalizaciones de huecos y una matriz de traceback.

A partir de dos secuencias de ADN, el programa construye la matriz de puntuación, calcula el alineamiento óptimo global, reconstruye las secuencias alineadas y muestra tanto las matrices como el alineamiento final

Este ejercicio permite comprender en detalle cómo funciona el alineamiento global a nivel algorítmico.

Se puede ver el ejercicio completo en:

[![Práctica Alineamiento](https://img.shields.io/badge/Ver_Notebook-GitHub-blue?logo=github)](https://nbviewer.org/url/raquelaq.github.io/NeedlemanWunschAlgorithm/NeedlemanWunsch.ipynb)

## Ejercicio 2. Alineamiento de ADN con PairwiseAligner

En este ejercicio se utiliza la clase PairwiseAligner para realizar alineamientos de ADN en dos escenarios:

### a) Secuencias generadas aleatoriamente

Se generan dos secuencias de longitud aleatoria y se alinean en modo global, observando cómo el algoritmo introduce huecos y penaliza sustituciones.
Esto permite comprobar el funcionamiento del alineador con secuencias sin relación biológica.

### b) Secuencias reales obtenidas de bases de datos (NCBI)

Se descargan secuencias reales desde NCBI (por ejemplo, un gen humano y su ortólogo de ratón) y se alinean bajo distintas configuraciones, modificando:

- match / mismatch 
- penalización de apertura y extensión de huecos 
- modo global vs local

Se observan cambios importantes en el alineamiento según el sistema de puntuación, lo que demuestra la importancia de elegir adecuadamente los parámetros dependiendo del estudio biológico.

[![Práctica Alineamiento](https://img.shields.io/badge/Ver_Notebook-GitHub-blue?logo=github)](https://nbviewer.org/url/raquelaq.github.io/NeedlemanWunschAlgorithm/Ejercicio2.ipynb)

## Ejercicio 3. Alineamiento de proteínas con matrices de sustitución

En el último ejercicio se trabaja con secuencias de proteínas, donde las sustituciones no pueden tratarse como simples matches o mismatches. Se realizan dos escenarios:

### a) Secuencias proteicas generadas automáticamente

Se generan dos proteínas aleatorias y se alinean con PairwiseAligner usando los valores por defecto, lo que muestra que este sistema es insuficiente para proteínas.

### b) Secuencias reales obtenidas de UniProt + uso de matrices

Se alinean proteínas reales utilizando distintas matrices de sustitución:

- *BLOSUM62*: adecuada para similitud moderada
- *PAM250*: útil para similitud distante
- *Matriz personalizada*: diseñada para favorecer aminoácidos hidrofóbicos

El ejercicio muestra cómo cada matriz altera profundamente la puntuación y el alineamiento, revelando distintos tipos de similitud evolutiva o estructural.

Se puede ver el ejercicio completo en el siguiente enlace:

[![Práctica Alineamiento](https://img.shields.io/badge/Ver_Notebook-GitHub-blue?logo=github)](https://nbviewer.org/url/raquelaq.github.io/NeedlemanWunschAlgorithm/Ejercicio3.ipynb)
