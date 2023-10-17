# EDA_LINEAR-REGRESSION_HYPOTHESIS_BRENDA_CORTES_AGUILAR

Descripción y objetivos del proyecto.
Objetivos:
•	Que el estudiante pueda utilizar Git para llevar a cabo el control de versiones.
•	Que el estudiante pueda realizar el análisis exploratorio de los datos completo sobre un dataset real.
•	Que el estudiante ponga en práctica sus conocimientos teóricos y ejercite su capacidad de análisis.
•	Que el estudiante demuestre sus habilidades al crear un modelo de regresión lineal multivariable.
•	Que el estudiante se familiarice con las pruebas de hipótesis.
Descripción de la actividad:


Este proyecto consiste en cinco etapas principales:


1.	Exploración de los datos.

Paso 1: Cargue el dataset ("Retrasos.csv") en un dataframe, muestre información básica, enliste las columnas numéricas y las columnas objeto.

Sé observar que el data set, tienen un total de 27 columnas, contiene tipos de dato, "Object", "Int" y "float" y un total de 1000 registros, también se observa que más del 50% del data set, está representado por columnas tipo objeto.

Paso 2: Haga conteo de datos nulos (ordene de forma descendente); de las variables numéricas, muestre datos estadísticos; de las variables de tipo objeto, determine cuáles sí son factibles para convertir en categóricas y el porqué.

Podemos observar presencia de datos nulos en 5 columnas, se destaca la columna  unit_cost, que está nula casi en su totalidad, y dosage, que tiene contiene aproximadamente más de 40% de datos nulos, el resto de las columnas presentan niveles bastante bajos, abra que determinar la mejor manera para tratarlos.

Una vez observados la cantidad de datos únicos que posee cada una de las columnas objeto y de haber observado los valores que poseen, las variables que podrían categorizarse son,vendor_inco_term, shipment_mode, late, product_group, sub_classification y  freight_cost_groups, ya que sus valore únicos rondan entre los 2-6, el resto de columnas contiene un valor más elevado de datos únicos y a simple vista no se nota un patrón que podríamos aplicar para tratar de simplificar la categorización, por otro lado, existen columnas como:  managed_by, fulfill_via y first_line_designation, que únicamente contienen una categoría, no creo que sea conveniente considerarlas para la categorización, ya que no existe una variabilidad, pueden no ser útiles ni informativas.

Paso 3: Identifique si las columnas numéricas cuentan con anomalías, para ello puede apoyarse de gráficos; identifique si las columnas objeto tienen inconsistencias, para ello puede apoyarse de gráficos.

Al observar los gráficos de boxplot, de cada una de las columas numéricas, se puede observar, que las únicas columnas que no presentan datos atipicos son la colimna "id" y la columna "unit_cost", por lo que podemos inferir que quizá exista una gran dispersión en los datos. Por otro lado, en las columnas categóricas, resulta complicado observar si existen anomalías, existe columnas que presentan muchos valores únicos, en forma de abreviaturas y por lo mismo es complicado determinar si es un valor consistente o se trata de una anomalía que debe de ser removida.

Paso 4: Muestre las correlaciones (pearson y spearman) que hay en general (valores numéricos), puede utilizar gráficos, ¿cambian mucho los valores entre cada tipo de coeficiente de correlación?

La respuesta es que, si, cambia respecto a cada caso en particular, al observar el gráfico de diferencias se puede observar la  variación entre coeficientes, en algunas columnas es muy grande la variación, variando hasta un  0.30  de diferencia, en algunos casos la variación es muy baja y en algunos no cambia, permanece la misma correlación con ambos coeficientes.  

Paso 5: Muestre los gráficos de distribución de las columnas, elija el tipo de gráfico adecuado para el tipo de variable que está analizando.

Todas las columnas categorcas fueron graficadas con el KDE y su grafico de distribucion,  menos la variable "late_delivery" como una variable discreta, ya que unicamente contiene valores de 0 y 1



2.	Manipulación y tratamiento de los datos.

Paso 1: Trate los datos nulos, emplee las técnicas que considere más adecuadas de acuerdo al caso específico. Justifique el porqué de la técnicas que escogió.

Como se observa tenemos dos variables categóricas y tres variables numéricas que cuentan con datos nulos, por lo que, primordialmente, checaremos si estas columnas no exceden el porcentaje adecuado para tratar estos datos nulos con la eliminación.


