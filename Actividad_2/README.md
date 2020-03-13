# Taller 2: Ingeniería de  características 				

### Integrantes:   	Ana María Urán González. -                     Karen Lizeth Velásquez  Moná.

## I.	CONTEXTUALIZACIÓN DEL PROBLEMA

El difícil acceso al empleo desencadena unos altos niveles de desigualdad entre los  miembros de la sociedad, lo que hace que ciudades como Medellín  enfrenten graves problemas  de seguridad entre los que  se encuentra el consumo  y tráfico de  drogas, la mendicidad, la aparición de grupos  armados ilegales, los  homicidios  y el hurto.
Según la encuesta de Medellín como vamos  2019 , el 20% de los  problemas  más  graves de seguridad que  atraviesa la ciudad son por  casos de Hurto donde  se incluyen  los robos de vehículos, viviendas, negocios  y en general asaltos a la  población civil. En  un artículo  publicado por  el periódico El Tiempo, Medellín en los últimos 5 años  ha tenido una disminución en la  cantidad de  policías de 13,77%, pasando de 7925 en 2016 a 6833 en  2020, de los cuales  solo  5552  cumplen actividades operativas distribuidos en  3 turnos. Según las  cifras  presentadas recientemente por el secretario de  seguridad José Gerardo Acevedo se  percibió un incremento en los  casos de hurtos  a personas del 19% en lo que  va del 2020 comparándolo con las cifras  del mismo período en 2019.
Esta problemática hace necesario idear  estrategias  que permitan optimizar la distribución de los uniformados disponibles  con el fin de  prevenir  y atender de manera  rápida   la ejecución de actos delictivos.

### Objetivo

Definir  un  tipo de  hurto en cada  denuncia  es  complejo  ya que   un hurto a personas puede  involucrar un hurto a motocicletas   o un hurto a vivienda, por  esto con el fin de  buscar agilizar estos procesos  administrativos  que  deben cumplir las autoridades y que  demandan tiempo ,se  quiere  identificar  cuales  serían las características que ayudarían a el tipo de hurto cometido (hurto apersonas/ otros hurtos) con el fin de reducir el tiempo en labores administrativas  y dar diligencia  a la atención de  las  denuncias.

## II.	ANALISIS DE INFORMACIÓN

### PARTE I:  Descripción de los  datos originales
La base  original  contiene  63482  observaciones  correspondientes a los diferentes  tipos de  hurtos denunciados en Medellín  durante 2019  y los 2 primeros  meses del año 2020.
La base cuenta originalmente con  41 variables  de las  cuales  el 95% son categóricas

### PARTE II:  Limpieza de datos
Como primer  paso en este proceso es necesario  limpiar la  base  de  datos de  registros  faltantes, columnas  inútiles  y datos  atípicos. Iniciamos  esta parte del proceso definiendo  temporalmente  los  casos de análisis (2019), Adicionalmente, un mismo  caso de hurto puede  ser  reportado  varias  veces, por lo cual para depurar  las  denuncias  duplicadas  solo tomaremos la  variable  Caso_Hurto=1, el cual conserva solo la primera  denuncia  hecha por cada caso.
Es necesario eliminar  algunas  variables  que  hasta este  lugar  se detectan como inútiles para la elaboración de  cualquier análisis.

Como sabemos las  denuncias por hurto  pueden  hacerse por  el robo de cualquier  tipo de bien, el data set tiene  esta información consolidada en  3 campos Bien,Categoria_Bien,Grupo_Bien ; yendo  de lo particular a una agrupación macro,  considerando que   el campo Bien es de muy difícil manejo por  sus 335  categorías  y que  el  Grupo Bien puede  ocultar  información relevante, analizaremos  el desglose de la variable Categoría Bien, con el  finde  identificar aquellos  bienes  que  representan al menos  un 1% de los  hurtos de la  ciudad

### PARTE III:  Creación de nuevas  características.
Como hemos visto hasta este momento nuestras  variables categóricas tienen una amplia cantidad  de subclases, hemos disminuido algunas  bajo unas  reglas  de conformación del  data set, sin embargo, lo que  buscaremos ahora  es reagrupar  las  clases  persistentes con  el objetivo de  tener  la  información de  manera más  compacta  y manejable.


## III.	SELECCIÓN DE CARACTERISTICA

Como  último paso en el proceso de ingeniería de  características, buscaremos  métodos  para elegir  las variables más importantes y/o relevantes dentro de un conjunto de datos.
Como sabemos  nuestra variable respuesta  es una  variable  binaria que  debe ser  explicada  por medio de  variables exógenas en su mayoría cualitativas, trasformamos las  categorías en variables  indicadoras que  faciliten la implementación de  técnicas  de  selección  como el forward, backward y el Random Forest.

