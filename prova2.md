# Árvores

As árvores são conhecidas como uma estrutura de dados não linear. Elas não armazenam dados de modo linear. Elas organizam os dados de modo hierárquico.

Uma árvore é um conjunto de entidades chamadas nós. Os nós são conectados por arestas. Cada nó contém um valor ou dados e pode ou não ter um nó filho.

A altura de uma árvore é o tamanho do caminho mais longo até uma folha. A profundidade de um nó é o tamanho do caminho percorrido do nó até a raiz.

Obs.: começaremos contando os níveis a partir do zero, portanto, a raiz está sempre no nível 0.

# Árvores Binárias

É uma árvore cujos nós possuem grau no máximo 2.
Para as árvores binárias, vamos ver as seguintes implementações:

- Struct de árvore binária
- Criação da árvore
- Busca na árvore
- Percurso em profundidade: Pré-ordem
- Percurso em profundidade: Em-ordem
- Percurso em profundidade: Pós-ordem
- Percurso em largura

Não veremos a inserção e a remoção por enquanto, a partir dos próximos tópicos já veremos.

## Implementação
    
- Struct de árvore binária

A struct de uma árvore será chamada de nó, e vai conter um campo pra guardar o dado, que no caso será um valor inteiro, depois um ponteiro para o nó da esquerda e um ponteiro para o nó da direita.

```
typedef scruct no {
    int dado;
    scruct no *esq;
    struct no *dir;
} no;
```

- Criação da árvore

A função para criar uma árvore é muito simples, ela recebe como parâmetro o dado que será inserido na raiz, e os ponteiros para os nós da esquerda e da direita, e retorna um ponteiro para o nó raiz.

Na função, começamos alocando memória para o nó que será a nossa raiz, e depois atribuimos o determinado valor a cada campo, depois, retornamos a raiz.

```
no *cria_arvore(int dado, no *esq, no *dir) {
    no *raiz = malloc(sizeof(no));
    raiz->dado = dado;
    raiz->esq = esq;
    raiz->dir = dir;
    return raiz;
}
```

Lembrando que através da função **cria_arvore**, é possível popular toda uma árvore, mesmo sem a função de inserir. Para isso, começamos inserindo de baixo para cima, veja o exemplo:

```

            3
    4             7
 6     8       2    1
    10
```

Começamos inserindo o último nó, no caso o 10.
```
no *p1 = cria_arvore(10, NULL, NULL);
```
Agora, vamos criar o no 8, que tem como filho o nó 10.
```
p1 = cria_arvore(8, NULL, p1);
```
Agora, vamos criar o nó 6, que não possui filhos.
```
no *p2 = cria_arvore(6, NULL, NULL);
```
Agora vamos criar o nó 4, que possui como filhos os nós 6 e 8.
```
p1 = cria_arvore(4, p2, p1);
```
Agora, já temos a subárvore a esquerda, que está armazenada em p1.

Criaremos agora o nó 2:
```
p2 = cria_arvore(2, NULL, NULL);
```

Criamos agora o nó 1, e como o p1 está armazenado nossa subárvore esquerda e p2 está armazenando o nó 2, então, precisamos de um novo ponteiro.
```
no *p3 = cria_arvore(1, NULL, NULL);
```

Agora vamos pro nó 7:
```
p3 = cria_arvore(7, 02, p3);
```
Agora, já podemos criar nossa raiz e terminar nossa árvore:
```
p3 = cria_arvore(3, p1, p3);
```
- Busca na árvore

Na busca, começamos passando como parâmetro a raiz da árvore e o dado buscado. Se a raiz for nula ou o dado for o da raiz, retornamos a raiz, se não, buscamos na esquerda, se a esquerda for diferente de nulo, retornamos o que foi encontrado, se não, buscamos na direita e retornamos o que foi encontrado.

```
int busca(no *raiz, int x) {
    if (raiz==NULL || raiz->dado == x) return raiz;
    no *esq = busca(raiz->esq, x);
    if (esq != NULL) return esq;
    return busca(raiz->dir, x);
}
```

