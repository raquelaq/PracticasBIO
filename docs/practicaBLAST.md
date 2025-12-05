# Práctica de uso de BLAST con Biopython

## Introducción

En esta práctica se explora el uso de BLAST (Basic Local Alignment Search Tool) mediante Python y la librería Biopython, para comparar secuencias biológicas y encontrar similitudes en bases de datos públicas o locales.
BLAST es una de las herramientas más utilizadas en bioinformática, ya que permite identificar relaciones evolutivas, funciones potenciales de genes o proteínas, y verificar la identidad de secuencias experimentales.

## Ejercicio 1. Búsqueda BLASTn con una secuencia de ADN

En este ejercicio se desarrolla un programa que solicita al usuario una secuencia de ADN y realiza dos búsquedas BLAST: una
en modo online, y otra en modo local.

Este ejercicio introduce un flujo de trabajo completo de comparación de ADN utilizando Python, bases de datos locales y servidores remotos.

El ejerecicio y su explicación se pueden encontrar en el siguiente enlace:

[![Ejercicio 1](https://img.shields.io/badge/Ver_Notebook-GitHub-blue?logo=github)](https://nbviewer.org/url/raquelaq.github.io/PracticaBLAST/ejercicio1.ipynb)

## Ejercicio 2. Búsqueda BLASTp con una secuencia de proteína

El segundo ejercicio amplía el análisis al dominio proteico utilizando BLASTp.
Las proteínas suelen ser más informativas que el ADN en cuanto a similitudes funcionales, por lo que BLASTp es especialmente útil en anotación genémica y análisis evolutivo.

Como en el ejercicio anterior, se hará tanto online como local.

Este ejercicio demuestra cómo implementar análisis reproducibles sin depender de servidores externos, lo cual es esencial en proyectos bioinformáticos de gran escala.

El notebook con el procedimiento y su explicación se pueden obtener en el siguiente enlace:

[![Ejercicio 2](https://img.shields.io/badge/Ver_Notebook-GitHub-blue?logo=github)](https://nbviewer.org/url/raquelaq.github.io/PracticaBLAST/ejercicio2.ipynb)

## Ejercicio 3. Búsqueda BLASTn filtrando por organismo

En este ejercicio se implementa un programa en Python que realiza una búsqueda BLASTn utilizando una secuencia de ADN obtenida desde un archivo FASTA.

Este ejercicio combina lectura de datos, ejecución remota y local de BLAST, preprocesamiento y filtrado biológico de resultados, introduciendo un pipeline más cercano a los usados en estudios reales de anotación o control de calidad de secuencias.

El notebook con el procedimiento y su explicación se puede obtener en el siguiente enlace:

[![Ejercicio 3](https://img.shields.io/badge/Ver_Notebook-GitHub-blue?logo=github)](https://nbviewer.org/url/raquelaq.github.io/PracticaBLAST/ejercicio3.ipynb)

## Ejercicio 4. Comparación entre blastn, blastp, blastx, tblastn y tblastx

En este ejercicio se realiza una búsqueda de ejemplo con cada una de las cinco utilidades principales de la suite BLAST:

- **blastn**: ADN vs ADN 
- **blastp**: proteína vs proteína 
- **blastx**: ADN traducido vs proteínas 
- **tblastn**: proteínas vs ADN traducido 
- **tblastx**: ADN traducido vs ADN traducido

Para cada herramienta se ejecuta la búsqueda online y local, permitiendo comparar rendimiento, sensibilidad y diferencias en los alineamientos obtenidos.

Este ejercicio ofrece una visión global del comportamiento de cada variante de BLAST y constituye una práctica excelente para comprender cuándo es apropiado utilizar cada herramienta en función de la naturaleza de la secuencia y el objetivo biológico.

El notebook con la implementación y el análisis se puede consultar en el siguiente enlace:

[![Ejercicio 4](https://img.shields.io/badge/Ver_Notebook-GitHub-blue?logo=github)](https://nbviewer.org/url/raquelaq.github.io/PracticaBLAST/ejercicio4.ipynb)

