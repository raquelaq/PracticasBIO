# Práctica de manejo de ficheros con Biopython

## Introducción

El objetivo de esta práctica es aprender a manejar ficheros de secuencias en formato FASTA y desarrollar un flujo de trabajo básico de bioinformática utilizando **Biopython**. A partir de varios genes humanos almacenados como secuencias de ADN codificante (CDS), se realizará un proceso automatizado que incluye:

- Lectura de múltiples ficheros FASTA.
- Cálculo del **contenido GC** de cada secuencia.
- Traducción del ADN a **secuencias de proteínas**.
- Generación de archivos FASTA de salida con las proteínas obtenidas.

Este análisis se aplica a cinco proteínas humanas de relevancia biológica: **insulin**, **hemoglobin**, **myoglobin**, **albumin** y **keratin**. Cada una presenta características funcionales y composicionales distintas, lo que permite observar variabilidad real en los datos biológicos.

La práctica se estructura en varias etapas claramente definidas:

### 1. Preparación de los datos
Se descargaron las secuencias codificantes (CDS) de los genes seleccionados desde bases de datos públicas del NCBI.  

Cada proteína se guardó como un archivo FASTA independiente dentro de la carpeta `ficheros/`.

### 2. Implementación del pipeline
El código se organiza en funciones específicas para facilitar la modularidad:

- **`leer_fasta()`**: carga un archivo FASTA y devuelve una lista de registros.
- **`calcular_gc()`**: calcula el porcentaje de GC de una secuencia de ADN.
- **`traducir_secuencias()`**: convierte secuencias de ADN en proteínas.
- **`guardar_fasta()`**: guarda los resultados de la traducción en un nuevo archivo FASTA.
- **`pipeline()`**: coordina todo el proceso para todos los genes seleccionados.

### 3. Cálculo de GC
Para cada gen se calcularon los valores de GC de todas sus isoformas, permitiendo comparar entre proteínas con funciones y estructuras distintas. Posteriormente, las secuencias se tradujeron y guardaron como FASTA en la carpeta `outputs/`.

### 4. Interpretación de resultados
Los valores de GC observados mostraron variabilidad entre proteínas:

- **Insulina**: GC alto (~64.56 %), característico de un gen corto y altamente conservado.  
- **Hemoglobina**: GC medio-alto (~56 %), propio de genes fuertemente expresados.  
- **Mioglobina**: GC estable y relativamente alto (~57 %), coherente con su especialización funcional.  
- **Albúmina**: GC más bajo (~43 %), reflejando una secuencia larga y diversa.  
- **Queratina**: GC medio-alto (~54 %), típico de proteínas estructurales epiteliales.

Los archivos de salida confirmaron traducciones correctas (marco de lectura completo y presencia de codón de parada).

## Finalidad del trabajo

Este proyecto demuestra cómo construir un flujo de análisis reproductible y escalable para procesar grandes cantidades de datos biológicos. Además, introduce conceptos clave de bioinformática como el manejo de formatos FASTA, composición nucleotídica, traducción in silico y la organización estructurada de código para análisis automatizados.

El resultado final es un pipeline sencillo pero robusto que permite procesar múltiples genes con un solo comando, generando salidas limpias y listas para análisis posteriores.


Se puede ver el notebook con la implementación en este enlace:

[![Transcripción](https://img.shields.io/badge/Ver_Notebook-GitHub-blue?logo=github)](https://nbviewer.org/url/raquelaq.github.io/PracticasBIO/notebooks/PracticaFicheros.ipynb)