###  Forward
El algoritmo de selección hacia adelante comienza con un modelo nulo al cual va ingresando una a una las  variables  explicativas, la característica con el valor p mínimo es Seleccionada. Ahora ajuste un modelo con dos funciones probando combinaciones de la función seleccionada anteriormente con todas las demás funciones Repita este proceso hasta que tengamos un conjunto de características seleccionadas con un valor p de característica individual menor que el nivel de significancia. En resumen, los pasos para la técnica de selección hacia adelante son los siguientes:
•	Elija un nivel de significación (p. Ej., SL = 0.05 con un 95% de confianza).
•	Ajuste todos los modelos de regresión simple posibles considerando una característica a la vez. Total, de modelos 'n' son posibles.
•	Seleccione la función con el valor p más bajo.
•	Ajuste todos los modelos posibles con una característica adicional agregada a las características previamente seleccionadas.
•	Nuevamente, seleccione la función con el valor p mínimo. si p_value <nivel de significancia, vaya al Paso 3; de lo contrario, finalice el proceso.
Por  la  naturaleza de nuestros datos dicho modelo lo definiremos  como un modelo regresión logística  el cual emplearemos  mediante la siguiente función:
 
En este punto es importante  entender cómo  funcionan  el modelo  logístico y las  implicaciones que  tendría  estimar  este con  un dataset con las  características  del nuestro.
La regresión logística  es un método  estadístico empleado para predice el resultado de una variable categórica, siendo un método potente cuando se  tiene una  variable respuesta  dicotómica, en nuestro caso (Hurto a personas=1) .
La identificación del mejor modelo de regresión logística se realiza mediante la comparación de modelos utilizando el cociente de verosimilitud, que indica a partir de los datos de la muestra cuanto más probable es un modelo frente al otro. La diferencia de los cocientes de verosimilitud entre dos modelos se distribuye según la ley de la Chi‐cuadrado con los grados de libertad correspondientes a la diferencia en el número de variables entre ambos modelos.
En estos modelos, las variables explicativas de tipo nominal con más de dos categorías deben ser incluidas en el modelo definiendo variables dummy. En nuestro  caso un 95% de las  variables  explicativas  son nominales con las  de  2 categorías , es por esto que  para la aplicación de las  técnicas  de selección creamos las  variables dummys correspondientes siguiendo el criterio de que si uanvariable consta de k categorías deben crearse entonces (k −1) variables dicotómicas asociadas a la variable nominal. 
Dicho lo anterior, nuestra  modelo a emplear para los  métodos  de  forward  y backward será un modelo Logit o modelo de regresión logística binaria 

Corrriendo nuestro modelo y después  de 9 iteraciones  vemos que este nos  determina 21 variables como óptimas  para clasificar los  hurtos, sin embargo, no todas  las  variables son estadísticamente  significativas lo que  podría llevar a concluir en eliminarlas, no  obstante es común en las  investigaciones sociales  donde  se estudian  conjuntos de  datos similares al nuestro conservarlas  todas  ya que  podría  existir relaciones  entre las  variables  explicativas  que pueden tener  iteraciones y aportar al resultado.

### Backward
Este método inicia teniendo en cuenta todas las características  iterando sobre los valores de significancia (Valor P) eliminando la característica menos significativa en cada iteración, buscando obtener un mejor rendimiento del modelo. Este proceso es repetido hasta que la eliminación de características no represente una mejora para el modelo. Los pasos utilizados por esta técnica se mencionan a continuación:
•	Elija todas las variables en el conjunto de características 
•	Elija un nivel de significación (p. Ej., SL = 0.05 con un 95% de confianza).
•	Ajuste todos los modelos de regresión simple posibles considerando una característica a la vez. Total, de modelos 'n' son posibles.
•	Seleccione la variable con el valor p más alto y elimine
•	Ajuste todos los modelos posibles con las características restantes 
•	Nuevamente, seleccione la función con el valor p mínimo. si p_value <nivel de significancia, vaya al Paso 3; de lo contrario, finalice el proceso.
•	Ajuste todos los modelos posibles con una característica adicional agregada a las características previamente seleccionadas.


Partiendo de  las  mismas  interpretaciones hechas con el forward tenemos que  en este  caso son  necesarias 23 variables  explicativas  para clasificar los hurtos  a personas.

Vemos se ambos modelos explican una variabilidad total superior al 70% lo cual podría llevarnos  a concluir que  ambos  modelos son buenos y que  las  variables  empleadas  son las  necesarias  para  desarrollar un modelo de clasificación más  robusto, sin embargo, vemos que  por criterio de AIC el mejor de los 2 es el estimado por el método de backward.

### Métodos de envoltura 
Estos métodos son utilizados para seleccionar características y tienen incorporado en su proceso un algoritmo de Machine Learning donde el criterio de evaluación el mejor rendimiento del algoritmo.

Emplearemos  un random Forest para definir cuáles de las  características son las  que  me permite  clasificar los hurtos a personas, el criterio con el cual mediremos esto es por medio del índice  Gini  tomando como mejores  features aquellas  variables  que  según el índice de Gini me  permiten una  mejor  división de las  2 clases.

Tras entrenar un random forest con 500 arboles tenemos  que  la precisión  es de un 97%  y dicha clasificación esta principalmente  generada por  las siguientes  variables.

Vemos que  las  10 características  más importantes para el random forest se encuentran entre el listado de  variables  seleccionadas  por el modelo de  backward.

Considerando que  el random forest es una técnica  más robusta y que  logro  una precisión mayor  tomaremos  las  variables  allí definidas como las  mejores características  que  permiten clasificar la tipología del hurto.


