# Busca em Profundidade 

A busca em profundidade pode ser implementada de forma recursiva ou usando uma pilha. Veja abaixo o pseudocódigo para a implementação recursiva:

```
DFS(G, u):
    marque u como visitado

    para cada vertice v vizinho de u:
        se v nao foi visitado:
            DFS(G, v)
```

Agora veja o pseudocódigo da implementação iterativa:

```
DFS(G, u):
    marque todos como nao visitados
    inicializa_pilha(P)

    empilha(P, u)

    enquanto a pilha nao estiver vazia
        desempilha(P) em u
        se u nao foi visitado
            marque u como visitado
            para todos os vizinhos v de u
                se v nao foi visitado
                    empilha(P, v)
```

# Busca em largura

A busca em largura pode ser implementada usando uma pilha. Veja abaixo o pseudocódigo:

```
BL(G, u):
    marque todos os vertices como nao visitados
    cria_pilha(P)

    empilhe (P, u)
    marca u como visitado

    enquanto a pilha n estiver vazia
        desempilha(P) em u
        para cada vertice v vizinho de u
            se v nao foi visitado
                empilha(P, v)
                marca v como visitado
```

# Algoritmo de Dijkstra

O algoritmo de Dijkstra é um algoritmo que encontra o menor caminho entre um vértice inicial e todos os vértices de um grafo ponderado. Ele utiliza a busca em largura para encontrar estes caminhos, porém, ao invés de utilizar uma pilha, ele utiliza uma fila de prioridade. Sua complexidade é O(E + Vlog)

```
dijkstra(grafo g, s) 
    vetor pai[g->n]
    cria_fila_prioridade_(fp, g->n)

    para i de 0 ate g->n 
        pai[i] = -1
        insere(fp, i, INT_MAX)

    pai[s] = s
    diminui_prioridade(fp, s, 0)

    enquanto fp nao estiver vazia
        u = extrai_minimo(fp)
        para cada vertice v vizinho de u
            se (prioridade(fp, v) > prioridade(fp, u) + peso(u, v))
                diminui_prioridade(fp, v, prioridade(fp, u) + peso(u, v));
                pai[v] = u
    
    retorna pai
```
