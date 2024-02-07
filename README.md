## <h1 align=center> **PROYECTO INDIVIDUAL Nº1** </h1>

# <h1 align=center>**`MLOps (Data Engineer & Machine Learning)`**</h1>

# <h2 align=center>**`Luciana Chutte`**</h2>


Este proyecto se centra en el desarrollo de un sistema de MLOps acerca de la plataforma multinacional Steam, se realizaran unas series de tareas de extracción, transformación y carga de datos (ETL), así como análisis exploratorio de datos (EDA) en conjunto con la preparación de datos para el desarrollo de una API.A continuación explicare cada instancia. 

### Exploración, Transformación y Carga (ETL)

A partir de los 3 datasets proporcionados (steam_games, user_reviews y user_items) referentes a la plataforma de Steam, en primera instancia se realizó el proceso de limpieza de los datos.

#### `Steam games`
Eliminamos filas nulas, valores nulos y duplicados, cambiamos el tipo de dato a Int., identificamos valores únicos, redondeamos valores con solo 2 decimales,procesamos cada formato de fecha para extraer años y los no validos los eliminamos.

#### `User reviews`
Eliminamos filas y columnas con valores nulos porque los concideré irrelevantes. Separamos todas las reviews generando una fila por cada review dentro de la columna "reviews"
Se creó una nueva columna llamada 'sentiment_analysis' usando análisis de sentimiento y se eliminó la columna de review.
Se exportó para tener el dataset limpio.

#### `User Items`
Procesamos los datos par el conjunto de los items que posee cada usuario, eliminamos columnas innecesarioas para el desarrollo de la API, luego exportamos un csv en formato gzip.


### Análisis Exploratorio (EDA)

Teniendo los 3 datasets limpios, se realizó un proceso de EDA para realizar gráficos y así entender las estadísticas, encontrar valores atípicos y orientar un futuro análisis.

Top 5 de juegos mas jugados
<p align="center"><img src="https://ibb.co/Phm9r1N"></p>
