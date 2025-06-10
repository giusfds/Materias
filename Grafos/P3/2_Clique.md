## Definição 
Um **Clique** e um grafo $G=(V,E)$ é um **subconjunto de vértices** tal que **cada par de vértices dentro desse subconjunto esta conectado por uma aresta**.

Ou melhor dizendo, **todos os vértices estão ligados entre si** $\to$ Isso é justamente um **grafo completo**.

## Subgrafo induzido

Dado um grafo $G=(V,E)$, se voce pega um **subconjunto de vértices** $S \subseteq V$, o **subgrafo induzido** por $S$ é o grafo que:
- tem os vértives de $S$
- E **todas as asrestas entre esses vértices que existe, em $G$**. 
em outras palavras, você pega os vértiecs de $S$ e **mantem exatamente as conexões que eles tinham no grafo original** 

### CLIQUE
Um **clique é um subconjunto de vértices** cujo **subgrafo induzido é um grafo completo**.

Em outras palavras: todos os vértices estão ligados entre si **no grafo original**, então quando você induz o subgrafo, ele acaba sendo completo


##### Exemplo:

```
A --- B
| \   |
|  \  |
C     D
```

nesse grafo $G$, temos o subconjunto $\{A,B,D\}$, onde, ele e um $K3$, já que todas os vertices possíveis ja estão conectados entre si, isso e um clique do grafo

## Dificuldades

A maior dificuldade de um clique, não e acha-lo, e sim saber qual e seu maior em determinado grafo, ja que isso se trata de um codigo com custo de $NP-HARD$, isso siginifica que 
- Não existe (ate hj) um algoritmo conhecido que possa resolver esse programa em tmepo polinomial
- A media que a quantidade de vértices cresce, o numero possivel de subconjuntos que precisam ser verificados, **explode exponencialmente**


Porem existem codigos que tentam achar o maior clique sem usar a força bruta, como por exemplo o algoritmo de **Bron-Kerbosch**, nao sei se o silvio comentou sobre