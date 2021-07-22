# Dijkstra
- Hacer un [[Recorridos sobre grafos#BFS|BFS]] con un heap de minimos en vez de una cola. 
- El minimo del heap es por la distancia de los vertices.
- Hay una variacion donde el se encola todo con distancia infinto
- Diccionario de padres, distancia
- Padre de origen es nulo, distancia es 0
- El resto esta en infinito/ si no esta en el diccionario de distancias -> infinito
- Encolar (vertice,distancia) -> (A,0)
- Desencolo y me fijo todos los adyacentes
	- Puedo *mejorar su distancia yendo desde A -> V*  usando esa arista? veo el costo
	- Si el costo de V es menor al que dice el diccionario
		- Actualizo diccionario
		- Actualizo el padre
		- Encolar (V,distancia total), distancia total es la del padre + la de el
	- Si no puedo mejorar => el costo de V no es menor que el del diccionario
- Repito mientras la cola no este vacia. Como es un heap de minimo, me va devolviendo los mas cortos.

```python
def camino_minimo_dijkstra(grafo, origen):
	distancias={}
	padres={}
	for v in grafo:
		dist[v]=float("inf")
	distancia[origen]=0
	padre[origen]=None
	heap = Heap()
	heap.encolar(distancia[origen],origen))
	while not heap.esta_vacio():
		_, v = heap.desencolar() # se le puede poner un _ si no me interesa_
		for w in grafo.adyacentes(v):
			if distancia[v]+grafo.peso(v,w)<distancia[w]:
				distancia[w] = distancia[v]+grafo.peso(v,w)
				padre[w]=v
				heap.encolar(distancia[w],w)
	return padres, distancia
```
Sin llenar el grafo de infinitos
```python
def camino_minimo_dijkstra(grafo, origen):
	distancias={}
	padres={}
	distancia[origen]=0
	padre[origen]=None
	heap = Heap()
	heap.encolar(distancia[origen],origen))
	while not heap.esta_vacio():
		_, v = heap.desencolar() # se le puede poner un _ si no me interesa_
		for w in grafo.adyacentes(v):
			if d_infinita(distancia, w) or distancia[v]+grafo.peso(v,w)<distancia[w]:
				distancia[w] = distancia[v]+grafo.peso(v,w)
				padre[w]=v
				heap.encolar(distancia[w],w)
	return padres, distancia
def d_infinita(distancia,v):
	return w not in distancia
```
- Si el grafo es **no pesado** -> hacer [[Recorridos sobre grafos#BFS|BFS]] porque es lineal en vez de ser $O(V+E logV)$

# Bellmand-Ford
- Dijkstra no funciona con pesos negativos. Esto soluciona BF
- Se inicializan diccionarios de ```Padres```, ```Distancia``` y que A no tiene padres y distancia 0.
- Tambien se ponen todos los vertices en infinito.
- Para el recorrido que haga, obtener todas las aristas.
- Iteras *e* veces sobre las aristas en un orden particular
- Ver del inicio hasta el fin si *mejoramos la situacion*.