Por otro lado, la columna "unit_cost " es una variable numérica que se encuentra nula casi en su totalidad, al observar las matrices de correlación que se graficaron en el paso anterior, esta variable presenta una única correlación positiva fuerte con la columna, "unit_price", aunque no se nos ha especificado alguna variable objetiva, tomaré la decisión de preservar la columna. 

Como las columnas " line_item_insurance_usd ",  " freight_cost_groups" y " freight_cost_usd", no superan el límite, eliminaremos los registros que contienen datos nulos.

Dado que la columna "dosage" es categórica, imputaremos con la moda, por otro lado, recordando el gráfico de boxplot de la columna "Unit_cost" graficado en pasos anteriores, esta columna no presenta datos atípicos, pero sí un sesgo positivo (sesgo a la derecha), por lo que utilizaremos la mediana, para imputar esta columna.

Después del proceso, podemos observamos un data set sin presencia de datos nulos.

Paso 2: Convierta en categorías las variables objeto que considere adecuadas, en caso de ser necesario, trate las inconsistencias.

Como se menciono en pasos anteriores, las unicas variables que considero aptas para categorizar, son las columnas vendor_inco_term, shipment_mode, late, product_group, sub_classification y freight_cost_groups, por lo tanto son las unicas variables que convertire en categorizas. Con respecto a las inconsistecias, dado a la gran variabilidad que presentan las columnas y a falta de un diccionario de categorias, no me fue posible detectar inconsitencias

Paso 3: Utilice el coeficiente de variación para determinar qué columnas (variables) numéricas tienen mayor dispersión.

Siguiendo el criterio de,  0 - 0.5, existe poca dispersión, 0.5-1 existen dispersión media y anomalías no graves y coeficiente > 1, demasiada dispersión y anomalías graves. Podemos determinar que todas nuestras columnas numéricas, exceptuando el "id"   y "unit_cost"   presentan un nivel, un indicador de dispersión bastante grande, por lo que podría no ser viable utilizar el método del rango intercuartílico para tratar los datos atípicos. 


Como la gran mayoría de las columnas presentan un coeficiente mayor a 1, es decir, que su dispersión es enorme y posiblemente contengas muchos datos atípicos, las columnas que presentan los coeficientes más grandes son las columnas: late_delivery, unit_price   y line_item_quantity.

Paso 4: De las variables con mayor dispersión, presente su distribución, su gráfico boxplot, y describa a qué se debe que haya tanta dispersión.

Al observar los graficos de la columnas late_delivery, unit_price y line_item_quantity, en los gráficos boxplot, se observa presencia de valores atípicos. Estos valores atípicos contribuyen a que exista una mayor dispersión en los datos, ya que alargan la cola de la distribución. Es complicado determinar las razones por la cuales estas columnas cuentan con la presencia de estos datos atípicos que están afectando la dispersión de la variable.

Por los nombres que presentan las variables podemos determinar que tal vez la dispersión se deba a la propia naturaleza de los datos.

Por ejemplo, en el caso de late_delivery, la variabilidad puede deberse a varios factores externos que afectan la entrega. En el caso de unit_price, la variabilidad puede estar relacionada con los precios de los distintos proveedores. La variabilidad en line_item_quantity puede deberse a la naturaleza de los productos o servicios que se están contabilizando.


Paso 5: Conteste las siguientes preguntas acorde a la información obtenida de los datos.

1. ¿Considera que con los datos numéricos actuales se pueden realizar predicciones para la columna "line_item_insurance_usd"?
Recordando los coeficientes de correlación que calculamos en pasos anteriores, dependiendo del coeficiente que se utilice, se pueden detectar de 2-3 variables con una correlación positiva fuerte, line_item_value,  weight_kilograms y freight_cost_ usd.  Por lo tanto, yo considero que con los datos numéricos actuales y dada la fuerte correlación que presenta con las variables antes mencionadas, es posible utilizar estas variables para realizar predicciones sobre "line_item_insurance_usd".


2. ¿Considera que con los datos numéricos actuales se pueden realizar predicciones para la columna "late_delivery"?
Para contestar esta pregunta también creo que es importante recordar los gráficos de coeficiente de correlación, analizados anteriormente, independientemente del tipo de coeficiente, esta variable en particular no presente correlaciones positivas o negativas fuertes con alguna otra variable, por lo tanto, yo considero que no contamos con información suficiente para realizar predicciones con esta variable. 

3. ¿Cree que alguna otra columna (objeto o categórica) se pueda correlacionar fuertemente con "late_delivery"?, si es así, ¿cuál o cuáles cree que tendrían una correlación fuerte?

