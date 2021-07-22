# BFS
- No es recursivo, usa **cola**
- Empiezo sobre un vertice cualquiera
- Me voy a mover radialmente 
```c
		lista_adyacentes = grafo_obtener_adyacentes(v)
```
- Diccionario de padres , *orden/tiempo/distancia* y TDA Cola
- Se arranca por el vertice A y se le pone que el padre es *None* y el orden de A es 0 y que A fué visitado.
- Encolar A
```python
def bfs(grafo, origen)
	padres={}
	orden={}
	visitados=set()
	A= origen
	cola=cola.crear()
	padres[A]=None
	orden[A]=0
	visitados.add(A)
	cola.encolar(A)
	## aca termina setup
	while not cola.esta_vacia():
		v = cola.desencolar(cola)
		for w in grafo.adyacentes(v):
			if w not in visitados:
				visitados[w]=True
				padres[w]=v
				orden[B]=orden[A]+1
				cola.encolar(w)
	return padres, orden
# Termine recorrido
# El recorrido BFS es la inversa de padres
# Genera un arbol desde el padre con los caminos posibles con menor longitud
# aristas			
```


# DFS
- Hacer lo mismo que [[Recorridos sobre grafos#BFS|BFS]] pero con una pila pero pierde el chiste
- Naturaleza recursivo
- Voy a tener de nuevo los 3 diccionarios ,*visitados, padres, orden* (el primero es un conjunto?)
- Empiezo por un vertice cualquiera y el mismo setup que BFS.
- Llamo para el vertice A, se va a fijar para cada uno de sus adyacentes, si alguno no esta visitado -> llamo recursivamente.
```python
def dfs(grafo, origen):
	padres={}
	orden={}
	visitados=set()
	A= origen
	padres[A]=None
	orden[A]=0
	visitados.add(A)
	_dfs(grafo, A, visitados, padres,orden)
	return padres, origen
def _dfs(grafo, v,visitados,padres, orden)
	for w in grafo.adyacentes(v):
		if w not in visitados:
			visitados.add(w)
			padres[w]=v
			orden[w]=orden[v]+1
			dfs(grafo,w,visitados, padres, orden)
	return padres,origen
# el diccionario de padres es el que arma el arbol de recorrido	
```

#### ambos son $O(v)