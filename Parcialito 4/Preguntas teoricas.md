## Indicar verdadero o falso. Justificar
-  Es posible encontrar el camino minimo entre dos vertices de un grafo no pesado usando BFS.
	**VERDADERO**, ya que el momento de visitar por primera vez un nodo, ese camino hasta ese nodo es el camino mas corto desde el nodo del inicio. BFS recorre a traves de los adyacentes y no considera pesos.

- Si buscamos el camino minimo entre dos vertices de un grafo pesado (con pesos positivos) usando Dijsktra el camino minimo encontrado puede no ser la solucion optima.
	**FALSO**, Dijkstra se trada de un algoritmo que busca el nodo mas cercano al actual que todavia no haya sido visitado (el optimo local) en pos de obtener un optimo global. Ademas, no existe ejemplo donde se pruebe que Dijkstra devuelva una solucion no optima.