Lo más probable es que si, si tomando en consideración la variable está haciendo referencia a la entrega tardía, puede haber factores como, el  shipment_mode, vendor_inco_term  y country, puedan ser factores que provoquen que esta variable cambie; sin embargo, para determinar si existen y verificar que realmente estos factores influyen, tendríamos que verificarlo, convirtiendo en numérico estas columnas y calcular el coeficiente de correlación con la variable. 


3.	Construcción de un modelo de regresión lineal.

Paso 1: Seleccionar las columnas que estén más correlacionadas con "line_item_insurance_usd" y asígnelas en la variable "X", seleccione la columna "line_item_insurance_usd" y asignela a la variable "y".

Ya que se nos pide crear un modelo de regresión lineal, con las variables más relacionadas, construiremos un modelo multivariable, siguiendo el criterio de que, 0.1 - 0.3 se considera una relación débil, de 0.3- 0.5 una relación media y de 0.5 a 1 una relación muy fuerte, para este caso en particular, utilizaremos las variables, line_item_value, weight_kilograms y line_item_quantity. 

Paso 2: Divida en dos muestras los dos dataframes creados anteriormente (X,y), debe tener una muestra para entrenamiento y otra para pruebas, el tamaño de la muestra de entrenamiento debe ser del 80%, asigne una semilla aleatoria con valor de 2033 para poder brindar reproducibilidad.

Paso 3: Importe el modelo de regresión lineal (multivariable) de sklearn, entrene el modelo con el set de datos de entrenamiento, posteriormente haga predicciones con el set de pruebas (X_train).

Paso 4: Evalúe el modelo con la métrica "accuracy_score" y la métrica "f1_score" (ambas disponibles con sklearn).

# NOTA: Atendiendo las indicaciones proporcionadas por el profesor, se evaluará el modelo con pruebas R2 y MAE.

Paso 5: Responda

1. ¿Su modelo fue capaz de realizar predicciones con precisión?

Tomando en consideración los valores de las métricas utilizadas, el valor que me proporciona más información para determinar si el modelo es preciso, es el valor obtenido por la métrica r2, la cual nos dice que: cuanto más cercano a 1 sea el valor de esta métrica, mejor será nuestro modelo. Tomando en consideración que mi modelo presento una métrica de 0.9179, lo que nos indica que está teniendo un buen desempeño y posiblemente una buena precisión de predicción.  


2. ¿A qué cree que se deba el rendimiento de su modelo?

Puede que existan diversas razones por las cuales el modelo este teniendo un buen rendimiento; sin embargo, creo que se debe principalmente a que contábamos con variables con correlaciones bastante fuertes a la variable objetivo. 


3. Si selecciona todas las variables y las asigna en X, en lugar de las que tienen correlación más fuerte, ¿cree que el modelo mejore o empeore?

En este caso, en particular, no creo que sea lo más conveniente,  si seleccionamos todas las variables en lugar de solo aquellas con correlación más fuerte, el rendimiento del modelo podría variar. Quizá podríamos entorpecer el modelo, especialmente si algunas de esas variables no están realmente relacionadas con la variable objetivo. sin embargo, valdría la pena evaluar un segundo modelo y observar el comportamiento y realizar la comparativa de manera adecuada.


4.	Hipótesis.

Paso 1: Defina la hipótesis nula a partir de la siguiente pregunta:
¿La proporción de entrega tarde ("late_delivery") es mayor a 0.06 (6%)?, asigne el valor de la hipótesis nula a la variable "Ho".
Considere un nivel de significación del 5%.
Ho =La proporción de entregas tardías es mayor a 0.06

Paso 2: Defina la hipótesis alternativa según la pregunta anterior, solo escríba cómo quedaría y qué tipo de prueba de hipótesis se utilizará.
Su respuesta: Ha = La proporción de entregas tardías es menor o igual a 0.06 (6%).
Como estamos determinando que Ho, es mayor que, la prueba de hipotesis que debemos de considerar es, una pureba de cola derecha.

Paso 3: Haga una distribución bootstrap de la columna "late_delivery" y calcule el error estándar, guárdelo en una variable. El tamaño de la lista de la distribución de boostrap queda a libre elección, muestre un histograma de la distribución bootstrap.

Paso 4: Calcule la puntuación Z y guárdela en una variable.
Paso 5: Dependiendo del tipo de prueba, calcule el valor de P (p-value) y diga si puede rechazar (o falla al rechazar) la hipótesis nula.
Calcule el intervalo de confianza, utilice los cuantiles adecuados dado el nivel de significación establecido previamente.

--Al final del analisis 

# Se falla a rechaza la hipótesis nula.



