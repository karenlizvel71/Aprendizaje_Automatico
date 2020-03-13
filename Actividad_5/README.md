# ACTIVIDAD 5
## IMPLEMENTACIÓN DE ALGORITMOS GENÉTICOS
### Procesos de Optimización

## Integrantes:
		Ana María Uran González
		Karen Lizeth Velásquez Moná
								
### I.	CONTEXTUALIZACION

La Optimización se ha convertido en una herramienta fundamental para la toma decisiones, esta se enfoca en seleccionar la mejor opción que permita cumplir con los objetivos planteados los cuales están acompañados de una serie de condiciones o limitaciones propias del problema, buscando generar valores óptimos en pro de beneficiar una decisión, lo cual permitirá maximizar o minimizar el o los objetivos.
Matemáticamente, los modelos de optimización buscan darle solución a una función objetivo, a través del análisis de la dominancia; esta permite identificar basado en los objetivos definidos del problema, la clasificación de diferentes soluciones basado en los planteamientos de este.[1]

Bajo el concepto de dominancia se indicará que una solución x^((1))   es mejor que x^((2)) en todos los objetivos y x^((1))   es mejor que x^((2)) en al menos un objetivo.
Basado en la dominancia, los algoritmos genéticos permiten generar n iteraciones sobre un problema hasta encontrar la mejor combinación que permita llegar al objetivo de manera óptima; sin embargo, estos algoritmos pueden optimizar un solo objetivo o múltiples objetivos.
								
El desarrollo de esta actividad permite ejecutar e identificar la optimización de un problema para múltiples objetivos, permitiendo así evidenciar a través de un diagrama de Pareto la manera como se maximiza un objetivo y se minimiza otro; es decir, como mientras un objetivo se beneficia el otro se perjudica; cuya solución será generada basado en el algoritmo genético NSGA II.
Cuando estamos hablando de problemas multi objetivo es importante tener claro que pueden existir n cantidad de funciones multi objetivo, z cantidad de variables y i restricciones

Para este ejercicio se buscará un Pareto que halle la maximización de un objetivo y la minimización de otro, evidenciando el impacto y fricción que genera uno sobre el otro.

### II. ALGORITMO NSGA II

El algoritmo NSGA-II (Elitist Non-Dominated Sorting Genetic Algorithm) fue propuesto por Deb en el año 2000.[2] Este es un algoritmo, busca optimizar problemas multi objetivo a través de una clasificación de acuerdo a un nivel de no dominación, permitiendo hallar un conjunto de soluciones óptimas (en gran medida conocidas como soluciones óptimas de Pareto), en lugar de una sola óptima solución.
Este algoritmo contiene unos pasos claves los cuales serán descritos a continuación:
1.	Definición de soluciones codificadas en forma binaria llamada (“Cromosomas”). [3]
2.	Crea una población de hijos (Q) a través de cruce y mutación.[3]
3.	Combina P y Q y puntúa para todos los objetivos.[3]
4.	Identifica el primer frente de Pareto (F1); es decir, todas las soluciones donde no hay otras soluciones que sean al menos igualmente buenas en todos los objetivos y mejores en al menos un objetivo. [3]
5.	Si F1 es mayor que la solución máxima permitida, reduzca el tamaño de F1 mediante "crowding selection”. .3]
6.	Si F1 es más pequeño que el tamaño de población requerido repita la selección de Pareto (después de eliminar el seleccionado ya seleccionado). Este nuevo conjunto de soluciones es F2. Si el número total de soluciones seleccionadas es mayor que el tamaño de población máximo permitido, reduzca el tamaño de solo la última selección (en este caso F2) para que el número de todas las soluciones seleccionadas sea igual al tamaño de población máximo permitido.[3]
7.	Repita la selección de Pareto hasta alcanzar el tamaño de población requerido (y luego reduzca el último frente de Pareto seleccionado mediante "selección de hacinamiento" según sea necesario para evitar exceder el tamaño de población máximo permitido). [3]
8.	Los frentes de Pareto seleccionados para la nueva población, P.
9.	Repita desde (2) durante el número requerido de generaciones o hasta que se alcance algún otro criterio de "detención".[3]
10.	Realice una selección final de Pareto para que la población final informada sea solo la del primer frente de Pareto.[3]

### III.	APLICACIÓN  

#### Problema multiobjetivo

Actualmente una entidad bancaria busca generar optimización que permita maximizar la colocación de sus créditos y una minimización del riesgo de fraude. Para este caso cabe resaltar que en el sistema financiero la colocación de mayor número de créditos genera una exposición mayor al riesgo de fraude; sin embargo, se trabajara en este caso bajo este supuesto, ya que las entidades pueden tener herramientas alternas que permitan también mitigar los riesgos, por lo cual se hace la clarificación del supuesto con el que se partirá el ejercicio.

Minimizar  ⁡〖y_1=f_1 (x)=Riesgo de fraude (Casos) 〗
Maximizar  ⁡〖y_2=f_2 (x)=Colocación de créditos 〗

Una de las medidas que utiliza la industria para calcular la afectación que se da por fraude vs la generación de créditos corresponde a los puntos base, los cuales están estrechamente relacionados y permiten medir la proporción de los créditos colocaos vs la evolución del fraude:

PB=(Número de Créditos)/(Número de fraudes)  

De acuerdo con lo anterior y partiendo de un ejercicio académico se tiene un histórico de 1000 observaciones que contiene el número total de créditos colocados y los puntos base generados, así como los fraude generados y los puntos base asociados a este.



### Restricciones – parámetros iniciales:
	Con el fin de realizar un exhaustivo estudio se tendrá una población igual a 150, los cuales serán la solución inicial.
	Se permitirá al algoritmo generar máximo 501 iteraciones con el fin de que este genere combinaciones que permitan conocer a fondo el problema.
	Se establecerá un mínimo valor igual a 10 el cual hace símil con los puntos base explicados y es el mínimo número que se espera.
	Se establecerá un máximo valor igual a 1000 el cual hace símil con los puntos base explicados y es el mínimo número que se espera.

### Mutación:
Se define un % de mutación aleatorio, esto permite generar dinamismo dentro del algoritmo.

### Algoritmo:
	Como se mencionaba en un principio el algoritmo partirá de un número ya determinado de generaciones y una población que aduce a las posibles soluciones.
	Una vez son analizadas las posibles soluciones en las dos funciones objetivos, el algoritmo realiza el cálculo de la no dominancia, para el cual si la posición i es comparada con otra posición se indicará la no dominancia y esta será guarda lista de los no dominados.
	Posteriormente se inicia con la creación de poblaciones y posibles soluciones donde se realiza los cálculos basado en las funciones preestablecidas, y nuevamente se realiza el análisis de la no dominancia, evaluando la distancia de crowding. 
	Estos procesos son realizados hasta encontrar el dominante o no dominando, para llevar al diagrama de Pareto,
Una vez se realiza la ejecución del algoritmo podemos evidenciar que para cada generación el algoritmo se compara hasta con el número de población y inicia a establecer en cada generación la no dominancia.
 
## Resultado
Como resultado podemos observar en la línea azul los genes no dominados donde podemos evidenciar que cumple con el requerimiento inicial de nuestro problema, ya que es posible evidenciar que a medida que los fraude disminuyen la cantidad de colocación de créditos aumenta, donde podemos evidenciar los puntos óptimos para el ejercicio ya que se tiene en los extremos.