- Percurso em profundidade: Pré-ordem

O percurso em Pré-ordem começa da raiz, depois visita a esquerda, e depois a direita.
```
void pre_ordem(no *raiz) {
    if (raiz != NULL) {
        printf("%d", raiz->dado);
        pre_ordem(raiz->esq);
        pre_ordem(raiz->dir);
    }
}
```

Também é possível implementar este percurso de forma não recursiva, utilizando uma pilha.

Empilha-se a raiz, e depois remove-a, ao remover, empilha-se seu filho esquerdo e seu filho direito.

- Percurso em profundidade: Em-ordem

O percurso em Em-ordem começa da esquerda, depois visita a raiz, e depois a direita.
```
void em_ordem(no *raiz) {
    if (raiz != NULL) {
        em ordem(raiz->esq);
        pritnf("%d", raiz->dado);
        em ordem(raiz->dir);
    }
}
```

- Percurso em profundidade: Pós-ordem

O percurso em Pós-ordem começa da esquerda, depois visita a direita, e depois a raiz.
```
void pos_ordem(no *raiz) {
    if (raiz != NULL) {
        pos_ordem(raiz->esq);
        pos_ordem(raiz->dir);
        printf("%d", raiz->dado);
    }
}
```

- Percurso em largura

O percurso em largura pode ser feito usando uma fila, na qual primeiro enfileira-se a raiz, depois remove-a, e ao remover, insere-se seu filho esquerdo e depois seu filho direito. 
```
void largura(no *raiz) {
    enfileira(raiz);
    while(!=fila_vazia()){
        no *aux = desenfileira();
        printf("%d", aux->dado);
        if (aux->esq != NULL) enfileira(aux->esq);
        if (aux->dir != NULL) enfileira(aux->dir);
    }
}
```

# Árvores Binárias de Busca

A árvore binária de busca é um tipo de árvore binária que possui a seguinte propriedade:

raiz->esq->dado < raiz->dado < raiz->diz->dado

Neste tipo de árvore, vamos ver 3 operações:

- Busca
- Inserção
- Remoção
- Remoção do sucessor

As outras operações já vistas, com exceção da busca, podem ser utilizadas também na árvore binária de busca.

- Busca
A busca binária funciona da seguinte forma: se o dado buscado é menor que o dado da raiz, ele tá na subárvore a esquerda, e se for maior, está ba subárvore a direita.

```
int busca_binaria(no *raiz, int x) {
    while (raiz != NULL && raiz->dado != x) {
        if (x < raiz->dado)
            raiz = raiz->esq;
        else
            raiz = raiz-> dir;
    }
    return raiz;
}
```

O pior caso de complexidade de 0(n), quando a árvore é uma lista encadeada, portanto, desbalanceada.

O melhor caso é O(log n), quando a árvore está balanceada.

- Inserção

Na inserção, caso a raiz seja nula, criamos uma raiz, da mesma forma feita na função "cria_arvore", se não, inserimos o novo nó na subárvore correta.

```
no *insere(no *raiz, int dado) {
    if (raiz == NULL) {
        no *raiz = malloc(sizeof(no));
        raiz->dado = dado;
        raiz->esq = NULL;
        raiz->dir = NULL;
        return raiz;
    }

    if (dado < raiz->dado) {
        raiz->esq = insere(raiz->esq, dado);
    } else {
        raiz ->dir = insere(raiz->dir, dado);
    }

    retun raiz;
}
```

- Remoção

A remoção pode acontecer em três tipos de nó.

Se ele for folha, basta remover e redefinir esq ou dir como pai.

Se for um nó com subárvore esquerda (ou direita) nula, basta remover e redefinir esq/dir do pai como esq/dir do nó.

Se for um nó com subárvore esquerda e direita não nulas, remove o menos à direita (ou menor a esquerda).

