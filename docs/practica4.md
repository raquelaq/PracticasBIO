# Práctica 4: Análisis cuantitativo del sistema inmunitario humano 

## Introducción

El Atlas Cuantitativo del Sistema Inmunitario Humano publicado en PNAS (2023) ofrece por 
primera vez una estimación integrada del número y la masa de células inmunitarias en los 
distintos sistemas y tejidos del cuerpo humano.

El estudio combina fuentes histológicas, transcriptómicas y anatómicas (como Tabula 
Sapiens y Loyfer et al., 2023) para calcular tanto la cantidad absoluta de células como la masa 
inmunitaria total en un organismo adulto de referencia. 

El objetivo de este análisis es explorar la relación entre el número y la masa de células 
inmunitarias en los distintos tejidos corporales y cuantificar su desbalance mediante el 
índice: 

PONER AQUÍ LA FÓRMULA

Este índice permite identificar qué tejidos son “pesados pero escasos” (pocas células, pero 
grandes o voluminosas) y cuáles son “numerosos pero ligeros” (muchas células pequeñas).

Además, se evalúa un escenario alternativo simulando un aumento de macrófagos en tejido 
adiposo, análogo al observado en la obesidad, para estudiar cómo podría cambiar la 
distribución global del sistema inmunitario. 

## Descripción de los datos

Los datos se extrajeron de los ficheros suplementarios del estudio: 

- **pnas.2308511120.sd02.xlsx:** resultados consolidados del modelo. En concreto, las hojas:
  - **num_by_cell_and_system** → número total de células por tipo y sistema.
  - **mass_by_cell_and_system** → masa total (g) por tipo y sistema. 

A partir de estas tablas se generaron dos resúmenes: 

1. **MNI_por_sistema.csv**, que contiene las participaciones globales de masa, número y 
su diferencia (MNI) por sistema.
2. **Desbalance_por_tipo_celular_y_sistema.csv**, que detalla las contribuciones de cada 
tipo celular dentro de cada sistema al desbalance local (MNI_sys).

Las unidades se armonizan a nivel corporal total, por lo que las participaciones son 
proporcionales al total de células o masa inmunitaria del cuerpo humano

## Resultados e Interpretación

Para ver el Dashbooard, se puede acceder por el siguiente enlace:

