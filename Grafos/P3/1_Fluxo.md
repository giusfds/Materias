# Fluxo em Redes

Em um grafo direcionado, podemos atribuir pesos $w$ às arestas, onde cada aresta $(u, v)$ tem um peso positivo, ou seja, $w(u, v) > 0$. Suponha que não há perda durante a trajetória de um fluxo: se um valor $10$ sai de $u$, então esse mesmo valor $10$ chega em $v$.

## Caminhos disjuntos

Dessa forma, é possível encontrar até $n$ caminhos disjuntos entre um vértice inicial $S$ e um vértice final $T$. Para simplificar, podemos considerar que cada aresta tem capacidade $w = 1$, ou seja, permite a passagem de no máximo uma unidade de fluxo. Esse modelo é conhecido como **fluxo em redes**.

## Teorema do Fluxo Máximo

Para resolver problemas desse tipo, aplicamos o **Teorema do Fluxo Máximo**, que busca encontrar a maior quantidade de fluxo que pode ser enviada de $S$ até $T$, respeitando as capacidades das arestas.

Uma das abordagens para resolver esse problema consiste em construir um **grafo residual**, que nos permite acompanhar quanto fluxo ainda pode ser enviado por cada caminho.

### Algoritmo 
#### (ideia geral)

1. Inicialize o fluxo em todas as arestas como 0.
2. Enquanto existir um caminho de aumento de $S$ a $T$ no grafo residual:
   - Encontre esse caminho.
   - Envie o fluxo máximo possível por ele (respeitando a menor capacidade do caminho).
   - Atualize as capacidades residuais.

Esse processo continua até que não existam mais caminhos de aumento, ou seja, atingimos o **fluxo máximo**.

#### **Ford-Fulkerson**

O algoritmo de **Ford-Fulkerson** é uma das formas mais clássicas de resolver o problema do fluxo máximo. Ele se baseia na ideia de **caminhos de aumento** em um **grafo residual**, seguindo os seguintes passos:

1. Inicialize o fluxo em todas as arestas como 0.
2. Enquanto existir um caminho de aumento de $S$ a $T$ no grafo residual:
    - Encontre um caminho de $S$ a $T$ (ex: usando busca em profundidade ou largura).
    - Encontre a **capacidade mínima** do caminho (gargalo).
    - Envie esse fluxo pelo caminho.
    - Atualize as capacidades do grafo residual (incluindo arestas reversas).

O algoritmo termina quando não há mais caminhos de aumento, e o fluxo atual é o **fluxo máximo.** 

>[!note]
> A eficiência do algoritmo depende da forma como os caminhos de aumento são escolhidos





---

> 💡 Exemplos clássicos de aplicação:
> - Transporte de mercadorias
> - Fluxo de dados em redes de comunicação
> - Escalonamento de tarefas
> - Caminhos disjuntos em grafos

[[2_Clique]]