```
no *remove (no *raiz, int ch) {
    if (raiz == NULL) return NULL;

    if (ch < raiz->dado) 
        raiz->esq = remove(raiz->esq, ch);
    else if (ch > raiz->dado)
        raiz->dir = remove(raiz->dir, ch);
    else {
        if (raiz->esq == NULL) 
            return raiz->dir;
        else if (raiz->dir == NULL)
            return raiz->esq;
        else {
            int nova ch;
            raiz->dir = removeSucessor(raiz->dir, &nova_ch);
            raiz->dado = nova_ch;
        } return raiz;
    }
}
```

- Remoção do sucessor

```
no *removeSucessor(no *raiz, int *ch) {
    if (raiz->esq == NULL) {
        *ch = raiz->dado;
        return raiz->dir;
    }

    raiz->esq = removeSucessor(raiz->esq, ch);
    return raiz;
}
```

# Árvores Rubro-Negra Esquerdistas

As árvores rubro-negras esquerdistas são árvores binárias de busca que possuem as seguintes propriedades:

1. Todo nó é vermelho ou preto
2. A raiz é preta
3. Se um nó é vermelho, 
    então seus filhos são pretos
    seu pai é preto
4. Em cada nó, o caminho para qualquer uma de suas folhas possui a mesma quantidade de nós pretos, essa propriedade se chama altura negra
5. As folhas são nulas e tem a cor preta
6. A altura de uma árvore rubro-negra esquerda é O(log n), pois é uma árvore binária de busca.
7. Todo nó inserido é vermelho

## Operações de correção

Como podemos ver, uma árvore rubro-negra possui muitas regras, portanto, ao inserir ou remover um elemento, é preciso corrigir a árvore para que todas as regras volte a ser obedecidas.

- Rotação à esquerda
![Rotação a esquerda](./imagens/rotacao-pra-esquerda.png)
- Rotação à direita
![Rotação a direita](./imagens/rotacao-pra-direita.png)
- Subir a cor
![Subir a cor](./imagens/sobe-cor.png)

Para começar, vamos definir um ENUM para as cores, e uma struct para a árvore.

```
typedef enum {VERMELHO, PRETO} cor;
```

```
typedef struct no {
    int dado;
    struct no esq, dir;
    enum cor cor;
} no;
```

Agora, vamos entender em que caso usaremos cada uma das funções de correção:

1. Raiz com filho esquerdo preto e filho direito vermelho:
    - Rotação à esquerda
2. Raiz preta com filho esquerdo e direito vermelhos:
    - Subir a cor
3. Raiz preta com filho esquerdo vermelho e neto esquerdo vermelho:
    - Rotação à direita
    - Subir a cor

Agora, vamos ver a implementação das funções de correção:

- Rotação à esquerda

```
no *rotacao_esquerda(no *raiz) {
    no *aux = raiz->dir;
    raiz->dir = aux->esq;
    aux->esq = raiz;
    aux->cor = raiz->cor;
    raiz->cor = VERMELHO;
    return aux;
}
```
- Rotação à direita
```
no *rotacao_direita(no *raiz) {
    no *aux = raiz->esq;
    raiz->esq = aux->dir;
    aux->dir = raiz;
    aux->cor = raiz->cor;
    aux->cor = VERMELHO;
    return aux;
}
```

- Sobe cor
```
void sobe_cor(no *raiz) {
    raiz->cor = VERMELHO;
    raiz->esq->cor = PRETO;
    raiz->dir->cor = PRETO;
}
```

- Inserção

Para inserir, teremos duas funções:

```
no *insere(no *raiz, int ch) {
    raiz = insere_rec(raiz, ch);
    raiz->cor = PRETO;
    return raiz;
}
```

```
no *insere_rec(no *raiz, int ch) {
    if (raiz == NULL) {
        no *novo = malloc(sizeof(no));
        novo->dado = ch;
        novo->esq = NULL;
        novo->dir = NULL;
        novo->cor = VERMELHO;
        return novo;
    }

    if (ch < raiz->dado) {
        raiz->esq = insere_rec(raiz->esq, ch);
    } else {
        raiz->dir = insere_rec(raiz->dir, ch);
    }

    return corrige(raiz);
}
```

