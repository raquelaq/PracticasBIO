# Práctica 3 - Algoritmo de De Bruijn

En esta tarea se aborda el proceso de ensamblaje de secuencias de ADN a partir de fragmentos cortos obtenidos por secuenciación.
El objetivo es reconstruir la secuencia original utilizando la metodología basada en grafos de De Bruijn, una de las 
técnicas más empleadas en la genómica moderna para el ensamblaje de genomas.

A lo largo de la tarea se trabaja con diferentes conjuntos de fragmentos (lecturas o _reads_), representados por el alfabeto 
{A,C,G,T}, y se aplican los pasos fundamentales del método, como la generación de los k-mers, la consutrucción del grafo de
De Bruijn, y la búsqueda del camino euleriano.

El propósito de la tarea es comprender cómo los algoritmos de grafos se aplican en el contexto biológico, y cómo permiten 
transformar datos de secuenciación en una representación coherente del genoma original.

## Cuestión 1

Imagina que estás trabajando en un proyecto de investigación genómica y has recibido datos de secuenciación de ADN fragmentado.
La secuenciación te ha proporcionado una lista de lecturas cortas, cada una de longitud 4. La tarea consiste en ensamblar 
estas lecturas cortas para reconstruir la secuencia original u lizando un grafo de De Bruijn. Se partirá de los **3-mers**
de cada uno de ellos.

Los fragmentos secuenciados son:

- GACG
- CGTT
- TTAC
- ACTA
- TATG
- TGTG

### División en fragmentos, prefijos y sufijos 

**Se hará a partir de las lecturas _k-mers_ (de longitud 3) para modelar las superposiciones de las lecturas y generar el 
ensamblaje de la secuencia.**

El algoritmo de Bruijn no compara los fragmentos completos entre sí, ya que iría muy lento, así que los divide en pedazos
aún más pequeños llamados _k-mers_.

Por tanto, se comienza el ejercicio separando los fragmentos en _k-mers_ de longitud 3:

![Generación de los k-mers](images/tabla1.png)
*Tabla 1. Proceso de generación de los k-mers*

Como se puede observar en la **Tabla 1**, no hay ningún _k-mer_ repetido, por lo que ahora se procede a la **división de los _k-mers_
 en prefijos y sufijos**. 

Este paso es necesario para poder llegar a construir el grafo de De Bruijn, ya que cada nodo en el grafo representa un
fragmento de longitud _k - 1_. Por tanto, en este ejercicio cada nodo representará un fragmento de longitud _3 - 1 = 2_.

![Prefijos y Sufijos](images/tabla2.png)
*Tabla 2. Proceso de generación de los prefijos y sufijos*

En la **Tabla 2** se pueden ver los prefijos y sufijos resultantes para cada grupo de _k-mers_. Esto surge porque cada _k-mer_
crea una conexión (arista) entre dos nodos:

- El nodo de **inicio**, formado por las primeras _k - 1_ letras del _k-mer_ (prefijo)
- El nodo de **fin**, formado por las últimas _k - 1_ letras del _k-mer_ (sufijo).

### Construcción del grafo de De Bruijn

Sabiendo lo anterior, el conjunto de nodos que conformará el grafo de De Bruijn será: {GA, AC, CG, GT, TT, TA, CT, AT, TG}, y el grafo
de De Bruijn será el que se puede ver en la Figura 1:

![Grafo de De Bruijn](images/grafo1.png)
*Figura 1. Grafo de De Bruijn*

### Camino Euleriano

Ahora que el grafo de De Bruijn está construido, se podrá comprobar si existe un camino euleriano para poder reconstruir 
la secuencia.

Un **camino euleriano** es un recorrido dentro de un grafo que **pasa exactamente una vez por cada arista**. En un grafo 
dirigido, cada nodo puede tener:

- **Grado de salida:** que correspone al número de aristas que salen del nodo (flechas)
- **Grado de entrada:** que es el número de aristas dirigidas que entran al nodo

Las condiciones que deben cumplirse para que existe un camino euleriano son:

1. **Salida:** como máximo un nodo con un grado de salida mayor en 1 al grado de entrada
2. **Entrada:** como máximo un nodo con un grado de entrada mayor en 1 al grado de salida
3. **Resto de nodos:** todos los demás nodos deben tener el mismo número de entradas y salidas
4. **Conectividad:** todos los nodos deben estar conectados

Por tanto, se pasa a comprobar si los nodos del camino cumplen con dichas condiciones para seguir un camino euleriano:

- **GA:** entrada = 0, salida = 1 → Nodo de inicio (salida = entrada + 1)
- **AC:** entrada = 2, salida = 2
- **CG:** entrada = 1, salida = 1
- **GT:** entrada = 2, salida = 2
- **TT:** entrada = 1, salida = 1
- **TA:** entrada = 2, salida = 2
- **CT:** entrada = 1, salida = 1
- **AT:** entrada = 1, salida = 1
- **TG:** entrada = 2, salida = 1 → Nodo de fin (entrada = salida + 1)

