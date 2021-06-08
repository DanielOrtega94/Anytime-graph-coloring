# Anytime Automatic Algorithm Selection for Graph Coloring
This is an additional paper's webpage of [Anytime Automatic Algorithm Selection for Graph Coloring]()


We deal with the algorithm selection problem (ASP), as we previously did with [knapsack paper](https://www.sciencedirect.com/science/article/abs/pii/S0957417420304371) applied this time to the graph coloring problem. 
The ASP consists in selecting the solver that given a time budget obtains the best solution. 
For this purpose, we calculated the instances's characteristics and record the solutions's times of each solver with each instance.
Here, unlike the previous work, we focus on the graph coloring problem, with an scenario stronly dominated by the solver [Head](https://hal.archives-ouvertes.fr/hal-00925911/document), therefore we developed a strategy to deal with imbalanced scenarios.

### Dataset

Dataset
Here in after, we present the links to download the data generated and used for the development of this research:
*[Graph Coloring solvers](https://drive.google.com/drive/folders/1hp6ziPwby5IpzlW_-ocjdWySfD40HKmt?usp=sharing): This folder contains all the modified solvers used for the realization of this work.

* [Graph Coloring instances](https://drive.google.com/file/d/1TloL47siY5cHSEq8Bb9t7DgUVaUq3tiA/view?usp=sharing): This zip file contains 6380 in DIMACS format. [reference](http://prolland.free.fr/works/research/dsat/dimacs.html).
* [Features](https://drive.google.com/file/d/1sKfCg24mcJPPhu5IAcGDfCizBVClULG-/view?usp=sharing): This file contains 6380 intances with 82 features calculated.
* [Solver results](https://drive.google.com/file/d/143Ekm588NObz0f-6FK0q5l1z8LLRQe28/view?usp=sharing): This file contains the results of the solver execution. The times are reported in milliseconds.
* [Data for regression](https://drive.google.com/drive/folders/1Wb_NnFJr4rxBrREA2yBic4SdRfDgOa3x?usp=sharing):this folder contains all the files with the values used to train the regression models by solver

### How to load the data
To use the instances in python, we recommend using the networkx [networkx](https://networkx.org/).
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
