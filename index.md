
# Anytime Automatic Algorithm Selection for Graph Coloring



### Dataset

* [Graph Coloring instances](https://drive.google.com/file/d/1TloL47siY5cHSEq8Bb9t7DgUVaUq3tiA/view?usp=sharing) This zip file contains 6379 in DIMACS format [reference] (http://prolland.free.fr/works/research/dsat/dimacs.html).
* [Features](https://drive.google.com/file/d/1sKfCg24mcJPPhu5IAcGDfCizBVClULG-/view?usp=sharing): This file contains 6379 instances with 82 features calculated.
* [Solver results](https://drive.google.com/file/d/143Ekm588NObz0f-6FK0q5l1z8LLRQe28/view?usp=sharing) 

### How to load the data

to use the instances in python, we recommend using the networkx [networkx] (https://networkx.org/).
```python
def read_graph(filename):
    archivo = open(filename,"r")
    lista_arcos = []
    for linea in archivo.readlines():
        linea = linea.replace("   "," ").split(" ")
        if("p" in linea[0]):
            nodos,arcos = int(linea[2]),int(linea[3])
        if("e" in linea[0]):
            to,fro = int(linea[1])-1,int(linea[2].strip())-1
            lista_arcos.append((to,fro))
    lista_arcos_ = [(x,y) for (x,y) in lista_arcos]
    return nodos,lista_arcos_

def create_graph(nodos,lista_arcos):
    from networkx import Graph
    G=Graph()
    G.add_nodes_from(arange(1,nodos))
    G.add_edges_from(lista_arcos)
    return G

nodos,lista_arcos = read_graph("1-FullIns_3.col")
G = create_graph(nodos,lista_arcos)
```

For Python, we recommend using pandas to open files:
```python

import pandas as pd
features = pd.read_csv("features_gc.csv")
solver_results = pd.read_csv("execution_times.csv")
```
