
## Algoritmo de Kruskal

**Selecione todas as arestas do grafo e ordene-as em ordem crescente de peso. Em seguida, adicione cada aresta à árvore geradora mínima em construção, garantindo que a inserção não forme ciclos. O processo continua até que todos os vértices estejam conectados, resultando em uma árvore de custo mínimo.**

##### Seu passo a passo é:

1. Ordena as arestas por peso (da menor para a maior).
    
2. Escolhe as arestas uma a uma, começando pela mais leve.
    
3. Adiciona a aresta à árvore geradora mínima se ela **não formar ciclo** (verificado pelo Union-Find).
    
4. Repete até adicionar n-1 arestas (onde n é o número de vértices).
    
5. Resultado: Uma árvore geradora mínima com o menor custo possível, sem ciclos.


##### Seu código é:

```C++
vector<Aresta> kruskal(int n, vector<Aresta>& arestas) {
    sort(arestas.begin(), arestas.end()); // Ordena por peso crescente
    DSU dsu(n);

    vector<Aresta> mst; // Árvore Geradora Mínima

    for (Aresta& aresta : arestas) {
        if (dsu.unite(aresta.u, aresta.v)) {
            mst.push_back(aresta); // Adiciona se não formar ciclo
        }
    }

    return mst;
}
```

ao rodar o Kuskal, e gerada uma **AGM** (Arvore Geradora Minima) de um grafo qualquer.

> Uma AGM nada mais e do que uma arvore que conecta todos os vertices de um grafo com o menor custo total possível, sem formar ciclos
> [[Floresta Geradora Minima]]

### Exemplo de AGM

Tendo em vista esse grafo:

![[Grafo Kuskal.png]]

podemos ter mais de uma geração de AGM, porem a melhor de todas e:

![[AGM kuskal.png]]

nesse exemplo podemos ver que a aresta de peso 7 foi removida por alguns fatores simples, sendo eles:
- Evitar ciclo
- Ter uma AGM de menor peso total

## Algoritmo de Prim

**A partir do grafo original, é criado um novo grafo nulo, contendo apenas os vértices e nenhuma aresta. Em seguida, o algoritmo de Prim é aplicado: escolhe-se um vértice inicial e, a cada passo, adiciona-se a menor aresta que conecta um vértice já visitado a um ainda não visitado, desde que isso não forme ciclos. Esse processo continua até que todos os vértices estejam conectados, resultando na Árvore Geradora Mínima (AGM) — ou seja, o grafo de menor peso total que conecta todos os vértices.** 

##### Seu passo a passo é:

1. Comece com um **grafo nulo**, contendo apenas um **vértice inicial** escolhido arbitrariamente.
    
2. A cada passo, entre todas as arestas que conectam **vértices já visitados a vértices não visitados**, escolha a de **menor peso**.
    
3. Adicione essa aresta à AGM e marque o novo vértice como visitado.
    
4. Repita o processo até que todos os vértices estejam conectados.
    
5.  Ao final, a AGM estará formada, com o **menor peso total possível** e **sem ciclos**

##### Seu código é:
```C++
void prim(int n, vector<vector<int>>& graph) {
    vector<int> parent(n, -1);      // Armazena a árvore geradora mínima
    vector<int> key(n, INF);        // Menor peso para chegar no vértice
    vector<bool> inMST(n, false);   // Marca os vértices já incluídos na AGM

    key[0] = 0; // Começa do vértice 0

    for (int count = 0; count < n - 1; ++count) {
        int u = -1;

        // Encontra o vértice u com a menor chave que ainda não está na AGM
        for (int v = 0; v < n; ++v)
            if (!inMST[v] && (u == -1 || key[v] < key[u]))
                u = v;

        inMST[u] = true;

        // Atualiza os pesos das arestas dos vizinhos de u
        for (int v = 0; v < n; ++v) {
            if (graph[u][v] && !inMST[v] && graph[u][v] < key[v]) {
                key[v] = graph[u][v];
                parent[v] = u;
            }
        }
    }

    // Exibe as arestas da AGM
    cout << "Arestas da AGM:\n";
    for (int i = 1; i < n; ++i)
        cout << parent[i] << " - " << i << " (peso: " << graph[i][parent[i]] << ")\n";
}
```

### Conclusão

Ambos algoritmos servem, para achar a AGM, porem de diferentes modelos. Sendo **Prim** baseado em vértices e **Kruskal** baseado em arestas 

Comparação simples:

| Algoritmo   | Baseado em | Ideal para      | Estrutura típica              |
| ----------- | ---------- | --------------- | ----------------------------- |
| **Prim**    | Vértices   | Grafos densos   | Lista de adjacência + Heap    |
| **Kruskal** | Arestas    | Grafos esparsos | Lista de arestas + Union-Find |
Logo podemos falar que:

##### **Prim**

- **Modelo baseado em vértices.**
    
- Começa de um **vértice inicial** e vai **expandindo** a árvore adicionando a **aresta de menor peso que conecta a árvore a um novo vértice**.
    
- Costuma ser mais eficiente em **grafos densos** (muitos vértices e muitas arestas), especialmente com **min-heaps e listas de adjacência**.
##### **Kruskal**

- **Modelo baseado em arestas.**
    
- Considera **todas as arestas do grafo**, ordena por peso, e **vai adicionando as menores arestas que não formam ciclos**, até conectar todos os vértices.
    
- Costuma ser mais eficiente em **grafos esparsos** (menos arestas) e funciona bem com **estrutura Union-Find (Disjoint Set Union)**.

## Proximos passos:
[[Dijkstra]]