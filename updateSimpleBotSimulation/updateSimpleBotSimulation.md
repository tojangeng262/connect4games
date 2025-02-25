Heres, the update of my simulation i will explain using numpy. I dont really sure it will became better that before, since it seems hard for me to prompt the AI to do the change. But here i will share how i prompt and what changes happen

The first thing i do is upload my overall code, and suggest to change it to numpy. I past the prompt to 3 AI chat, which is OpenAI, GoogleAiStudio, and Grok. The only difference is i tell grok to used numpy and doesnt change the output and also doesnt change the effective or the eficient of the bot code. For the other bot i just tell it to used numpy. Overall, i get the better Win Result(based on how low the random bot win rate is) when using the grok, so thats the code i used instead. Heres my overall code change explanation.

**Modify the Connect4Game Class**

We'll change the board to a NumPy array and update all methods to use NumPy operations.


Update of the code is here [Connect4game](Connect4game_class)

Key Changes:

-Changed ```self.board``` to ```np.zeros((rows, columns), dtype=int)```.

-Updated ```is_valid_move``` to use ```self.board[0, column]```.

-Implemented ```get_next_open_row``` using ```np.where``` to find the bottommost zero in the column.

-Updated ```drop_piece``` to use ```self.board[row, column]```.

-Modified ```winning_move``` to use NumPy slicing for horizontal and vertical checks; kept diagonal checks with list comprehension for simplicity.

-```print_board``` and ```save_game_log``` remain largely unchanged since they don't heavily rely on board structure.


**Modify the Bot_class**


After editing the board, the next thing the AI do is editing every bot. Below is the explanation of every bot uses.

1. [RandomBot](RandomBot_class)

The RandomBot doesn't directly interact with the board beyond calling game methods, so no changes are needed:

2. [HeuristicBot](HeuristicBot_class)

Key Changes:

-Updated ```_get_next_open_row``` to use ```np.where``` for NumPy arrays.

-Updated ```_winning_move``` to use NumPy slicing for horizontal and vertical checks.

-Changed board copying in ```choose_move``` to ```game.board.copy()```.

3. [MinimaxBot](MinimaxBot_class)

Key Changes:

-Updated board copying to ```board.copy()```.

-Changed ```get_valid_locations``` to use ```board[0, col]```.

-Updated ```get_next_open_row``` to use ```np.where```.

-Modified ```winning_move``` to use NumPy slicing.

-Updated ```score_position``` to use NumPy operations, including ```(window == piece).sum()``` for counting.

-Ensured all board accesses use ```board[row, col]```.

After running the code, i find 2 bug in this Bot, here's what i changes after the bug

4. [MCTSBot](MCTSBot_class)

Key Changes:

-Updated board copying to ```game.board.copy()```.

-Changed ```get_valid_moves``` to use ```board[0, col]```.

-Updated ```get_next_open_row``` to use ```np.where```.

-Modified ```winning_move``` to use NumPy slicing for horizontal and vertical checks.

-Updated ```simulate_random_game``` to use ```np.all(board[0] != 0)``` for checking if the board is full.


**Update Simulation Function**


The ```run_game```, ```simulate_pairing```, and ```run_simulation``` functions don't directly interact with the board beyond calling game and bot methods, so they remain unchanged. However, we'll update the fallback move logic in ```run_game``` to use NumPy indexing for consistency:

Key Change:

Updated fallback move validation to use ```game.board[0, col]```.

Simulation Function can be seen [here](GameSimulation_function)

