## Segmentación de Clientes

### Objetivo

El objetivo del presente trabajo es segmentar a los clientes de un supermercado en un número reducido de grupos, esto a partir de información obtenida a través de las tarjetas de membresía.

### Prerequisitos

Las librerias necesarias están listadas en requirements.txt. También se incluye environment.yml para los usuarios de Anaconda.

### Datos

El conjutno de datos proviene de Kaggle bajo el nombre de "Customer Clustering", el cual fue subido por Dev Sharma. Este cuenta con 2000 observaciones.

Ver la carpeta de referencias para más información.

### Exploración Inicial de Datos

El conjunto de datos se compone de variables numericas, ordinales y categoricas. La mayoria de los clientes se encuentra entre los 20 y 60 años y tienen ingresos medio-altos.

<img src="referencias/images/age.png" alt="Alt text 1" width="300"/>

También, se puede observar que existe correlación entre ciertas variables numéricas. 

<img src="referencias/images/corr.png" alt="Alt text 1" width="400"/>

### Construcción del modelo
Tres algoritmos de agrupamiento distintos fueron implementados: K-means, HDBSCAN y Gaussian Mixture Model. En cada caso,  se determinaron los mejores hiper-parámetros. Se utilizó la biblioteca Scikit-learn para K-means y GMM, mientras que para el algoritmo HDBSCAN se utilizó la implementación provista por la biblioteca hdbscan.

Se utilizaron varias técnicas para la selección de los hiperparámetros para cada algoritmo.

- Para K-means se utilizó una combinación entre el método del codo (elbow curve) que usa la métrica inercia, y la métrica de la silueta.

<img src="referencias/images/elbow.png" alt="Alt text 1" width="300"/> <img src="referencias/images/silhouette.png" alt="Alt text 2" width="300"/>

- Para HDBSCAN se utilizó la métrica de la silueta.
- Para GMM se utilizó la métrica BIC (Bayesian Information Criterion) junto con la métrica score para escoger los valor más óptimos.

### Selección del modelo

A continuación se ilustra los resultados de cada uno de los modelos.

<img src="referencias/images/scores1.png" alt="Alt text 1" width="400"/>

Se observa que el modelo con una capa oculta es el que mejor se desempeña en el test set bajo la métrica "Accuracy". Este modelo tiene la función tanh como función de activación en la capa oculta y consta de 35 neuronas en la misma. 

### Explicabilidad del Modelo

Se desea conocer la importancia de cada una de las variables en el momento de hacer la predicción por parte del modelo. Para ello se usa la técnica de permutación. Esta consiste en permutar los valores de las filas de cada columna, una columna a la vez, y calcular como el desempeño es afectado por esta permutación. Aquellas columnas (esto es, las variables) cuya permutación cause la mayor caída en el desepeño serán las mas importantes para el modelo.

A continuación se detallan los resultados de permutación para el trainin-set y test-set.

<img src="referencias/images/importances_train.png" alt="Alt text 1" width="300"/> <img src="referencias/images/imprtances_test.png" alt="Alt text 2" width="300"/>

En ambos casos, caa (número de vasos principales) es una varible muy importante. También se puede ver que oldpeak (depresión de ST inducida por ejercicio en relación con el reposo) es una variable muy importante cuando se usa el training set, pero no con el test set. Esto puede ser una señal de que esta varible esta causando overfitting. Finalmente, cp_0 (tipo de dolor de pecho. Valor 0: angina típica) es muy importante en el test set, pero no así cuando se usa en training set. Esto sugiere que el modelo puede no estar capturando parte de la complejidad en los datos.


### Conclusiones

El modelo que mejor se desempeña con la métrica escogida es el de arquitectura más simple. Sin embargo, todavía es posible mejorar este modelo buscando hiperparámetros más óptimos realizando una busqueda exaustiva con "Grid Search".

### Contacto


jimenezc.bo@gmail.com  

jimenezc.antn@gmail.com