El resto de nodos están equilibrados (entrada = salida), y el grafo está conectado por las aristas relevantes.

**Camino euleriano:** GA → AC → CG → GT → TT → TA → AC → CT → TA → AT → TG → GT → TG

Por tanto, se cumple con las condiciones indicadas, así que existe un camino euleriano y se puede hacer la reconstrucción.

### Reconstrucción

En grafos de De Bruijn, se reconstruye tomando el primer nodo y luego añadiendo la última letra de cada nodo siguiente. Por 
tanto, el resultado de la reconstrucción es **GACGTTACTATGTG**.

Para comprobar que la reconstrucción está bien, es tan sencillo como observar que todas las lecturas originales aparecen
como subcadenas de la secuencia ensamblada (Figura 2).

![Comparación](images/comparacion_lecturas_reconstruccion_1.png)
*Figura 2. Subcadenas de la reconstrucción*

El uso del grafo de De Bruijn ha permitido representar de manera eficiente las relaciones de superposición entre los 
fragmentos de ADN, facilitando el ensamblaje de la secuencia original. Este procedimiento ilustra cómo los algoritmos 
basados en grafos son una herramienta esencial en la bioinformática moderna, ya que permiten transformar grandes 
volúmenes de datos de secuenciación en representaciones precisas del genoma, optimizando tanto el tiempo de cómputo como
la fiabilidad del ensamblaje.

## Cuestión 2

Estás trabajando en un proyecto de inves gación genómica y enes a tu disposición fragmentos de ADN obtenidos mediante un
proceso de secuenciación de próxima generación (NGS). La tarea es ensamblar estos fragmentos y reconstruir la secuencia 
original de ADN usando un grafo de De Bruijn.

Los fragmentos secuenciados son:

- AGTC
- GTCA
- TCAG
- CAGT
- AGTT
- GTTG

Se seguirán los mismos pasos que en el ejercicio anterior:

### División en prefijos y sufijos 

Esta vez, se dividirá cada fragmento (lectura) en un prefijo de longitud _k-1=3_ y un sufijo _k-1=3_. 

El resultado es el que se puede observar en la **Tabla 3**:

![Prefijos y Sufijos](images/tabla3.png)
*Tabla 3. Generación de los prefijos y sufijos*

### Construcción del grafo de De Bruijn

Los prefijos y sufijos el conjunto de nodos que conformará el grafo de De Bruijn será: {AGT, GTC, TCA, CAG, GTT, TTG},
y el grafo de De Bruijn será el que se puede ver en la Figura 3:

![Grafo de De Bruijn](images/grafo2.png)
*Figura 3. Grafo de De Bruijn*

### Camino Euleriano

Con el grafo de De Brujin construido, se pasa a comprobar si existe o no un camino euleriano para reconstruir la secuencia.

Primero, se comprueba los nodos cumplen o no con las condiciones necesarias:

- **AGT:** entrada = 1, salida = 2 → Nodo de inicio (salida = entrada + 1)
- **GTC:** entrada = 1, salida = 1 
- **TCA:** entrada = 1, salida = 1
- **CAG:** entrada = 1, salida = 1
- **GTT:** entrada = 1, salida = 1
- **TTG:** entrada = 1, salida = 0 → Nodo de fin (entrada = salida + 1)

El resto de nodos están equilibrados (entrada = salida), y el grafo está conectado por las aristas relevantes.

**Camino euleriano:** AGT → GTC → TCA → CAG → AGT → GTT → TTG

Por tanto, se cumple con las condiciones indicadas, así que existe un camino euleriano y se puede hacer la reconstrucción.

### Reconstrucción

El resultado de la reconstrucción es **AGTCAGTTG**.

Para comprobar que la reconstrucción está bien, se hace lo mismo que se hizo anteriormente en la Figura 2.

![Comparación](images/comparacion2.png)
*Figura 4. Subcadenas*

Como se ve en la **Figura 4**, todas las lecturas originales aparecen como subcadenas en la secuencia ensamblada.

Con De Bruijn modelamos las superposiciones locales (k−1) y reducimos el ensamblaje a encontrar un camino euleriano que
recorra cada lectura exactamente una vez. Verificar los grados de entrada/salida identifica el posible inicio y final,
y la reconstrucción se obtiene concatenando un carácter por arista. Este enfoque es robusto y escalable: admite 
multiplicidades, ramas y bulbos cuando hay errores o repeticiones, y sirve de base para ensambladores modernos.

## Cuestión 3

En este último ejercicio se aborda un caso más complejo del ensamblaje genómico mediante grafos de De Bruijn.

A diferencia de los anteriores, aquí el objetivo no es solo reconstruir la secuencia original, sino identificar los problemas que aparecen cuando existen repeticiones o errores en las lecturas, los cuales hacen que el grafo presente ambigüedades y no sea posible obtener un ensamblaje único.

