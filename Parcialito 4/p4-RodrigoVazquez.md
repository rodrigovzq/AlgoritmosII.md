3. En un juego, un jugador comienza en un estado "inicio", pasa por distintos estados (por ejemplo, "entrenar para
batalla", "pasar a nivel 5", etc) y finalmente llega a un estado final llamado "campeón del juego". Según la acción
que realice un jugador puede pasar de un estado a otro. No se puede pasar de cualquier estado a cualquier otro. Algunos de
esos pasajes le harán perder una cantidad de energía, y otros le harán ganar. No hay un máximo de energía que el jugador
pueda tener (puede acumular para usar en futuras batallas).
	a. Explicar cómo se puede modelar este problema con un grafo.
	b. Diseñar un algoritmo (en pseudocódigo) que nos permita llegar desde el estado "inicio" hasta el estado "campeón
	del juego" con la mayor cantidad de energía posible.
	c. Explicar qué problemática podría suceder en este escenario, y cómo lo puede detectar el algoritmo planteado.

---
a. El problema se puede modelar considerando un grafo con vertices representando los distintos estados del juegador y con aristas que sean dirigidas desde un estado anterior a uno siguiente. En el peso de las aristas podria considerarse la energia que el jugador gane o pierda al pasar de un estado a otro.
b. 
```python
energia_final = max(flujo(grafo,s,t)) #obtiene flujo maximo
def ganar(grafo,s,t,energia,peso):
	padres, origen = dfs(grafo,s)
	
	
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
def _dfs(grafo, v,visitados,padres, orden):
	for w in grafo.adyacentes(v):
		if w not in visitados:
			visitados.add(w)
			padres[w]=v
			orden[w]=orden[v]+1
			dfs(grafo,w,visitados, padres, orden)
	return padres,origen
```
c.

---
7. Definir si las siguientes afirmaciones son verdaderas o falsas. Justificar.
	a. Al resolver el problema de maximización de flujo buscamos caminos entre la fuente y el sumidero en la red residual. Si
	en dicho camino se utiliza una arista que no existe en el grafo original, significa que el flujo en la arista original (la del
	grafo original) se debe disminuir, por lo que el flujo total también disminuye.
	b. No podemos resolver el problema de maximización de flujo si hay ciclos en el grafo.
	c. Podemos calcular el Árbol de tendido mínimo de un grafo no dirigido que tenga pesos negativos.

---
a. VERDADERO. Si al buscar el camino minimo entre la fuente y el sumidero se atravesara una arista que no se encontraba en el grafo original es porque significa que al hacer el recorrido estaria "yendo para atras" entonces por eso se resta el flujo.

b. FALSO. La limitacion para ciclos es de solamente dos aristas ( aristas antiparalelas). Puede haber ciclos de mas de dos aristas para resolver un problema de maximizacion de flujo.

c. VERDADERO. Los algoritmos de Prim y Kruskal funcionan con pesos negativos y estos sirver para calcular Arbol de tendido minimo
