É o algoritmo mais comum quando se trata de menor caminho possível dentro de um grafo.

### O que é Dijkstra
O algoritmo mantém dois grupos de vértices: os que já foram visitados e os que ainda não foram. Ele começa no vértice inicial (origem) e, a cada passo, escolhe o vértice não visitado que está mais próximo da origem. Depois, ele olha os vizinhos desse vértice e atualiza a distância deles, caso encontre um caminho mais curto. Esse processo continua até chegar no destino ou até visitar todos os vértices que podem ser alcançados.

### O Dijkstra pode funcionar em grafos não direcionados

>[!NOTE]
>O algoritmo funciona em ambos os grafos, contanto que ele nao tenha arestas negativas (que e o requisito minimo para o algoritmo funcionar)

- **Grafo direcionado**: Cada aresta tem uma direção, ou seja, mostra para onde é possível ir entre os vértices conectados. Nesse caso, o algoritmo respeita essa direção na hora de procurar o caminho mais curto.
- **Grafo não direcionado**: As arestas não têm direção, ou seja, é possível ir e voltar por elas. Assim, o algoritmo pode seguir em qualquer sentido ao buscar o caminho mais curto.

### Passo a passo do algoritmo
1. Marque o nó de origem com uma distância atual de 0 e os demais com infinito.
    
2. Defina o nó não visitado com a menor distância atual como o nó atual.
    
3. Para cada vizinho **N** do nó atual, some a distância atual do nó com o peso da aresta que conecta os dois. Se esse valor for menor que a distância atual de **N**, atualize a distância de **N** com esse novo valor.
    
4. Marque o nó atual como visitado.
    
5. Volte ao passo 2, caso ainda existam nós não visitados.

### Como que ele funciona
_Considerando o grafo a baixo, vamos passo a passo_
![[Dijikstra Exemple.png]]

O algoritmo irá gerar o caminho mais curto do nó 0 para todos os outros nós no grafo.
Para este grafo, vamos assumir que o peso das arestas representa a distância entre dois nós.
Inicialmente temos:
- A distância do nó de origem para ele mesmo é 0. Neste exemplo o nó de origem é o 0.
- A distância do nó de origem para todos os outros nós é desconhecida, então marcamos todos eles como infinito.
Exemplo: 0 -> 0, 1 -> ∞, 2 -> ∞, 3 -> ∞, 4 -> ∞, 5 -> ∞, 6 -> ∞.
- Também teremos um array de elementos não visitados que irá manter o controle dos Nós não visitados ou não marcados.
- O algoritmo será concluído quando todos os nós forem marcados como visitados e a distância entre eles for adicionada ao caminho. Nós não visitados:- 0 1 2 3 4 5 6.

**Passo 1**: Comece pelo Nó 0 e marque o Nó como visitado, como você pode ver na imagem abaixo o Nó visitado está marcado em vermelho.

![[Dijikstra 1.png]]

**Passo 2**: Verifique os Nós adjacentes. Agora temos duas opções (ou escolhemos o Nó 1 com distância 2 ou escolhemos o Nó 2 com distância 6) e escolhemos o Nó com a menor distância. Neste passo, o **Nó 1** é o Nó adjacente com a menor distância, então o marcamos como visitado e somamos a distância.
**Distância: Nó 0 -> Nó 1 = 2**
![[Dijikstra 2.png]]
**Passo 3**: Em seguida, avance e verifique o Nó adjacente, que é o Nó 3, então marque-o como visitado e some a distância. Agora a distância será:
**Distância: Nó 0 -> Nó 1 -> Nó 3 = 2 + 5 = 7**
![[Dijikstra 3.png]]
**Passo 4**: Novamente temos duas opções de Nós adjacentes (podemos escolher o Nó 4 com distância 10 ou o Nó 5 com distância 15), então escolhemos o Nó com a menor distância. Neste passo, o **Nó 4** é o Nó adjacente com a menor distância, então o marcamos como visitado e somamos a distância.
**Distância: Nó 0 -> Nó 1 -> Nó 3 -> Nó 4 = 2 + 5 + 10 = 17**
![[Dijikstra 4.png]]
**Passo 5**: Novamente, avance e verifique o Nó adjacente, que é o **Nó 6**, então marque-o como visitado e some a distância. Agora a distância será:
**Distância: Nó 0 -> Nó 1 -> Nó 3 -> Nó 4 -> Nó 6 = 2 + 5 + 10 + 2 = 19**
![[Dijikstra 5.png]]
**Portanto, a menor distância a partir do vértice de origem é 19, que é a menor distância.**

### Como representar na prova
Na prova, se for provar por Dijkstra, lembrar d fazer a tabela colocando todos os vertices como ∞ e depois vai alterando cada no com o Guloso, de forma que seja um alista de prioridade (o menor caminho de vertices). lembrando de colocar os descendentes de cada vértice 

### Lista de Prioridade

1.	Inicialização:
	•	Cria-se um vetor dist\[] com as distâncias mínimas até cada vértice.
	•	Inicialmente, todas as distâncias são INF (infinito), exceto a do vértice de origem, que é 0.
2.	Fila de Prioridade:
	•	Usa-se uma fila de prioridade (min-heap) para escolher o vértice com a menor distância atual ainda não processado.
	•	Isso garante que sempre lidamos com o “melhor candidato” primeiro.
3.	Relaxamento de Arestas:
	•	Para cada vizinho v do vértice atual u, verificamos se o caminho passando por u até v é melhor (mais curto) que o caminho atual.
	•	Se for, atualizamos dist\[v] e colocamos v na fila com a nova distância.
4.	Repetição:
	•	Esse processo continua até que todos os vértices tenham sido processados, ou seja, a fila fique vazia.

> [!IMPORTANT]
> É importante ressaltar que quando se trata de lista de prioridade, o valor ja atribuído ao vertice permanece inalterado, mesmo que futuramente achamos um camino de menor peso
#### Código
```C++
void dijkstra(int origem) {
    // Fila de prioridade (min-heap) com pares (distância, vértice)
    // O menor elemento sempre fica no topo
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> fila;

    // A distância do vértice de origem até ele mesmo é 0
    dist[origem] = 0;

    // Inserimos a origem na fila
    fila.push({0, origem});

    // Enquanto houver vértices a serem processados
    while (!fila.empty()) {
        // Pegamos o vértice com a menor distância atual
        int d = fila.top().first;
        int u = fila.top().second;
        fila.pop();

        // Se a distância retirada for maior do que a já registrada, ignoramos
        // (isso evita processar vértices que já foram atualizados por caminhos melhores)
        if (d > dist[u]) continue;

        // Para cada vizinho v de u
        for (auto [v, peso] : adj[u]) {
            // Se encontramos um caminho mais curto até v passando por u
            if (dist[u] + peso < dist[v]) {
                // Atualizamos a distância de v
                dist[v] = dist[u] + peso;

                // Colocamos v na fila para continuar o processo a partir dele
                fila.push({dist[v], v});
            }
        }
    }
}
```

### Dijkstra com pesos negativos

Uma das possibilidades que temos para fazer Dijkstra com pesos negativos é dar um push nos valores, sendo assim, temos que colocar o menor peso de todas as arestas do grafo (W) e somar |K+|  neles, sendo K um numero positivo inteiro para o menor valor ficar 1.
Porem, dependendo de como é aplicado, a AGM pode mudar, assim, tornando Dijkstra uma opção não valida para grafos com E˜
[[4_Bellman-Ford]]