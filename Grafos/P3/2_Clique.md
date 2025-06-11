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

## Conjunto Independente

Um **conjunto independente** (ou _independent set_) em um grafo é um **conjunto de vértices tal que nenhum par de vértices desse conjunto está conectado por uma aresta**. 

**Em outras palavras:**
Se você pegar dois vértices quaisquer do conjunto, **eles não podem ser vizinhos**.

#### Exemplo

```
A --- B
|     |
C     D
```

existe arestas:
A-C
A-B
B-D

Nesse meio existe alguns conjuntos independentes, sendo eles:
- {C, D} e valido, ja que C e D nao se ligam.
- {A-D} e valido, ja que A nao liga em D, mesmo tendo um caminho direto passando por B
	- o que acontece e que eles nao sao vizinhos diretos, ou seja, nao necessariamente estao ligados diretos
- {A-B} e invalido, ja que eles sao vizinhos
- {B} e valido, ja que o mesmo e independente

## Maximo conjunto independente

No grafo acima, e representado pelo conjunto de {C-D}, com tamanho de 2, isso e chamado de MIS.

## Algoritmos

1. Achar o vertice de maior ou menor grau
2. Checar se ha arestas 
	1. Se houver, incluir
	2. Se nao, ignorar

- Cobertura de vertice

1. Pega o $v \in V$ de maior grau
2. remover $v$
3. Pegar o próximo maior



[[3_Planaridade]]