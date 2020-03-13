# ACTIVIDAD 4
## IMPLEMENTACIÓN DE ALGORITMOS NO SUPERVISADO

## Integrantes:
		Ana María Uran González
		Karen Lizeth Velásquez Moná


# INTRODUCCIÓN

Actualmente, la necesidad de encontrar grupos de patrones o características que permitan describir un problema ha dado a pie al aprendizaje no supervisado, el cual es un método de aprendizaje automático en el que un modelo se ajusta a las observaciones sin tener un conocimiento previo de los datos. En el desarrollo de esta actividad, se tendrá la prioridad de conocer y aplicar esta técnica a través de algoritmos de agrupamiento (Clustering), los cuales generan una agrupación a una serie de vectores de acuerdo con un criterio que típicamente se dan por distancias o medidas de similitud entre los datos. 

## 1.	Modelo no supervisado para variables Categóricas

Muchos de los problemas encontrados en la industria y los datos recogidos por las mismas se centran en datos consolidados que contemplan variables que representan características, por lo cual es un reto encontrar un algoritmo de agrupación enfocado en este tipo de variables que permitan generar entendimiento del problema, por lo anterior nuestra primera aplicación se centra en algoritmo de agrupamiento para variables categóricas.

## 1.1.	Objetivo de la iteración

Entender, desarrollar y aplicar modelo k-modes el cual es una adaptación del modelo de k- means cuyos centroides se basan en la frecuencia de las variables categóricas. Entender este problema, permite conocer soluciones implementadas para problemas que se centran en datos categóricos.

## 1.2.	Entendimiento del problema

Medellín en la actualidad enfrenta diferentes problemas de inseguridad entre los que se encuentra homicidios, hurtos, y tráfico de drogas. De acuerdo con encuestas realizadas en la ciudad de Medellín (Medellín como vamos) el 20% de los casos de inseguridad está asociada a hurtos el cual involucra hurto a personas, vehículos, bienes y negocios. La ciudad de Medellín cuenta con una línea de atención y un escuadrón de policías cuyo objetivo es recibir y atender las denuncias de este tipo de casos; por lo que esta problemática hace necesaria idear estrategias que permitan entender las diferentes denuncias que hace la ciudadanía con el fin de que dicho entendimiento, sea la base para el despliegue de diferentes acciones que permitan la mitigación del problema.


## 1.3.	Datos 

Para cumplir el objetivo planteado anteriormente, se parte de un dataset de hurtos denunciados realizados en Medellín durante el año 2019, el cual se componen de 60579 denuncias con 41 variables. Bajo análisis previo se eliminan algunas variables las cuales no aportan al modelo ya que tienen un mismo valor definido.

Se realiza un proceso de exploración, donde se establecen algunas variables que no son objetivo del problema, ya que no cuenta con una sola categoría asociada. Adicionalmente, se realizan análisis descriptivos de las variables donde se establece nuevos grupos que las suplen ya que en algunas de las variables se encontraron más de 200 categorías, el procedimiento se encuentra descrito tanto en el informe de la selección de características como el notebook.

De acuerdo con el procedimiento anterior la base para aplicar el método de k modes contara con las siguientes 16  variables:

-	Jornada	
-	Modalidad	
-	Sexo	
-	Rango_Edad	
-	Rango_Edad_Pisc	
-	Comuna	
-	Grupo_Lugar
-	Valor_Hurto	
-	Medio_Transporte_Agresor	
-	Sede_Receptora	
-	Arma_Medio	
-	Grupo_bienes	
-	Grupo_dia1	
-	Grupo_dia2	
-	Grupo_hora	
-	Grupo_hora2

A través de la función astype("category").cat.codes de pandas estas variables fueron llevadas a categorías de tipo numérico, con el fin de que se conviertan bajo un esquema homogéneo la entrada del algoritmo.




 
  
  ## 1.1. Desarrollo del modelo K modes


  
 






 



Con el fin de tener un análisis sobre
variables categóricas teniendo como objetivo encontrar grupos que demuestren
homogeneidad en nuestro set de datos y aunque actualmente los métodos de aprendizaje
no supervisados que buscan generar agrupaciones se enfocan en variables no
categóricas, nuestro enfoque será entender y utilizar método que permita
generar agrupaciones en dataset donde predomina las variables categóricas; de
acuerdo a lo anterior, la aplicación se centrara en la moda de los datos cuyo
algoritmo es representado como K modes, este utiliza un coeficiente de
disimilitud para medir la proximidad de los clúster. Por lo anterior, se adapta
el algoritmo de k means a la moda dado que por las características del set de
datos se utilizará una medida de disimilitud. 



 



