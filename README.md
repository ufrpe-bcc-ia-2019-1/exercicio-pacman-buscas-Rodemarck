# Projeto 1VA: Implementando algoritmos de busca no PAC-MAN

**NOME**: NOME DO ALUNO

## Descrição
O jogo Pac-Man consiste em mover o personagem (Pac-Man, o círculo amarelo com uma boca) em um labirinto, e tentar comer o maior número de tabletes possível, ao mesmo tempo em que deve evitar o contato com os fantasmas. O Pac-Man vence o jogo se comer todos os tabletes do labirinto. 

O projeto Pac-Man foi desenvolvido na Universidade de Berkeley para a disciplina de Introdução à Inteligência Artificial. A idéia do projeto é aplicar algumas técnicas clássicas de IA no jogo, para  servir como ferramenta da apoio para o ensino e aprendizagem de conceitos fundamentais de IA. 

Este repositório contém uma cópia do código original (mais detalhes podem ser encontrados [aqui](http://ai.berkeley.edu/search.html) ). 

## Requisitos
- Python 2.7

## Orientações iniciais
Clone o repositório, em seguida, no diretório `pacman/`, jogue uma partida digitando:

`python pacman.py`

Neste trabalho, trabalharemos em uma versão mais simples do jogo, no qual o agente Pacman tem que encontrar caminhos no labirinto para chegar a um destino. O código desse trabalho consiste de diversos arquivos Python, entretanto você só precisará editar os seguintes arquivos:

- `search.py`: Onde ficam os algoritmos de busca.
- `searchAgents.py`: Onde ficam os agentes baseados em busca. Este arquivo contém um agente de busca (SearchAgent), que planeja um caminho no mundo do Pacman e executa o caminho passo-a-passo.

Arquivos com informações importantes, que serão usadas nas soluções:

- `pacman.py`: 
O arquivo principal que roda jogos de Pacman. Esse arquivo também descreve o tipo GameState, que será amplamente usado nesse trabalho.
- `game.py`: 
A lógica do mundo do Pacman. Este arquivo descreve vários tipos auxiliares como AgentState, Agent, Direction e Grid.
- `util.py`: 
Estruturas de dados úteis para implementar algoritmos de busca.

<!---
Disponibilizamos como base para a sua implementação o código do algoritmo de busca não informada de busca em profundidade (arquivo `search-starter.py`), e -->
A sua tarefa é implementar os métodos referentes a **busca em profundidade**, **busca em largura**, **busca de custo uniforme** e **busca A\***.

## Quickstart
O agente mais simples em `searchAgents.py` é o agente `GoWestAgent`, que sempre vai para oeste (um agente reflexivo trivial). Este agente pode ganhar às vezes: 

`python pacman.py --layout testMaze --pacman GoWestAgent`

Mas as coisas se tornam mais difíceis quando virar é necessário: 

`python pacman.py --layout tinyMaze --pacman GoWestAgent`

`pacman.py` tem opções que podem ser dadas em formato longo (por exemplo, --layout) ou em formato curto (por exemplo, -l). A lista de todas as opções pode ser vista executando: 

`python pacman.py -h`

## Navegando no mapa
Primeiro, verifique que o agente de busca SearchAgent está funcionando corretamente, rodando: 

`python pacman.py -l tinyMaze -p SearchAgent -a fn=tinyMazeSearch`

O comando acima faz o agente SearchAgent usar o algoritmo de busca tinyMazeSearch, que está implementado em search.py. Este método simplesmente retorna uma sequência de movimentos pré-estabelecidos para resolver o mapa tinyMaze:

```
def tinyMazeSearch(problem):
    """
    Returns a sequence of moves that solves tinyMaze.  For any other maze, the
    sequence of moves will be incorrect, so only use this for tinyMaze.
    """
    s = Directions.SOUTH
    w = Directions.WEST
    return  [s, s, w, s, w, w, s, w]
```

Agora chegou a hora de implementar os seus algoritmos de busca para o Pacman! Lembre-se que um nó da busca deve conter não só o estado mas também toda a informação necessária para reconstruir o caminho (sequência de ações) até aquele estado. 

Importante: Todas as funções de busca devem retornar uma lista de ações que irão levar o agente do início até o objetivo. Essas ações devem ser legais (direções válidas, sem passar pelas paredes). 

## Testando o DFS
O algoritmo de busca em profundidade (DFS) está implementado na função `depthFirstSearch` do arquivo `search.py`. Teste executando: 

```
python pacman.py -l tinyMaze -p SearchAgent -a fn=dfs
python pacman.py -l mediumMaze -p SearchAgent -a fn=dfs
python pacman.py -l bigMaze -z .5 -p SearchAgent -a fn=dfs
```

A saída irá mostrar os estados explorados e a ordem em que eles foram explorados (vermelho mais forte significa que o estado foi explorado antes). 

## Projeto
a) Implemente a busca em profundidade (método `depthFirstSearch` do arquivo `search.py`). [0.5 pontos]

b) Implemente a busca em largura (método `breadthFirstSearch` do arquivo `search.py`). [0.5 pontos]

c) Implemente a busca de custo uniforme (método `uniformCostSearch` do arquivo `search.py`). [0.5 pontos]

d) Implemente a **busca A\*** (método aStarSearch do arquivo `search.py`). O algoritmo A* recebe como argumento uma função heurística. A função heurística por sua vez recebe dois argumentos: um estado no problema de busca e uma instância do próprio problema (para informações de referência).  Um exemplo trivial de função heurística é dado pela função `nullHeuristic`. [0.5 pontos]

Para testar sua implementação, você pode utilizar a heuristica da distancia de Manhattan (implementada no método `manhattanHeuristic` em `searchAgents.py`):

```
python pacman.py -l bigMaze -z .5 -p SearchAgent -a fn=astar,heuristic=manhattanHeuristic
```

e) Insira seu nome na área especificada do arquivo `README.md`, e realize o `commit` e o `push` no github classroom.

Obs: CÓDIGOS ENVIADOS POR EMAIL OU QUALQUER OUTRA FORMA DIFERENTE DO GITHUB NÃO SERÃO AVALIADOS.

### Dicas: 
1) Os algoritmos de busca são muito parecidos. Os algoritmos de busca em profundidade, busca em extensão, busca de custo uniforme e A* diferem somente na ordem em que os nós são retirados da borda. 

2) Dê uma olhada no código dos tipo *Stack* (pilha), *Queue* (fila) e *PriorityQueue* (fila com prioridade) que estão no arquivo `util.py`
