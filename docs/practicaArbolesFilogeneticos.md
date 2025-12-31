# Práctica de Árboles Filogenéticos con Biopython

## Introducción

En esta práctica se aborda el estudio de los árboles filogenéticos como herramienta fundamental para inferir relaciones evolutivas entre secuencias biológicas. A partir de secuencias de ADN alineadas, se exploran distintos métodos de construcción de árboles filogenéticos, analizando cómo las decisiones metodológicas influyen en la topología y en la interpretación de los resultados

La práctica se desarrolla íntegramente en Python utilizando la librería Biopython, lo que permite integrar análisis computacionales reproducibles con una interpretación biológica rigurosa. A lo largo de los ejercicios se trabaja tanto con árboles ya existentes en formato Newick como con árboles generados a partir de datos, combinando análisis manuales y computacionales.

---

## Ejercicio 1. Análisis de un árbol filogenético en formato Newick

En este ejercicio se trabaja con un árbol filogenético previamente definido en formato Newick, con el objetivo de comprender su estructura y los elementos que lo componen.

A partir del árbol de extrae información relevante como:

- número de especies terminales
- número de nodos internos
- nombres de las especies
- longitudes de las ramas
- organización en clados y clado raíz

Este ejercicio permite familiarizarse con la representación estándar de árboles filogenéticos y con el uso del módulo `Bio.Phylo` para su análisis estructural y visualización.

El notebook con el desarrollo completo del ejercicio puede consultarse aquí:

[![Ejercicio 1](https://img.shields.io/badge/Ver_Notebook-GitHub-blue?logo=github)](https://nbviewer.org/url/raquelaq.github.io/ArbolesFilogeneticos/ejercicio1.ipynb)

---

## Ejercicio 2. Modificación e interpretación visual de un árbol filogenético

En este ejercicio se parte del árbol analizado anteriormente y se introducen distintas modificaciones controladas con el objetivo de explorar cómo la representación gráfica puede influir en la interpretación de un árbol filogenético.

Las modificaciones realizadas incluyen:

- cambio de nombres comunes por nomenclatura científica
- ajuste selectivo de longitudes de ramas para enfatizar divergencias evolutivas
- uso del color para destacar linajes y clados evolutivos

Este ejercicio pone el foco en el árbol filogenético no solo como estructura de datos, sino como una herramienta de comunicación científica, donde la claridad visual juega un papel clave.

El notebook correspondiente puede consultarse en el siguiente enlace:

[![Ejercicio 2](https://img.shields.io/badge/Ver_Notebook-GitHub-blue?logo=github)](https://nbviewer.org/url/raquelaq.github.io/ArbolesFilogeneticos/ejercicio2.ipynb)

---

## Ejercicio 3. Construcción y comparación de árboles filogenéticos a partir de secuencias

En este ejercicio se trabaja directamente con un conjunto de secuencias de ADN alineadas en formato FASTA, correspondientes a distintas especies de primates. A partir de estas secuencias se abordan varias fases del análisis filogenético.

### Ejercicio 3.1. Construcción manual de un árbol mediante UPGMA

En primer lugar, se resuelve de forma manual la construcción de un árbol filogenético utilizando el método UPGMA, calculando paso a paso la matriz de distancias, los agrupamientos sucesivos y las longitudes de rama.

Este ejercicio resulta clave para comprender de forma intuitiva el funcionamiento del algoritmo y sus supuestos, como la hipótesis de reloj molecular.

### Ejercicio 3.2. Construcción computacional de árboles filogenéticos

A continuación, las mismas secuencias se utilizan para generar árboles filogenéticos mediante distintos métodos computacionales:

- **Máxima parsimonia**, buscando el árbol que minimiza el número de cambios evolutivos.
- **Métodos basados en distancia**, empleando:
  - UPGMA
  - Neighbor Joining

Este apartado permite comparar cómo distintos criterios de construcción pueden dar lugar a topologías similares o diferentes a partir del mismo alineamiento.

### Ejercicio 3.3. Almacenamiento y visualización de los árboles

Los árboles obtenidos mediante los distintos métodos se guardan en formato Newick, el estándar para el intercambio de árboles filogenéticos. Posteriormente, se representan gráficamente para facilitar su comparación visual y análisis conjunto.

### Ejercicio 3.4. Comparación de resultados y conclusiones

Finalmente, se comparan los árboles obtenidos por los distintos métodos, analizando similitudes, diferencias y las implicaciones de las suposiciones de cada enfoque. Este apartado pone de manifiesto el carácter hipotético de la filogenia y la importancia de contrastar resultados obtenidos con distintos métodos.

El notebook que recoge todo el desarrollo del Ejercicio 3 puede consultarse aquí:

[![Ejercicio 3](https://img.shields.io/badge/Ver_Notebook-GitHub-blue?logo=github)](https://nbviewer.org/url/raquelaq.github.io/ArbolesFilogeneticos/ejercicio3.ipynb)

## Ejercicio 4. Generación de secuencias aleatorias y almacenamiento en FASTA

En este ejercicio se desarrolla un script en Python que genera automáticamente cinco secuencias de ADN de cinco nucleótidos cada una, de forma aleatoria, y las almacena en un archivo FASTA válido.

Este ejercicio introduce el uso de datos sintéticos como herramienta didáctica para estudiar el comportamiento de los métodos filogenéticos en ausencia de una señal evolutiva real, reforzando la comprensión de sus limitaciones y supuestos.

El notebook con la implementación del script puede consultarse aquí:

[![Ejercicio 3.1](https://img.shields.io/badge/Ver_Notebook-GitHub-blue?logo=github)](https://nbviewer.org/url/raquelaq.github.io/ArbolesFilogeneticos/ejercicio3_1.ipynb)


Esta práctica ofrece una visión progresiva del análisis filogenético, desde la lectura e interpretación de árboles hasta su construcción y comparación mediante distintos métodos. El uso de Biopython permite integrar de forma natural programación, análisis de datos y razonamiento biológico, acercando el trabajo realizado a un flujo de trabajo real en bioinformática.