El algoritmo k means presenta un
correcto funcionamiento para datos numéricos, el enfoque tradicional para
convertir datos categóricos en valores numéricos en ocasiones no produce
resultados adecuados donde son dominantes los datos categóricos.[2] Por
lo anterior se decidió explorar el algoritmo k modes (Huang, 1997b)
el cual tiene como objetivo hallar una medida de disimilitud, modas en lugar de
medias y cluster basados en frecuencia que ejecutan un proceso cuyo k aporta en
la minimización de la función de costo de agrupamiento.



 



El método está basado en un conjunto  al cual pertenecen n individuos
descritos por p variables categóricas que para nuestro ejercicio
contamos con un p = 24 correspondiente a Xp variables. A partir de esto
se define la moda para cada variable donde se minimiza la distancia entre la
moda elegida y el valor de la variable. [3]



 



Este análisis busca reunir los
individuos que más se parezcan y para esto naturalmente se asocian los
individuos que se parecen más el cuándo coinciden en un número alto de
categorías 



 



 es la mínima.



 



Este método requiere definir un número
k óptimo de modas, aunque para nuestro ejercicio realizaremos iteraciones sobre
los diferentes k es importante resaltar que al iniciar estos k funcionan como
núcleos transitorios. Uno a uno se realiza se asigna cada elemento al conjunto
original del grupo más cercano en términos de disimilaridad y se calcula la
moda para ese grupo y cada elemento se compara con los ciclos anteriores, el
algoritmo para solo hasta que no evidencie cambios.

## 1.4.1.	Algoritmo K Modes Python

Actualmente Pyhton contiene el algoritmo implementado llamado K modes, el cual será utilizado para el desarrollo del ejercicio.

##  1.4.1.1.	Parámetros:

-	Medida de disimilitud:

Para este caso la inicialización del algoritmo estará dada por la medida de disimilitud Huang. 

Esta medida de disimilitud se define como la discrepancia entre dos objetos X y Y las cuales deberán ser dos variables categóricas, mientras existan un número menor de discrepancias se consideran que tienen mayor relación los objetos.[1]

- Cálculo del costo

Basado en lo anterior, como estamos trabajando con una medida de disimilitud para variables categóricas, se define una función de costo la cual tiene como objetivo calcular el costo total P contra todo el conjunto permitiendo hallar una cantidad de clusters óptima (k) que permita tener un proceso computacional eficiente, debido que este tipo de medidas requieren evaluar la coincidencia para resolver P_!, utilizando frecuencias para grupos en lugar de medias y la selección de modas.

-	Elección de mejor K

De acuerdo con lo anterior se ejecuta el modelo con el fin de realizar iteraciones que permitan minimizar el costo con el fin de hallar un k óptimo.

Se evidencia que existe un quiebre en el costo computacional en un k = 4 donde para k = 5 se mantiene la tendencia a la baja y posteriormente se evidencia de nuevo un quiebre en un k= 6. 

Adicionalmente se utiliza el método de la silueta que ofrece sklearn, el calcula utilizando la distancia media dentro del grupo (a) y la distancia media más cercana al grupo (b) para cada muestra. El coeficiente de silueta para una muestra es (b - a) / max (a, b). Para aclarar, b es la distancia entre una muestra y el grupo más cercano del que la muestra no forma parte, devolviendo un promedio, el mejor valor es 1 y el peor es -1. Los valores cercanos a 0 indican grupos superpuestos. Los valores negativos generalmente indican que se ha asignado una muestra al grupo incorrecto, ya que un grupo diferente es más similar.[3]

basado en esto se elige el 4 cluster y se ejecuta algoritmo.

## Análisis de Grupos
De acuerdo con lo anterior se obtiene un resultado de 4 grupos, dado que el objetivo de este tipo de algoritmos es caracterizar los datos se realiza a continuación un análisis descriptivo de los resultados.

