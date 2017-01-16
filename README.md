MinMax game tree search with alpha-beta pruning implemented in FPGA. 
Rules and heuristics implemented for Reversi/Othello game. The system is capable of analyzing ~5M game states/second @50MHz. (no selective search). 
RTL design Verilog 2001 compliant. 
VGA output, pushbuttons input (for playing), using Spartan3E Starter Kit board. 



General Features 

Transition from a current game state to another is done in 1cc.
Determining all possible transitions from a game state to another is also done in 1cc.
Evaluation of one game state is done in 1cc.
The heuristic evaluation function consists of pattern matching between current game state configuration and empirically determined board patterns (about 100 patterns), all comparisons are done concurrently.
Capable of analyzing ~5M game states/second, compared to ~0.2M game states/second obtained with a software version running on P4 processor.
MinMax with alpha/beta pruning, but no selective search.
Maximum frequency is 50MHz.
All RTLs are Verilog. Some RTL's are python generated.
VGA output of the board game.
RS232 transmission: AI-time in clock cycles, number of game positions analyzed.
Number of Slices: 3292 out of 4656 (70%).
Number of BRAMs: 8 out of 20 (40%).
Description         

A Game Tree is a directed graph whose nodes are states of a game. A game state is a configuration of the game on a specific time. The complete game tree of a game consists of all possible game states, from the initial game position to the every possible end-game position, containing all transitions from a game state. Of course, when analyzing a game you cannot look at every game state to choose the best move using reasonable time resources, so this problem is intractable. 

Anyway, AI for such games are based on searching only a partial game tree starting from the current game position and going a few plies deep, than based on a function that will heuristically evaluate the game state, you will pick a good, hopefully the best, move. Generally, increasing the search depth will improve your chance to pick the best move. (In rare cases this is not true). 

The well-known algorithm to search a game tree and choosing the best move, is MinMax. This search method will start from a game state considered initial game state and expand it to generate all possible next-states, and then for every new state will generate the next game states and so on, until a specific depth is reached. When a leaf-node is reached, we can consider that to be an end-game state (because we cannot see deeper), and we will evaluate it. Evaluation of a game state should return a score reflecting the win-lose quantity. Then, going backwards in game tree, we have to maximize or minimize this value. For example, for your point of view, you will have to maximize your wining score and minimize mine. So from a game state you will pick the move which is best for you and worst for me. When it's mine turn, I will maximize my winning score and so on. MinMax will consider playing both roles, alternating. This mathematical model works very well for turn based games like chess, reversi/othello, checkers, etc. 

An improvement for this search is alpha-beta pruning. The difference is that will not search all branches from the partial game tree. This improvement is also implemented in this system. 


also on: https://opencores.org/project,othellogame
