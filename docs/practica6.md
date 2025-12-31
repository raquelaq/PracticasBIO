# Práctica de Estructuras Tridimensionales con Biopython

## Introducción

En esta práctica se aborda el análisis de estructuras tridimensionales de proteínas utilizando Python y la librería Biopython. Aunque el análisis de secuencias es fundamental en bioinformática, la función biológica de una molécula está determinada en última instancia por su estructura 3D.

A lo largo de la práctica se trabaja con estructuras reales obtenidas de la base de datos RCSB Protein Data Bank (PDB) en formato PDBx/mmCIF, explorando cómo Biopython representa internamente estas estructuras y cómo pueden analizarse mediante operaciones geométricas como distancias, ángulos y ángulos diedros.

## Ejercicio 1. Análisis estructural de la hemoglobina humana (PDB: 1A3N)

En este ejercicio se descarga y visualiza la estructura tridimensional de la hemoglobina humana, y se carga en Biopython como un objeto `Structure`.

A partir de esta estructura se realizan los siguientes análisis:

- cálculo de la distancia entre átomos concretos de la cadena A
- cálculo de un ángulo diedro entre átomos consecutivos del esqueleto peptídico
- cálculo del centro de masas de la proteína

Este ejercicio introduce la jerarquía interna de Biopython (Structure → Model → Chain → Residue → Atom) y el manejo directo de coordenadas atómicas.

El notebook con el desarrollo del ejercicio puede consultarse aquí:

[![Bloque1](https://img.shields.io/badge/Ver_Notebook-GitHub-blue?logo=github)](https://github.com/marianabordes/Practica6BIO/blob/main/ejercicio1.ipynb)


## Ejercicio 2. Análisis estructural de la lisozima (PDB: 1LYZ)

En este ejercicio se trabaja con la estructura tridimensional de la lisozima del huevo de gallina, una proteína clásica en estudios estructurales.

Las tareas realizadas incluyen:

- recuento de átomos de la estructura
- identificación del primer y último átomo
- cálculo de un ángulo entre átomos
- localización del átomo situado en la posición central de la estructura y su residuo correspondiente

Este ejercicio profundiza en el recorrido secuencial de los átomos de una proteína y en el análisis geométrico básico de estructuras 3D.

El notebook puede consultarse en el siguiente enlace:

[![Bloque1](https://img.shields.io/badge/Ver_Notebook-GitHub-blue?logo=github)](https://github.com/marianabordes/Practica6BIO/blob/main/ejercicio2.ipynb)

## Ejercicio 3. Análisis estructural y comparación de orexinas / hipocretinas

En este ejercicio final se realiza un análisis más completo combinando secuencia y estructura. Se trabaja con las proteínas:

- Orexina-A / Hipocretina-1 (PDB: 1WSO)
- Orexina-B / Hipocretina-2 (PDB: 1CQ0)

Las tareas incluyen:

- descarga y alineamiento de las secuencias
- búsqueda de homólogos mediante BLAST
- construcción de un árbol filogenético con Neighbor Joining
- visualización de las estructuras 3D
- implementación de una función en Biopython para determinar cuál de las dos proteínas presenta la mayor distancia entre sus átomos

Este ejercicio integra conceptos de filogenia, análisis estructural y programación bioinformática.

El notebook completo se encuentra disponible aquí:

[![Bloque1](https://img.shields.io/badge/Ver_Notebook-GitHub-blue?logo=github)](https://github.com/marianabordes/Practica6BIO/blob/main/ejercicio3.ipynb)


Esta práctica proporciona una introducción práctica al análisis de estructuras tridimensionales de proteínas, mostrando cómo la información estructural puede explorarse y cuantificarse mediante herramientas computacionales. El uso de Biopython permite trabajar de forma directa con datos reales del PDB y desarrollar análisis reproducibles que combinan geometría molecular, biología estructural y programación.