### Clúster 0:
Resumen de descripción
Clúster con el 30.6% de los datos
Personas víctimas de hurtos en la madrugada
Modalidad de robo atraco y cosquilleo
Hurto cometido a hombres y mujeres
Personas víctimas entre los 18 y 28 años
Victimarios jóvenes entre los 18 y 29 años
Hurtos cometidos en la candelaria
Denuncios realizados en sede policial de la candelaria
Por lo general el victimario no utiliza arma
Los principales elementos hurtados son tecnología, documentos y dinero
Días de hurto entre los 15 y 23 días del mes
Perteneces también hurtos entre los días 1,2,10,12,18,21,22,23,27,28 del mes
Los hurtos son cometidos en horas mayores a las 18 p.m y menores a las 7 a.m
Algunas horas foco horas foco 20,19,21.

### Clúster 1:
Resumen de descripción:
con el 25,4% de los datos

Personas víctimas de hurtos en la tarde
Modalidad de robo atraco
Hurto cometido a hombre
Personas víctimas entre los 29 y 38 años
Victimarios jóvenes entre los 29 y 39 años
Hurtos cometidos en la Laureles
Denuncios realizados en sede policial de la Laureles
Por lo general el victimario arma de fuego.
Los principales elementos hurtados son dinero, tecnología y vehículos
Días de hurto últimos 7 días del mes
Hurtos entre los días 3,13,14,17,19,20,24,25,26,29,31 del mes
Los hurtos son cometidos en horas mayores a las 18 p.m y menores a las 12 p.m y 18 p.m
Algunas horas foco horas foco 6,14,8,5,13,3

###Clúster 2:
Resumen de descripción:
Clúster con el 19,4% de los datos
Personas víctimas de hurtos en la mañana
Modalidad de robo descuido
Hurto cometido a mujeres
Personas víctimas entre los 39 y 45 años
Victimarios jóvenes entre los 40 y 59 años
Hurtos cometidos en la Candelaria
Denuncios realizados en sede policial de la Candelaria
Por lo general el victimario no uso de arma
Los principales elementos hurtados son tecnología, dinero, vehículos y documento
Días de hurto primeros 15 días del mes
Perteneces también hurtos entre los días 2,4,5,6,8,9,11,15,16,30 del mes
Los hurtos son cometidos en horas mayores las 7 a.m y 12 p.m

### Clúster 3:
Resumen de descripción:
Clúster con el 24,6% de los datos
Personas víctimas de hurtos en la noche
Modalidad de robo atraco
Hurto cometido a hombres
Personas víctimas entre los 18 y 24 años
Victimarios jóvenes entre los 18 y 29 años
Hurtos cometidos en la Candelaria y Poblado
Denuncios realizados en sede policial de la Candelaria y Laureles
Por lo general el victimario el no uso de arma seguido de arma cortopunzante y arma de fuego.
Los principales elementos hurtados son tecnología, dinero, vehículos y vehículos
Días de hurto primeros 15 días del mes
Perteneces también hurtos entre los días 2,4,5,6,8,9,11,15,16,30 del mes
Los hurtos son cometidos en horas mayores a las 18 p.m
Algunas horas foco horas foco 22,2,4,0,1,23

## Conclusiones
Para elegir un k óptimo el método de k modes utiliza según la literatura la medida del costo, sin embargo, al combinar o comparar esta medida con otras como métodos que miden la cohesión se evidencia que las métricas podrían no ser tan eficientes, sin embargo, ante tantas categorías corresponde a un método adaptado que es útil al momento de generar clasificación.
En nuestro ejercicio si bien se generó una descripción correcta de las características predominaron datos con clases que representan una gran proporción en el set de datos, como lo son la Comuna de la Candelaria donde se concentran los mayores robos en la ciudad de Medellín, lo que se convierte en una de la razón para que la métrica de la silueta genere un valor negativo y bajo nuestro k = 4 que tiende a cero, tener este tipo de datos podrían superponer los grupos.
Los datos categóricos deben ser tratados bajo medidas de disimilitud, ya que de estos deben ser comparado bajo este tipo de métricas, como recomendación general.
Bajo el criterio de experto se hace coherente el resultado de los cluster, ya que aunque predominaba la categoría de atraco como modalidad, Candelaria como comuna y caminata como tipo de vehículo utilizado, factores que generan inseguridad como lo son las horas y días de hurto fueron bien calificados los cuales también estuvieron influenciados por el genero.
