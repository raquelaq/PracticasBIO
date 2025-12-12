# Análisis estructural de proteínas mediante AlphaFold y Python

Para esta práctica, se propone trabajar con AlphaFold (DeepMind, 2021), que ha transformado la predicción estructural de 
proteínas tridimensionales de alta calidad a partir únicamente de la secuencia aminoacídica.

A lo largo de la práctica, se trabajará con una proteína en concreto, y se examinarán sus características estructurales 
sin necesidad de herramientas externas complejas.

## Bloque 1 - Descarga de la secuencia desde UniProt

En este caso, se ha elegido la protenína **Beta-2-microglobulin (B2M)**.

La B2M es un componente esencial del complejo mayor de histocompatibilidad de clase I (MHC I). Su función principal es asociarse a las cadenas pesadas del MHC I y permitir su correcta estabilidad y transporte a la superficie celular, donde el complejo presenta péptidos antigénicos a los linfocitos T citotóxicos del sistema inmunitario. Además, se ha descrito que proteínas de Mycobacterium tuberculosis (como EsxA o el complejo EsxA-EsxB) pueden unirse a B2M y reducir su exportación a la membrana celular, lo que podría interferir en la presentación antigénica y facilitar la evasión inmunitaria del patógeno

- **Organismo de origen:** Esta proteína procede de **Homo sapiens (humano)**.
- **Longitud de la secuencia:** La proteína está compuesta por 119 aminoácidos.
- **Familia o dominios relevantes:** La beta-2-microglobulina pertenece a la superfamilia de las inmunoglobulinas y presenta un dominio tipo inmunoglobulina, característico de proteínas implicadas en procesos de reconocimiento y respuesta inmunitaria.

**Anotaciones importantes**

La proteína está revisada en UniProtKB/Swiss-Prot, lo que indica que su anotación es de alta calidad y está respaldada por evidencia experimental. Su existencia está confirmada a nivel proteico, y cuenta con una puntuación de anotación máxima (5/5), lo que refleja un alto grado de conocimiento y fiabilidad sobre su estructura y función.

A continuación, se puede acceder a un Notebook en el que se verifica el contenido del archivo FASTA mostrando por pantalla 
su longitud total y los 20 primeros aminoácidos de la secuencia:

PONER AQUÍ EL NOTEBOOK

## Bloque 2 -  Descarga del modelo AlphaFold

En este bloque se ha trabajado con la base de datos AlphaFold para obtener el modelo estructural predicho de la proteína
beta-2-microglobulina. Para ello, se introdujo el identificador UniProt **P61769**, desde el cual se accedió a la página
correspondiente del modelo y se descargó el archivo en formato **PDB**. 

El modelo descargado se cargó posteriormente en Python y se visualizó utilizando la librería **py3Dmol**, con el objetivo
de reproducir la visualización tridimensional mostrada en la propia web de AlphaFold. En ambos casos, el modelo representado
es el mismo, variando únicamente el entorno de visualización y el grado de control sobre el estilo gráfico.

Al comparar ambas visualizaciones, se observa que la **forma general de la proteína es coincidente**. La estructura presenta
un plegamiento compacto y globular, dominado por un núcleo de láminas β característico del plegamiento tipo
**inmunoglobulina**, lo cual es coherente con la función biológica de la proteína como componente del complejo MHC I.

En cuanto al **patrón de colores asociado a los valores de confianza (pLDDT)**, inicialmente la estructura se mostraba sin
colores debido a que py3Dmol no interpreta automáticamente esta información. Tras configurar explícitamente la visualización
para utilizar el campo **B-factor** del archivo PDB, donde AlphaFold almacena los valores de pLDDT, se obtiene un patrón de
colores equivalente al mostrado en la web de AlphaFold. Las regiones centrales de la proteína aparecen en tonos azules,
indicando una alta confianza en la predicción estructural, mientras que algunas regiones periféricas presentan colores más
cálidos, asociados a una mayor flexibilidad conformacional.

En conjunto, la comparación confirma que la visualización en Python reproduce fielmente el modelo estructural proporcionado
por AlphaFold, permitiendo interpretar tanto la arquitectura tridimensional de la proteína como la fiabilidad de la
predicción.

A continuación, se puede acceder al notebook con el código en cuestión:

PONER EL ENLACE AL NOTEBOOK

## Bloque 3 - Extraer pLDDT del PDB

En este bloque se analiza la calidad del modelo estructural predicho por AlphaFold a partir de los valores de
**pLDDT (predicted Local Distance Difference Test)** incluidos en el archivo PDB descargado. Estos valores,
que representan el nivel de confianza de la predicción estructural, se encuentran almacenados en el campo
**B-factor** de las líneas correspondientes a átomos (`ATOM`) del archivo.

Para evaluar la calidad del modelo, se extrajeron los valores de pLDDT y se asignó un valor único por residuo,
calculado como el promedio de los valores asociados a sus átomos. A partir de esta serie, se calcularon dos
indicadores básicos: el pLDDT medio de la estructura y el porcentaje de residuos con pLDDT superior a 70,
considerados como regiones predichas con alta fiabilidad.

Los resultados obtenidos muestran un **pLDDT medio de 94.04** y un **94.12 % de residuos con pLDDT > 70**, lo que
indica que el modelo presenta una **calidad global muy alta** y una elevada fiabilidad en la predicción de la
estructura tridimensional de la proteína.

El procedimiento completo, junto con el código empleado y el análisis detallado de los resultados, puede
consultarse en el siguiente notebook:

PONER EL ENLACE AL NOTEBOOK

## Bloque 4 – Gráfico de pLDDT por residuo

En este bloque se representa gráficamente la calidad de la predicción estructural del modelo AlphaFold mediante
un gráfico lineal de los valores de pLDDT por residuo. Este tipo de representación permite analizar cómo varía
la confianza de la predicción a lo largo de la secuencia de la proteína y distinguir visualmente las regiones
predichas con mayor o menor fiabilidad.

En el gráfico generado, el eje X corresponde al índice del residuo a lo largo de la secuencia, mientras que el
eje Y representa el valor de pLDDT asignado a cada residuo. Además, se incluye una línea horizontal en
pLDDT = 70, utilizada como umbral de referencia para identificar las regiones predichas con alta confianza.

El gráfico muestra que la mayor parte de la secuencia presenta valores de pLDDT elevados, generalmente muy por
encima del umbral de 70, lo que indica una alta fiabilidad de la predicción estructural en la mayor parte de la
proteína. Estas regiones corresponden principalmente al núcleo estructural de la beta-2-microglobulina, que
presenta un plegamiento estable y bien definido.

Por el contrario, se observan descensos locales de los valores de pLDDT en los extremos de la secuencia,
especialmente en las regiones N- y C-terminales, donde los valores se reducen de forma más acusada. Estas
zonas probablemente corresponden a regiones más flexibles o menos estructuradas, un comportamiento habitual
en proteínas globulares.

En conjunto, la representación gráfica confirma los resultados obtenidos en el bloque anterior y refuerza la
idea de que el modelo estructural predicho por AlphaFold para la beta-2-microglobulina presenta una calidad
global muy alta, con pequeñas regiones de menor confianza asociadas a zonas periféricas de la proteína.

El código empleado para generar el gráfico y el análisis detallado del mismo se encuentra disponible en el
siguiente notebook:

PONER EL ENLACE AL NOTEBOOK

