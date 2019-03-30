# UniversityHack2019 - Reto Minsait Real Estate Modelling
**Equipo.** AI\|Learners  
**Miembros.**: Alberto Fernandez de Marcos Giménez de los G., Rohit Uttamchandani Dadlani  
**Centro.** Universidad Politécnica de Madrid (UPM)

### 1. Resumen del trabajo desarollado
-------------------------------------------------------
El tiempo que dedica un usuario a visitar un anuncio de vivienda, es un factor de gran relevancia que permite medir la calidad del mismo.
El porcentaje de éxito en la venta o alquiler de una vivienda, dependerá en gran medida del mismo.
En este documento se presentan las variables obtenidas a través de dos fuentes: una inmobiliaria (La Haya) y un gestor de anuncios web (idealista).
Adicionalmente se disponen de analíticas y métricas sobre la interacción del usuario durante su visita al anuncio.


### 2. Análisis exploratorio.
-------------------------------------------------------
Partiendo de un dataset con 9958 y 53 variables, se ha procedido a añadir algunas variables adicionales, que en principio se han entendido como relevantes:
· Número de imágenes por anuncio
· Longitud del texto de la descripción
· Características especiales (Piscina)
· % Descuento: 100%\*(Precio actual-Precio anterior)/Precio anterior
· Precio relativo con respecto a la zona
· Cantidad de pixeles que forman parte de bordes en las imagenes
· Luminosidad media de los pixeles de las imagenes
· Cantidad de anuncios publicados en la zona que comprende el mismo código postal

Tras añadir las variables al dataset, se ha procedido a realizar una exploración de datos no disponibles por atributo (missing values).
Se ha procedido a calcular la matriz de correlaciones asi como la información mutua entre las variables, para encontrar variables irrelevantes y redundantes.

### 3. Manipulación de variables
-------------------------------------------------------
                             
Se ha observado que la variable "HY_distribución" no se encuentra disponible en 6745 muestras, y el certificado energético en 8300.
La provincia de origen, es una variable categórica que no se encuentra muy desequilabra (1700 muestras para Valencia y menos de 10 muestras para 15 provincias).
Por tanto se asume independiente de la variable objetivo.

Observando la distribución de la variable objetivo, se procede a mantener un 98.02% de las muestras, eliminando outliers (TARGET>300 s).
Además se ha visto la irrelevancia de variables como "HY_ascensor" y "HY_cert_energ".
Tras esto, se ha visto la distribución conjunta de cada una de las varibles con la variable objetivo, tratando de encontrar patrones.

Según el tipo de viviendas, debido a la gran variedad de clases disponibles (20) se procede a la reducción de la cantidad de las mismas en este apartado, atendiendo a diferentes criterios y al contenido de la descripción.

Finalmente se ha procedido con la imputación de los valores no disponibles (missing values), utilizando la mediana de los valores disponibles por provincia.Utilizando la mediana se garantiza la minimización del efecto de los outliers, frente a la utilización de la media.

Una vez se ha preparado el dataset, se ha procedido a obtener la importancia de las varaibles en la predicción de la variable objetivo mediante un modelo de regressión basada en Random Forest.
Se ha elegido este método por ser explicativo y proporcionar relaciones observables entre los atributos y la variable objetivo.


### 4. Justificación selección del modelo.
-------------------------------------------------------
El modelo seleccionado ha sido el XGBoost (eXtreme Gradient Boosting) por ser explicativo, computacionalmente eficiente y preciso.
Siendo un algoritmo de tipo "ensemble", ofrece soluciones que permiten combinar la capacidad de múltiples modelos, mejorando la predicción final.


Mejoras a introducir:
· Reconocimiento de patrones en las imágenes mediante CNN de tipo regresión
· Algoritmo genético para optimización de hiperparámetros del XGBoost
