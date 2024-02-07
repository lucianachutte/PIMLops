Para que el markdown se vea correctamente en GitHub, necesitas ajustar algunos elementos. Aquí tienes una versión reformateada:

```markdown
# PIMLops

## PROYECTO INDIVIDUAL Nº1

# MLOps (Data Engineer & Machine Learning)

## Luciana Chutte

Este proyecto se centra en el desarrollo de un sistema de MLOps acerca de la plataforma multinacional Steam, se realizarán una serie de tareas de extracción, transformación y carga de datos (ETL), así como análisis exploratorio de datos (EDA) en conjunto con la preparación de datos para el desarrollo de una API. A continuación, explicaré cada instancia.

### Exploración, Transformación y Carga (ETL)

A partir de los 3 datasets proporcionados (steam_games, user_reviews y user_items) referentes a la plataforma de Steam, en primera instancia se realizó el proceso de limpieza de los datos.

#### Steam games
- Se eliminaron filas nulas, valores nulos y duplicados.
- Se cambió el tipo de dato a Int.
- Se identificaron valores únicos.
- Se redondearon valores con solo 2 decimales.
- Se procesó cada formato de fecha para extraer años y los no válidos se eliminaron.

#### User reviews
- Se eliminaron filas y columnas con valores nulos porque los consideré irrelevantes.
- Se separaron todas las reviews generando una fila por cada review dentro de la columna "reviews".
- Se creó una nueva columna llamada 'sentiment_analysis' usando análisis de sentimiento y se eliminó la columna de review.
- Se exportó para tener el dataset limpio.

#### User Items
- Se procesaron los datos para el conjunto de los items que posee cada usuario.
- Se eliminaron columnas innecesarias para el desarrollo de la API.
- Se exportó un CSV en formato gzip.

### Análisis Exploratorio (EDA)

Teniendo los 3 datasets limpios, se realizó un proceso de EDA para realizar gráficos y así entender las estadísticas, encontrar valores atípicos y orientar un futuro análisis.

![Top 5 de juegos con mas horas jugadas](https://github.com/lucianachutte/PIMLops/blob/main/top_5_juegos%2Bhoras.png)

![Análisis price](https://github.com/lucianachutte/PIMLops/blob/main/distri%20precios.png)

![Cantidad de juegos por género](https://github.com/lucianachutte/PIMLops/blob/main/generos%20por%20juego.png)

![Top 5 de géneros más jugados](https://github.com/lucianachutte/PIMLops/blob/main/top_5_juegos%2Bjugados.png)

![Cantidad de juegos lanzados por año](https://github.com/lucianachutte/PIMLops/blob/main/juegos%20lanzados%20por%20a%C3%B1o.png)

![Análisis recommend](https://github.com/lucianachutte/PIMLops/blob/main/cant.recomendaciones.png)

![Top 5 juegos mas recomendados](https://github.com/lucianachutte/PIMLops/blob/main/top%205%20juegos%20mas%20recomendados.png)

![Análisis de sentiment_Analysis](https://github.com/lucianachutte/PIMLops/blob/main/sentiment_analysis.png)

![Top 5 juegos mayor cantidad de sentiment_analysis](https://github.com/lucianachutte/PIMLops/blob/main/top5%20juegos%20con%20%2B%20cant.sent.png)

### Modelo de aprendizaje automático

Para este modelo, se ha elegido utilizar el algoritmo SVD (Singular Value Decomposition) de la biblioteca Surprise. El objetivo es predecir las calificaciones de los usuarios para los elementos del conjunto de datos para hacer un sistema de recomendación usuario-item.

El proceso consta de los siguientes pasos:

1. Creación de las Calificaciones: Para entrenar el modelo, se genera una calificación a partir de la suma de las columnas recommend (0 o 1) y sentiment_analysis (0, 1, 2). Estas calificaciones se escalan en una clasificación que varía de 0 a 3.

2. Selección de Características: Se seleccionan las características relevantes para el modelo, incluyendo user_id, item_name y la calificación creada en el paso anterior.

3. Entrenamiento del Modelo: El conjunto de datos se divide en un 70% para entrenamiento y un 30% para pruebas. Luego, se crea el modelo SVD, se entrena con los datos de entrenamiento y se evalúa su rendimiento utilizando la métrica RMSE (Error Cuadrático Medio de la Raíz). El valor obtenido indica la precisión del modelo, obteniendo un valor aceptable para su utilización.

4. Optimización de Hiperparámetros: Se ajustan los hiperparámetros del modelo para mejorar su rendimiento. Esto se aplica en la creación del modelo, y el proceso de entrenamiento se repite con los nuevos hiperparámetros.

Finalmente, el modelo entrenado se guarda en formato Pickle para poder ser utilizado en la API.

### Función recomendacion_usuario

La función "recomendacion_usuario" recibe como parámetro el nombre de un usuario (str) y devuelve una lista de los 5 juegos recomendados para ese usuario. Ejemplo de retorno: { "Juegos recomendados para Sp3ctre": [ "King Arthur's Gold", "Everlasting Summer", "Call of Juarez Gunslinger", "The Wolf Among Us", "SUPERHOT" ] }

El proceso de recomendación se realiza de la siguiente manera:

- Se verifica si el usuario existe en el conjunto de datos. Si no se encuentra, la función retorna {'Error': 'El usuario no existe'}.
- Si el usuario existe, se filtran los juegos que ya posee el usuario y se eliminan de la lista de juegos disponibles para que no se le recomienden juegos que ya tiene.
- A continuación, importamos el modelo de recomendación previamente entrenado, que se encuentra en formato pickle.
- Se genera una clasificación para el usuario con respecto a todos los juegos disponibles en el conjunto de datos. El modelo utiliza esta clasificación para predecir qué juegos podrían gustarle al usuario.
- Finalmente, la función selecciona y retorna los 5 juegos con la mayor probabilidad de que le gusten al usuario, basándose en las predicciones del modelo.

### Desarrollo API

Se implementará una API utilizando FastAPI. [Aquí está el enlace](https://pimlops-72b8.onrender.com/docs) a la documentación de la API.

Las siguientes son las funciones para los endpoints:

- developer(desarrollador: str): Retorna la cantidad de ítems y el porcentaje de contenido gratis por año para un desarroll

ador dado.
- userdata(usuario: str): Retorna el dinero gastado, cantidad de ítems y el porcentaje de comentarios positivos en la revisión para un usuario dado.
- UserForGenre(genero: str): Retorna al usuario que acumula más horas para un género dado y la cantidad de horas por año.
- best_developer_year(año: int): Retorna los tres desarrolladores con más juegos recomendados por usuarios para un año dado.
- developer_reviews_analysis(desarrollador): Retorna como parámetro el nombre de una desarrolladora (str) y devuelve el total de revisiones positivas y negativas que tiene.
- recomendacion_usuario(usuario): Retorna como parámetro el nombre de un usuario (str) y devuelve una lista de los 5 juegos recomendados para ese usuario.

### Video

[Enlace al video]

### Contacto

- Correo Electrónico: luciana.tte8@gmail.com
- LinkedIn: [Luciana Chutte](https://www.linkedin.com/in/lucianachutte/)
```

Asegúrate de reemplazar `[Enlace al video]` con el enlace correcto a tu video.