- Função de correção

Relembrando, podemos ter 3 casos em que necessitamos de correção, são eles:

1. Raiz com filho esquerdo preto e filho direito vermelho:
    - Rotação à esquerda
2. Raiz preta com filho esquerdo e direito vermelhos:
    - Subir a cor
3. Raiz preta com filho esquerdo vermelho e neto esquerdo vermelho:
    - Rotação à direita
    - Subir a cor

```
no *corrige(no *raiz) {
    if (raiz == NULL) return raiz;

    if (raiz->dir && raiz->esq) {
        if (raiz->dir->cor == VERMELHO && raiz->esq->cor == PRETO) {
            raiz = rotacao_esquerda(raiz);       
        } else if (raiz->dir->cor == VERMELHO && raiz->esq->cor == VERMELHO) {
            sobe_cor(raiz);
            return raiz;}
    } else if (raiz->esq && raiz->esq->esq) {
        if (raiz->esq->cor == VERMELHO && raiz->esq->esq->cor == VERMELHO){
            raiz = rotacao_direita(raiz);
            sobe_cor(raiz);
            return raiz;
        }
    }
}
```

# Heap

Uma heap é uma fila de prioridade onde o dado guardado em cada raiz é sempre maior que o dado guardado em seus filhos.

Uma max-heap é uma árvore binária quase completa. Uma árvore binária quase completa é uma árvore binária se todos os níveis estiverem cheios, com exceção do último. Veja abaixo um exemplo:

![max heap](./imagens/max-heap.jpg)

Agora, vamos analisar como encontrar o pai e os filhos de um nó, considerando o nó V[i].

- Pai de V[i]: V[i-1/2];
- Filho esquerdo de V[i]: V[2i+1];
- Filho direito de V[i]: V[2i+2];

Para este tipo de árvore binária, vamos implementar:

1. Struct de heap
2. Criação da heap
3. Inserção
4. Função sobe no heap
5. Remoção
6. Função desce no heap

- Struct de heap

```
typedef struct {
    int *V;
    int n;
    int tam;
} FP;

```

- Criação da heap

```
FP *cria_heap (int tam) {
    FP *fp = malloc(sizeof(FP));
    fp->V = malloc(tam*sizeof(int));
    fp->n = 0;
    fp->tam = tam;
}

```
- Inserção

```
void insere(FP *fp, int dado) {
    fp->V[fp->n] = dado;
    fp->n++;

    sobe_no_heap(fp, fp->n-1);
}
```

Na inserção, inserimos o novo elemento na última posição do vetor, por isso, precisamos da função "sobe_no_heap" para que o elemento inserido possa subir na árvore até a posição correta.

```
void sobe_no_heap(FP *fp, int i) {
    if (i>0 && fp->V[i] > fp->V[(i-1)/2]) {
        troca(V, i, (i-1)/2);
        sobe_no_heap(fp, (i-1)/2);
    }
}
```

- Remoção

Para remover um elemento, vamos trocar o primeiro elemento com o último, para que seja possível remover o último elemento. Depois, chamamos a função "desce_no_heap" para que o elemento que trocou de lugar com a raiz volte ao seu devido lugar.

```
int remove(FP *fp) {
    troca(fp->V, 0, fp->n-1);
    fp->n--;
    desce_no_heap(fp, 0);
    return fp->V[fp->n];
}
```

```
void desce_no_heap(FP *fp, int i) {
    int maior_filho;
    int esq = i*2 + 1;
    int dir = i*2 + 2;

    if (esq < fp->n) {
        maior_filho = esq;
        if (dir < fp->n && fp->V[dir] > fp->V[esq]) {
            maior_filho = dir;
        }

        if (fp->V[i]<fp->V[maior_filho]) {
            troca(fp->V, i, maior_filho);
            desce_no_heap(fp, maior_filho);
        }
    }
}
```

