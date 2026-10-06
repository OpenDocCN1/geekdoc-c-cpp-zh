# Development of a Framework for the Desktop Grid Federation ■ 239

TABLE 10.1 Complexities of Computer Board Games
| Game | Board Size | State-Space Complexity | Game Tree Complexity | Branching Factor |
| Tic-tac-toe | 9 | 3 | 5 | 4 |
| Chinese Checkers | 121 | 23 | | |
| Chess | 64 | 47 | 123 | 35 |
| Connect6 | 361 | 172 | 140 | 46,000 |
| Shogi | 81 | 71 | 226 | 92 |
| Go (19x19) | 361 | 171 | 360 | 250 |

a state, the game tree search algorithm is used to evaluate all possible moves and select a move based on certain policy. The challenge of computer board game comes from the fact that the state space of game trees is usually exponential to the input size, as shown in Table 10.1. Thus, an efficient tree search algorithm prunes useless paths and go deep to the best moves. A typical strategy for evaluating the best moves is to run a Monte Carlo tree (MCTS) simulation of the game playing processes [15,18,19].

Among the board games, Connect6 attracted much attention due to three merits: fairness, simplicity of rules, and game complexity. First, Connect6 is fair in the sense of balancing. For example, each player has one stone more than the other, after finishing a move and before the opponent makes the next move. Second, Connect6 is simple in the sense that no extra rules are imposed. In contrast, prohibition rules of double threes and doubles for Black are imposed in Renju, a professional version of five-in-a-row games [2], for the sake of balancing. Third, Connect6 is complex in the sense of game tree complexity, since the combination of choosing two intersections to place stones is normally much higher than of choosing one.

# 10.2.2 Application Components

The game tree search application contains two major modules: a game record editor and a job-level (or JL) module. The game record editor is the interface of the computer board games displays status and waits for the player commands. The JL module is the component that executes jobs such as searching the best game moves or detecting the end-of-game.

Using the game record editor, players can browse, interpret, and process the game records that are stored in the standard Smart Game Format