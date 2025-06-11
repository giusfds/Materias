- Grafo dual (nao direcionado)

- Face = região de vertices e arestas
	$\to$ regiao delimitada por vertices e arestas $(u,v)$ 

- $v \times f = a \times 2$  
	$\to$ Ao adicionar uma aresta, adiciona-se também uma face

```
A-----B
|     |
|     |
C-----D
 \   /
  \ /
   O
```

Dado o grafo acima, podemos notar que o mesmo tem duas faces visíveis sendo elas um quadrado e um triangulo, o que temos que tomar cuidado e que temos a terceira face escondida, que seria a parte de fora do grafo, o todo.

Não ha faces em Kn (G completo)

### Definições

- Grafo planar: grafo onde arestas, sejam elas quais quer, não se cruzam
- Se um grafo todas as faces são triângulos, então o limite de planaridade foi atingido
- Aplicável em construções de estradas e rodovias

## Teoremas

$\to$ Teorema de **Kurathoski**
	Esse teorema ``AFIRMA`` que todo e qualquer grafo e planar a não ser que haja um grafo $K_5$ ou um $K_3,_3$, já que esses dois grafos são **IMPOSSÍVEIS** de virar planar, mesmo com a suavização de vertices
		$\to$ suavização de um vertice e juntar 2 vertices, sendo vizinhos um ao outro, em apenas um, assim tendo um "duplo vertice"
$\to$ Teorema de **Wagner**
	Esse teorema fala paraticamente a mesma coisa do teorema anterior, porem sem a parte de suavizar as arestas
$\to$ Formula de **Euler**
	Para um grafo planar com vertices ($v$), arestas ($e$) e faces ($f$), existe a formula para saber se os grafos podem ser desenhados no plano sem que se cruzem. É dada pela formula:
		$\to V - A + F = 2$
	Assim, podemos colocar em pratica de forma:
		$\to$ V = 4 vertices
		$\to$ A = 5 arestas
		$\to$ F = 3 faces
	Colocando esses valores na formula, podemos concretizar que:
		$4 - 5 + 3 = 2$ 
	Assim, sendo uma das formulas bases para o primeiro teorema