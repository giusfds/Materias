### AGM

Antes mesmo de falar sobre Floresta Geradora Minina, temos que arender o que e uma AGM.

> Uma **árvore geradora mínima** (AGM) de um grafo conexo e ponderado é uma subárvore que inclui **todos os vértices do grafo**, **sem formar ciclos**, e cuja **soma dos pesos das arestas é mínima** entre todas as possíveis árvores geradoras.

##### **Características:**

- Só existe se o grafo for **conexo**.
    
- Uma árvore com **|V| - 1 arestas**, onde |V| é o número de vértices.
    
- Pode haver mais de uma árvore geradora mínima se houver empates nos pesos.

### Floresta Geradora Minima

> Uma **floresta geradora mínima** é a união das **árvores geradoras mínimas de cada componente conexo** de um grafo não conexo e ponderado.

##### **Em outras palavras:**

- Se o grafo tiver várias partes desconexas (vários componentes conexos), não dá pra ter uma única árvore ligando tudo — então cada parte vira sua **própria árvore geradora mínima**, e o conjunto dessas árvores forma a **floresta geradora mínima**.
    
- A floresta conecta todos os vértices **dentro de cada componente**, com **o menor custo possível** e **sem ciclos**.

##### Exemplo visual

```
Componente 1:       Componente 2:

A---1---B           D---2---E
 \      |           |1
  \--3--C           F
```

- A AGM do componente 1 pode ser B-A-C com a soma de pesos dando 4 (3+1)
- A AGM do componente 2 pode ser E-D-F com a soma de pesos dando 3 (2+1)
Juntando as duas AGM, temos uma floresta geradora minima.

##### Outra maneira de escrever uma AGM

![[AGM.png]]

> Considerando esse grafo, é possível organizar os vértices em uma **ordem topológica**, ou seja, dispor os nós em uma lista linear de forma que, para toda aresta do tipo u \rightarrow v, o nó u apareça antes de v. Essa ordenação respeita as dependências entre os nós e pode influenciar a forma como eles são processados ou “alcançados” durante a execução de algoritmos.


Levando em conta os algoritmos que ja conhecemos, podemos colocar os nos, podeos escrever de forma:

###### Prim
P = A, B, C, G, D, E, K, H, F
###### Kuskal
K= A, B, E, C, G, D, K, H, F