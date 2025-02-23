#For the next thing im using bot for simulation. 
For the simulation, First, i defined about the **game board and the game condition**. Heres the code i used
    
[You can see it here!!!](Connect4game_class)

**How This Setup Works**

-Board Initialization:
The Connect4Game class sets up a 6x7 board (by default), initializing all cells to 0 (empty).

-Move Execution and Notation:
make_move(column): Checks if a move in the given column is valid, finds the next open row, places the piece, and logs the move with the move number, player, column, row, and timestamp.
winning_move(piece): Checks the board for any horizontal, vertical, or diagonal win conditions for the specified piece.

-Logging and Analysis:
All moves are recorded in the move_log list. Once the game ends (or after each game), we can call save_game_log() to save the log as a JSON file for later analysis.

Visualization:
print_board() prints the current board state, making it easy to track the game's progression in the console.



