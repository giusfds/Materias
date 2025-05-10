Podemos dizer que é um algoritmo melhorado do [[3_Dijkstra]], ja que o mesmo consegue fazer contas com arestas negativas.

### Como que funciona
Dado um grafo ponderado com **V vértices** e **E arestas**, junto com um **vértice de origem** (chamado src), a tarefa é calcular as **menores distâncias** do vértice de origem para todos os outros vértices.
Se um vértice for **inalcançável** a partir da origem, sua distância deve ser marcada como **10^8**.
Caso exista um **ciclo de peso negativo**, retorne **-1** para indicar que não é possível calcular os caminhos mais curtos.

#### Exemplo:
![[Bellman Ford 1.png]]

Nesse caso, para a saída do algoritmo ser \[0, 5, 6, 6, 7] temos que fazer o seguinte caminho
``0 -> 1 -> 2 -> 4 -> 3``, sendo o peso acumulado de cada vertice:
```
0 = 0 (src)
0 -> 1= 5 (0+5)
1 -> 2= 6 (5+1)
2 -> 4= 7 (6+1)
4 -> 3= 6 (7+(-1))
```
Apos ordenar a saída,  temos a saída do código

### Código
```C++
// Função de Bellman-Ford
// Parâmetros:
// - arestas: vetor contendo todas as arestas do grafo
// - V: número de vértices
// - origem: vértice de origem para calcular as distâncias
// Retorna: vetor de distâncias mínimas a partir do vértice origem
std::vector<int> bellmanFord(const std::vector<Edge>& arestas, int V, int origem) {
    // Definimos o valor "infinito" como o maior valor possível de int
    const int INF = std::numeric_limits<int>::max();

    // Inicializa o vetor de distâncias com INF, exceto a origem (distância zero)
    std::vector<int> distancia(V, INF);
    distancia[origem] = 0;

    // Relaxamento das arestas (V - 1) vezes
    for (int i = 0; i < V - 1; ++i) {
        // Para cada aresta, tenta atualizar a distância do vértice destino
        for (const Edge& e : arestas) {
            // Se a distância até o vértice de origem da aresta não é infinita,
            // e se o caminho pela aresta atual leva a um caminho mais curto
            if (distancia[e.origem] != INF && distancia[e.origem] + e.peso < distancia[e.destino]) {
                // Atualiza a distância
                distancia[e.destino] = distancia[e.origem] + e.peso;
            }
        }
    }

    // INFORMACAO FALTANTE (proximo topico)

    // Retorna o vetor com as menores distâncias a partir da origem
    return distancia;
}
```

### Ciclos negativos
Uma das coisas que temos que tomar cuidado ao aplicar o algoritmo são os ciclos negativos, que os mesmo podem gerar atualizações no peso de cada vertice a cada interação.
##### Mas o que são esses ciclos?
Ciclos negativos nada mais e que um ciclo comum em um grafo, onde a soma de cada peso das arestas resultam em um negativo. 
- Exemplo: ![[Bellman Ford 2.png]]
Nesse contexto podemos notar que: a soma geral do pesos dos vertices vão dar negativo, ou seja, > a cada nova iteração, o ciclo negativo continuará reduzindo indefinidamente o custo dos caminhos que passam por ele, tornando impossível determinar o menor caminho de forma estável. Assim, um dos objetos de parada do algoritmo tera que ser um break ou lançar uma exceção caso isso ocorra

##### Exemplo:
```C++
// Verificação de ciclos negativos
    for (const Edge& e : arestas) {
        // Se ainda for possível relaxar uma aresta, há um ciclo negativo
        if (distancia[e.origem] != INF && distancia[e.origem] + e.peso < distancia[e.destino]) {
            throw std::runtime_error("O grafo contém um ciclo de peso negativo");
        }
    }
```

O algoritmo de **Bellman-Ford** é utilizado para encontrar o **caminho mínimo a partir de um único vértice** em grafos, mesmo quando há **arestas com pesos negativos**. Ele se baseia no princípio de **relaxamento das arestas**, ou seja, atualizar a menor distância conhecida para um vértice se um caminho mais curto for encontrado.
O algoritmo realiza **(V – 1)** iterações (onde V é o número de vértices), pois o caminho mínimo entre dois vértices pode ter no máximo (V – 1) arestas. Após essas iterações, uma verificação extra permite identificar **ciclos de peso negativo**, caso alguma distância ainda possa ser reduzida.
Diferente do algoritmo de Dijkstra, Bellman-Ford **pode lidar com arestas negativas** e ainda detectar **ciclos negativos**, tornando-o mais robusto para certos problemas, apesar de ser menos eficiente em termos de tempo (complexidade O(V·E)).