Los fragmentos secuenciados son:

- AGTT
- GTTG
- TTGA
- TGAC
- GACG
- ACGA
- CGAA
- GAAC
- AACG

### División en fragmentos, prefijos y sufijos 

Cada fragmento tiene longitud k = 4, por lo que se divide en un prefijo de longitud 3 (k−1) y un sufijo de longitud 3 (k−1).
De esta forma, cada lectura genera una arista dirigida desde el nodo correspondiente a su prefijo hacia el nodo de su sufijo.

# insertar tabla

Con estos pares se construye el conjunto de nodos:
{AGT, GTT, TTG, TGA, GAC, ACG, CGA, GAA, AAC}

### Construcción del grafo de De Bruijn

Cada arista conecta un prefijo con su sufijo, representando las posibles superposiciones entre lecturas. 

En la Figura 5 se muestra el grafo dirigido correspondiente:

# insertar grafo brujin

### Camino Euleriano

Se comprueban los grados de entrada y salida de cada nodo, comprobando si se cumplen las condiciones previamente mencionadas para que sea posible trazar un camino euleriano.

Nodo	Entradas	Salidas
AGT	0	1
GTT	1	1
TTG	1	1
TGA	1	1
GAC	1	1
ACG	2	1
CGA	1	1
GAA	1	1
AAC	1	1

El nodo AGT tiene una salida más que entradas, por lo que es el posible inicio.

El nodo ACG tiene dos entradas y una salida, generando una bifurcación en el grafo.

A pesar de que el grafo presenta un camino euleriano aparente, que sería el siguiente: 

AGT → GTT → TTG → TGA → GAC → ACG → CGA → GAA → AAC → ACG

E nodo ACG recibe dos aristas de entrada (desde GAC y desde AAC). Esto significa que existen dos posibles rutas que convergen en el mismo punto, generando ambigüedad sobre cuál es la secuencia correcta

El grafo de De Bruijn, por sí solo, no puede decidir entre estas alternativas, ya que solo modela solapamientos de longitud k−1 sin incluir información contextual adicional (como cobertura o pares de lectura).

Por este motivo, no es posible garantizar el ensamblaje de la secuencia original.

## Preguntas adicionales

### 1. ¿Por qué el grafo de De Bruijn no puede resolver este problema?
 Porque las lecturas contienen repeticiones locales que generan nodos con múltiples aristas entrantes o salientes. El grafo pierde la información sobre la posición exacta de las repeticiones, produciendo caminos alternativos que son indistinguibles entre sí.

### 2. ¿Qué sucede cuando existen múltiples caminos entre dos nodos?
 Aparecen bifurcaciones o bucles en el grafo. El ensamblador no puede saber qué camino seguir, por lo que puede generar contigs fragmentados o ensamblajes erróneos si se elige un camino arbitrariamente.

### 3. ¿Cómo se puede ajustar el grafo para manejar estas ambigüedades?

Algunas posibilidades serían: 
- Aumentar el valor de k para reducir repeticiones.
- Usar lecturas emparejadas (paired-end) o de mayor longitud.
- Incorporar pesos o frecuencias de cobertura en las aristas para discriminar los caminos más probables.

Por ejemplo, si se decidiera aumentar el valor de k (k=5), se obtendrían lecturas de longitud ≥5. Con la secuencia compatible con las lecturas dadas, los **5-mers** son:
AGTTG, GTTGA, TTGAC, TGACG, GACGA, ACGAA, CGAAC, GAACG.

### Grafo de De Bruijn (nodos = 4-mers)

Aristas:

* AGTT→GTTG
* GTTG→TTGA
* TTGA→TGAC
* TGAC→GACG
* GACG→ACGA
* ACGA→CGAA
* CGAA→GAAC
* GAAC→AACG

Grados:

* **AGTT** out=1,in=0 → inicio
* **AACG** out=0,in=1 → fin
* Resto equilibrados (in=out=1)

### Camino euleriano y ensamblaje

Único camino: AGTT→GTTG→TTGA→TGAC→GACG→ACGA→CGAA→GAAC→AACG.
Reconstrucción: **AGTTGACGAACG**.

El nodo ambiguo de k=4, **ACG** (in=2), se descompone en nodos distintos con k=5 (**GACG** y **AACG**). La bifurcación desaparece y el camino queda determinado, resultando en el ensamblaje único sin ambigüedad.



## Conclusión

En esta práctica se demuestra que el grafo de Bruijn es una herramienta potente para representar las relaciones de solapamiento entre fragmentos, pero su eficacia depende de la complejidad de la secuencia.

Cuando hay regiones repetitivas o errores en la lectura, el grafo genera ambigüedades que impiden reconstruir de sin errores la secuencia original.

Por ello, los ensambladores reales combinan esta representación con estrategias complementarias (como cobertura, pares de lectura y análisis estadístico) para obtener un ensamblaje genómico fiable.