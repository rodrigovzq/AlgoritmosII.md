# Caminos Minimos
## Dijkstra
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

## Bellmand-Ford
- Dijkstra no funciona con pesos negativos. Esto soluciona BF
- Se inicializan diccionarios de ```Padres```, ```Distancia``` y que A no tiene padres y distancia 0.
- Tambien se ponen todos los vertices en infinito.
- Para el recorrido que haga, obtener todas las aristas.
- Iteras *e* veces sobre las aristas en un orden particular
- Ver del inicio hasta el fin si *mejoramos la situacion*.

```python
def bellman_ford(grafo,origen):
	padre={}
	distancia={}
	padre[origen]=None
	distancia[origen]=0
	aristas= obtener_aristas(grafo)
	for i in range(len(grafo)): #V veces
		cambio = False
		for v,w,peso in aristas:
			if distancia[v]+peso < distancia[w]: # mejoro la situacion
				padre[w]=v
				distancia[w]=distancia[v]+peso
				cambio = True
		if not cambio: # convergió–
			break
	
	for v,w,peso in aristas:
		if distancia[v] + peso < distancia[w]:
			return None # encontro un ciclo negativo
	return padre, distancia
		
```

```python
def obtener_aristas(grafo):
	aristas=[]
	for v in grafo:
		for w in grafo.adyacentes(v):
			aristas.append((v,w,grafo.peso(v,w)))
	return aristas
```

- El orden es $O(V*E)$ 
- En todos los casos que funciona [[Algoritmos sobre grafos#Dijkstra|Dijkstra]], funciona Bellmand-Ford.
- Si el grafo es no pesado, se usa [[Recorridos sobre grafos#BFS|BFS]] porque es el mas rapido
- Si el grafo es pesado, BFS no funciona, uso Dijkstra si los pesos no son negativos.
- Si es un grafo dirigido y los pesos pueden ser negativos, se usa Bellmand-Ford

# Arbol de Tendido Minimo
A partir de un grafo, devuelve un un arbol que minimice el pesos total sumando las aristas involucradas.

## Prim
- Empezar por un vertice al azar -> A
- Tengo set de vertices *visitados*-> evita ciclos.
- Creo **nuevo grafo** que va a ser un arbol
- Visito A
- Encolar todas las aristas adyacentes al origen en un heap de minimos -> (V,W,peso)
- Repito mientras que el heap no este vacio
	- Desencolo y me fijo si el extramo *w* esta visitado
	- Si *w* no fue visitado, lo visito, **agrego la arista** y encolo todas las aristas adyacentes a *w*
	- Si *w* fue visitado, **descarto la arista**
-   Es único? La justificación no es por el vértice inicial, sino porque:=
	-   puede haber varios caminos del mismo peso que haya decidido tomar antes.
-   Orden $O (E log V)$

```python
def prim(grafo):
	v = grafo.vertice_random()
	visitados = set()
	visitados.add(v)
	heap = Heap() #usar heap Q
	for w in grafo.adyacentes(a): # encolo todas las aristas
		heap.encolar((v,w),grafo.peso(v,w))
	#creo arbol con los mismo vertices
	arbol = Grafo(es_dirigido=False,lista_vertices=grafo.obtener_vertices())
	
	while not heap.esta_vacio():
		(v,w), peso = heap.desencolar()
		if w not in visitados:
			arbol.agtergar_arsita(v,w,peso)
			visitados.add(w)
			for x in grafo.adyacentes(w):
				if x not in visitados:
					heap.encolar((w,x),grafo.peso(w,x))
	return arbol
	
```

## Kruskal
- Ordena las aristas de menor a mayor
- Recorro esa lista y pregunto si pertenencen a la misma componente conexa
	- Si **no** son de la misma componente -> **uno**
- SI son de la misma componente conexa -> ignoro.
- Este algoritmo, si el grafo no es conexo, obtiene el *bosque* de tendido minimo
- Cual es el problema?
	- Ordenar las aristas es -> $O(ElogE)$=$O(ElogV)$ (por acotacion)
	- Obtener la componenete conexa necesito **miniTDA** -> UnionFind
```python
def kruskal(grafo):
	conjuntos = UnionFind(grafo.obtener_vertices())
	aristas = sorted(obtener_aristas(grafo), key=lambda arista:arista[PESO])
	## aristas = ordenar(obtener_aristas(grafo)) en pseudocodigo
	arbol = Grafo(es_dirigido=False,lista_vertices=grafo.obtener_vertices())
	
	for a in aristas:
		v, w, peso = a
		if  conjuntos.find(v) != conjuntos.find(w): ## del TDA UnionFind
			arbol.agregar_arista(v, w, peso)
			conjuntos.union(v,w)
	return arbol
	
```
      

### mini TDA: UnionFind

-   Solo va a tener 2 primitivas
	-   Unir dos conjuntos
	-   Ver si pertenecen al mismo grupo
-   Find -> O(1)-> O( α ^-1 (e))
-   Union -> O(n): porque tengo que recorrer todo un grupo para cambiarle el grupo.
-   Tengo que mejorarlo porque pierde el sentido de agregar un TDA si no mejora la situación previa. Quiero que cueste mejor que lineal.
-   Como mucho ser logarítmicos.
-   Otra implementación: @1:10
	-   O( α-1(E)) mejor que O(logE),
	-   α es la función de Ackerman, crece muy rápido y la inversa crece muy lento.
	-   casi lineal, pero no es lineal.

```python
class UnionFind:
	def __init__(self,items):
		# self.groups = {i:i for i in items}
		self.groups={}
		for i in items:
			self.groups[i] = i
	
	def find(self,v):
		if self.groups[v] == v
			return v
		real_group = self.find(self.groups[v])
		# plancho al estructura
		self.groups[v] = real_group
		return real_group
	
	def union(self,u,v):
		new_group = self.find(u)
		other = self.find(v)
		self.group[other]=new_group
```