[![Abrir app en Streamlit](https://img.shields.io/badge/Ver_App-Streamlit-brightgreen?logo=streamlit)](https://biodashboardgit-ys6bl6bjk7ybbxc8jnmen2.streamlit.app/)

### Desbalance masa-número por sistema

| Sistema              | Participación en número | Participación en masa | **MNI**   |
|----------------------|------------------------:|----------------------:|-----------:|
| **Others** *(incluye tejido adiposo)* | 0.050 | 0.122 | **+0.072** |
| **Liver**            | 0.028 | 0.094 | **+0.067** |
| **Lungs**            | 0.039 | 0.100 | **+0.061** |
| **Skin**             | 0.044 | 0.065 | **+0.021** |
| **GI (Tracto gastrointestinal)** | 0.029 | 0.034 | +0.005 |
| **Blood**            | 0.020 | 0.009 | −0.011 |
| **Bone Marrow**      | 0.401 | 0.301 | **−0.100** |
| **Lymphatic System** | 0.390 | 0.274 | **−0.115** |

**Interpretación:**

- Los tejidos con MNI positivo (Others, Liver, Lungs, Skin) concentran más masa relativa 
que número, indicando predominio de células grandes (macrófagos, mastocitos, 
células dendríticas).
- Los tejidos con MNI negativo (Bone Marrow, Lymphatic System) presentan muchas 
células pequeñas, principalmente linfocitos y precursores hematopoyéticos, que 
aportan gran cantidad numérica pero poca masa global.

El patrón reproduce la conclusión central del artículo: la masa inmunitaria y el número de 
células no coinciden espacialmente, lo que refleja funciones inmunes diferenciadas 
(vigilancia tisular vs. recirculación sistémica).

### Comparación global: masa vs número 

En la gráfica de dispersión (share_mass vs share_cells), los sistemas Liver, Lungs y Others 
aparecen por encima de la diagonal (más masa que número), mientras que Bone Marrow y 
Lymphatic System caen por debajo (más número que masa). 

Esto visualiza claramente la asimetría funcional:

- Los tejidos metabólicamente activos (hígado, pulmón, piel) albergan menos células 
pero de mayor tamaño y especialización.
- Los sistemas de producción o almacenamiento (médula, linfático) son 
cuantitativamente dominantes pero con células más pequeñas (linfocitos). 

### Desglose por tipo celular

El análisis intra-sistémico (MNI_sys) muestra qué tipos celulares impulsan los desbalances:

- En hígado y pulmones, los macrófagos y mastocitos dominan la masa inmunitaria, 
aunque son relativamente escasos.
- En médula ósea y sistema linfático, los linfocitos T y B aportan la mayoría del número 
pero muy poca masa. 
- En sangre, los neutrófilos son el componente más “pesado” dentro de un sistema 
globalmente “ligero”. 

### Simulación: aumento de macrófagos en tejido adiposo (escenario obesidad) 

Al multiplicar por 10 los macrófagos del sistema “Others” (que incluye tejido adiposo): 

- El MNI de “Others” aumenta bruscamente (+0.15 aprox.), desplazando el centro de 
masa inmunitaria hacia los tejidos grasos. 
- El resto de los sistemas ve reducida su participación relativa en masa, pese a que el 
número total de células no cambia sustancialmente. 

Esto reproduce el fenómeno documentado en la literatura: la obesidad provoca acumulación 
de macrófagos en el tejido adiposo, alterando la distribución y la función del sistema inmune 
a nivel corporal (mayor masa, inflamación crónica).

## Discusión y limitaciones

### Limitaciones del dataset

**Agregaciones de sistemas ("Others")**

El grupo “Others” combina varios tejidos menores, entre ellos el adiposo, pero 
también muscular, endotelial o conectivo. Por tanto, no se puede separar cuantitativamente cuánto corresponde al 
adiposo real, lo que limita la precisión de la simulación de obesidad. 

**Supuesto de propocionalidad anatómica**

El modelo se basa en un individuo promedio de 70 kg, extrapolando 
proporciones tisulares estándar. Esto ignora variabilidad por edad, sexo, raza o condición fisiológica (embarazo, 
enfermedad, obesidad, entrenamiento físico). 

**Homogenenidad dentro de los tejidos**

Se asume que las densidades celulares son uniformes dentro de cada sistema. En la realidad, hay heterogeneidad local importante (por ejemplo, distintas 
capas de la piel o zonas hepáticas). 

**Falta de dinámica temporal**

El dataset es estático; no contempla recambio celular ni migración. Muchos linfocitos circulan entre sangre, linfáticos y tejidos, lo que podría 
distorsionar la interpretación “espacial” del número. 

**Estimación de masas celulares**

Las masas promedio por tipo celular se estimaron a partir de volúmenes 
celulares medios, no de mediciones directas. Cualquier error en esos valores afecta proporcionalmente los cálculos de MNI.

**Incertidumbre no propagada en este análisis**

Aunque el Dataset S2 incluye hojas con incertidumbres 
(*_unc_by_cell_and_system), este trabajo usó las estimaciones puntuales sin 
propagar intervalos de confianza. Incluirlos podría ajustar el rango de valores especialmente en sistemas 
intermedios (GI, piel).

### Supuestos metodológicos del estudio original

- **Cierre de masa y número:** el modelo asegura que la suma de células y masa total 
coincida con estimaciones fisiológicas globales (balance corporal).
- **Escalado anatómico:** usa volúmenes de órganos y densidades inmunes derivadas de 
_Tabula Sapiens_ y de datos histológicos humanos.
- **Independencia entre tipos celulares:** se asume que las proporciones locales son 
independientes de la variación sistémica, lo que simplifica el modelo pero podría 
subestimar correlaciones (p.ej., respuesta inflamatoria multiorgánica).

### Mejoras o ampliaciones posibles

- Incorporar incertidumbre en el cálculo de MNI (con bandas o bootstrap).
- Separar el bloque “Others” en componentes adiposo, muscular, conectivo, etc.
- Extender el modelo a condiciones fisiopatológicas (obesidad, envejecimiento, 
infección). 
- Integrar datos temporales o longitudinales para representar migración de linfocitos. 
- Cruzar con transcriptómica para correlacionar masa inmunitaria y actividad genética. 

## Conclusiones

El análisis confirma que los tejidos inmunitarios más “pesados” (en masa) no son 
necesariamente los más numerosos, reflejando diferencias morfofuncionales claras: 

- Médula ósea y sistema linfático → abundancia numérica (producción y recirculación).
- Hígado, pulmones, piel y adiposo → dominancia de células voluminosas residentes 
(macrófagos, mastocitos). 

El índice MNI es una métrica intuitiva y robusta para distinguir peso funcional frente a 
cantidad celular. 

La simulación muestra que alteraciones locales (como obesidad) pueden redistribuir el 
balance masa–número a escala corporal. 

Sin embargo, las limitaciones anatómicas y estadísticas del dataset aconsejan interpretar los 
resultados como tendencias promedio, no como valores absolutos para individuos 
concretos. 