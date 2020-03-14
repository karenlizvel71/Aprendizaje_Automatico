# Taller 3: Métodos supervisados 		
## Integrantes: 	
Ana María Urán González.
Karen Lizeth Velásquez  Moná.

# I.	CONTEXTUALIZACIÓN

El aprendizaje automático ha  revolucionado la  computación facilitando la realización de  tareas  manuales  de  forma digital. El maching learning como también es  conocido este campo se enmarca en la inteligencia artificial, permitiendo el desarrollo de algoritmos  que  permiten  que las  maquinas  aprendan por  su cuenta  y respondan a determinadas  preguntas  con bastante  certeza.

Una de las  modalidades de  estos algoritmos son  los   de aprendizaje  supervisado. Los  modelos supervisados son aquellos que  buscan a partir de un conjunto de entrenamiento lograr que un algoritmo aprenda a asignar  etiquetas  a nuevos  valores, es decir, se busca que  el algoritmo prediga un valor de  salida.

Estas técnicas  pueden dividirse en dos  tipologías los métodos  enfocados  en predicción y los métodos enfocados en clasificación. Lo que distingue estos dos enfoques es la tipología de la  variable objetivo. En los casos de clasificación, es de tipo categórico, mientras que en los casos  de regresión la  variable objetivo es de  tipo numérico.

Los  algoritmos más habituales  que son aplicados para el aprendizaje supervisado son:
•	Árboles de decisión.
•	Clasificación de Naïve Bayes.
•	Regresión por mínimos cuadrados.
•	Regresión Logística.
•	Support Vector Machines (SVM).
•	Métodos “Ensemble” (Conjuntos de clasificadores).

# II.	PLANTEAMIENTO DEL PROBLEMA
 
Continuando con el dataset estudiado en el taller 2, el cual cabe  recordar  corresponde  a los hurtos  realizados en la ciudad de  Medellín  durante  2019 , nos  interesa  diseñar un algoritmo que nos  clasifique la tipología del  hurto. Como lo vemos en el siguiente  gráfico, existen un desbalance entre las  clases, que  puede derivar en un deterioro  en la eficiencia del clasificador, aumentando así  los  casos de  Falsos-positivos ya que  el algoritmo desempeñaría una buena  labor  sobre la  clase mayoritaria en  detrimentos de las minoritarias. Es por esto que  para este trabajo compararemos los resultados de dos de los algoritmos de  ensamblé más  conocidos  (Random Forest  y AdaBoost), con el  fin de  identificar cual de  los dos  presenta mejores  resultados en precia de desbalances de  clases.


# III.	EXPLICACIÓN DE LA  TECNICA

## AdaBoost
La  técnica de AdaBoost es uno de los  clasificadores de refuerzo  propuesto por  Yoav Freud y Robert Schapire en 1996.Esta técnica, crea un clasificador  fuerte combinando múltiples clasificadores de bajo  rendimiento, para obtener un clasificador fuerte de  alta precisión.
El concepto central de este algoritmo es  definir los pesos de los  clasificadores y entrenar la muestra de datos en  cada  iteración de modo  que garantice las predicciones precisas de  observaciones  de clases  bajas.

Este algoritmo funciona de la siguiente manera:
1.	Selecciona un subconjunto de entrenamiento aleatoriamente.
2.	Capacita iterativamente el modelo seleccionado  el conjunto de  entrenamiento  basado en la  predicción precisa del último entrenamiento.
3.	Asigna mayores pesos a las  observaciones clasificadas incorrectamente para que  en la  próxima iteración esta observación  obtenga la  probabilidad más alta de clasificación.
4.	Asigna pesos al clasificador entrenado en cada iteración de acuerdo con la precisión del clasificador.El clasificador más  preciso obtendrá un alto peso.
5.	Este proceso itera hasta que los datos  de entrenamiento completos  se ajusten sin ningún error o hasta que se alcance  el número máximo de  estimadores.

Un problema común en este algoritmo  suele  ser  su lentitud, ya que  busca clasificar perfectamente  los  puntos sin sobreajustar el  modelo.


## Random Forest
Un random forest es un conjunto de árboles de  decisión combinados con bagging, lo cual permite  que cada árbol  vea una  proporción distinta de  datos de entrenamiento
De esta manera, al combinar  sus resultados, unos errores se compensan con otros  y se  obtiene una predicción  que  generaliza la mejor de ellas.


Unas  de las  ventajas  más  atribuibles al random forest son:
•	La facilidad en la preparación de los datos y el manejo de miles de variables donde  puede  fácilmente seleccionar las más significativas.
•	Incorpora métodos efectivos para estimar valores faltantes.

## IV.	APLICACIÓN.

Iniciamos  el proceso diviendo nuestro dataset en un conjunto de  entrenamiento y uno de prueba  bajo el  criterio 70%-30%.

### Random Forest

Entrenaremos  un Random Forest , con  500 árboles, un criterio de calidad de división  Gini ( Medida utilizada para clasificar un individuo en una clase), sin  limite de profundidad en los nodos  y un procesamiento en paralelo.

Vemos  que  el modelo, no logra predecir  perfectamente  todas  las clases,  sin embargo, con la  precisión vemos  que en un 94.9% de las  veces logra hacerlo muy  bien. Con el  desbalance de  clases antes expuesto podría  esperarse que el  recall fuera muy malo ya que podría no  ser capas de  detectar estos  patrones  diferentes, pero contrariamente  a esto su recall es del 94.9% lo cual también  es una buena  señal que  el modelo  tiene un perfecto manejo de la  predicción de clases.
Finalmente  revisando la métrica F1 que  agrupa el recall y la precisión en una  sola medida , podemos   concluir  que  estadísticamente  el modelo   es bueno   pues posee una  calidad global del 94.3%.

### AdaBoost

Entrenaremos  el Adaboost con la  función de activación básica  de  este algoritmo que  es un árbol de decisión, esto lo podremos  hacer a través de la  siguiente sintasis en Python.

En este caso los resultados no son tan buenos  como en el ramdom forest, si bien este algoritmo da prioridad a las  clases desbalanceadas, en este  caso no logra diferenciar con claridad el  hurto a personas  del  hurto a  residencias. Este mal manejo de las  clases  se refleja lo refleja cada una de las  métricas  calculadas, por  ejemplo,  la  precisión y el recall es solo del 71.5%  es decir la  cantidad de predicciones correctas y la capacidad de detectar diferencias  entre las clases disminuye en almenos  23% con respecto al random forest. Esto conlleva a que   la media  total del modelo F1 sea del 76%.
Con estos  resultados y teniendo en contraste el random forest anterior, el Adaboost no  sería  una  buena alternativa  para modelar este  caso.
Propondremos un último  modelo ensamblando  los  2 anteriores, realizaremos un  nuevo Adaboost con un ramdom  forest como  función de  activación, de esta manera  pretendemos  tener la  precisión del random forest  empleando un algoritmo que  me identifica las  clases desbalanceadas.


