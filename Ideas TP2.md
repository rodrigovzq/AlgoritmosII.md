      


## Implementar Trending Topics

#### Count Min Sketch

-   Implementar un diccionario hash cuya clave sea el hashtag y cómo dato la cantidad de ocurrencias. 
	-   Si f(hashtag)=4, incrementamos el valor almacenado en la posición 4 del arreglo. 
-   Cuando se hay colisiones se cuentan mal porque se mezclan las ocurrencias. Si tenemos k contadores y tomamos el mínimo entonces esa es una buena aproximación para el valor real. 
-   Tener varios contadores con funciones de hashing distintas

  

### Procesar Tweets

-   Contar los TT de un conjunto de tweets
-   Leer por stdin
-   Dos parametros, _n_ y _k_ enteros. 
-   Imprimir por stdout el histórico de los k TTs aproximados cada _n_ lineas. 
-   Orden de ranking o alfabetico. 
-   n y k cantidades se pueden almacenar en memoria. 
-   Impresion de k TT debe ser O(n+ k log n)
-   TDA CountMintSketch. 

  

### Procesar Usuario

-   Ordenamiento no comparativo-> **Counting sort/ Bucket sort?**
-   Contar la cantidad de hashtags para cada usuario. 
-   Se puede almacenar en memoria todo. 
-   Imprimir por stdout los usuarios y la cantidad de hashtags que usaron en tiempo lineal O(u+t) u la cantidad de usuarios y t la cantidad de hashtags