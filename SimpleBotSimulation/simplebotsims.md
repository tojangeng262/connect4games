#For the next thing im using bot for simulation. 
    For the simulation, First, i defined about the **game board and the game condition**. Heres the code i used
    
[class_connect4game](Connect4game_class)

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

##___________________________________________________________________________________________________________________________________##

After complete the code of game setup, i create a class for bot. this is to make all the bots moves is recorded in the same way as the game logs.

**Standard Bot Interface and Move Format**

-Common Interface
    
Every bot should implement a method (for example, choose_move(game_state)) that takes the current game state as input and returns a move. The move will be represented as the column number (0-indexed) where the bot wants to drop its piece.

-Validation Before Deciding
    
Move Validity: The bot must first ensure that the move it plans to make is valid—that is, the chosen column isn’t already full.
Fallback: If its preferred move is invalid, the bot should have a fallback mechanism (e.g., choose a random valid move).

-Move Logging Format

Once the bot has decided on a column, the game environment will place the piece and record the move. Each move should be logged in a standard format (as we set up earlier), which might include:
        move_number: The sequential move count.
        player: The ID of the player (or bot) making the move (e.g., 1 or 2).
        column: The chosen column for the move.
        row: The row where the piece landed.
        timestamp: The exact time when the move was made.

-Decision-Making Strategy
    
Although different bots may have different strategies (random, heuristic, minimax, etc.), they should all:

1.Return a valid column: Ensure that the returned move will result in a legal move.

2.Follow game rules: Not attempt to place a piece in a column that's already full or out of bounds.

-Error Handling and Edge Cases

Graceful Handling: In case the bot's logic somehow selects an invalid move, it should catch that error and select another valid move.
Time Constraints (if applicable): If you plan on having a time limit per move, all bots should adhere to the same time constraints.

For the code, you can see it here: [class_bot](bot_class)

##_________________________________________________________________________________________________________________________________##

For the simulation, i created 4 bot
Heres all the bot that i used



**1. Random Bot:**

the code i use is here : [RandomBot](RandomBot_class)

What it does: Chooses moves completely at random among the valid options.
Why: Serves as a baseline and tests if more advanced strategies can consistently beat a “dumb” opponent.

the explanation of the code:

-Building a list of valid columns using the is_valid_move() method from the game.
-Randomly selecting one of those columns.




**2.Heuristic (Rule-Based) Bot:**

the code i use is here [HeuristicBot](HeuristicBot_class)

What it does: Checks for immediate wins or blocks an opponent’s winning move, and then makes a move based on simple board evaluations (e.g., center column preference).
Why: Mimics a novice human player with some tactical awareness.

Explanation of the code


-Immediate Win Check: For every valid column, the bot simulates placing its piece. If that move wins the game, it is chosen.

-Block Opponent: Next, the bot simulates the opponent's move for every valid column. If the opponent would win with that move, the bot selects that column to block them.

-Center Preference: If no immediate wins or blocks exist, the bot prefers the center column if available.

-Heuristic Preference: Finally, if the center is not available, the bot selects the column closest to the center.




**3.Minimax Bot (with Alpha-Beta Pruning):**

the code i use is here: [MinimaxBot](MinimaxBot_class)

What it does: Uses the minimax algorithm to look several moves ahead, with alpha-beta pruning to optimize the search.
Variations:
Depth Variants: Create two versions—one with a shallower search (novice level) and one with a deeper search (expert level).
Why: Demonstrates a more calculated, strategic approach.

How It Works

-Iterative Deepening with Time Check:
The choose_move method starts with a depth of 1 and increases the depth as long as there’s time (2 seconds limit). If the time is exceeded (via a TimeoutError raised in the minimax recursion), it returns the best move found in the previous iteration.

-Minimax with Alpha‑Beta Pruning:
The minimax method recursively evaluates moves. It uses a simple evaluation function (score_position) and checks terminal conditions (win/draw). The search is pruned using the alpha and beta values.

-Heuristic Evaluation:
The board is scored by giving extra weight to center control and by evaluating all possible windows of four cells on the board.





**4.Monte Carlo Tree Search (MCTS) Bot:**

the code i use is here:[MCTSBot](MCTSbot_class)

What it does: Runs many random simulations from the current board state to statistically evaluate moves.
Why: Offers a different flavor of decision-making that can mimic human intuition and sometimes find creative strategies.

Explanation
-Time Constraint:
The choose_move method uses a loop that runs until 2 seconds have passed. In each iteration, it goes through each valid move, simulates one random playout from that move, and updates the win count and simulation count.

-Simulation Function:
The simulate_random_game function plays random moves until a terminal state is reached. It returns:

1 if the simulation results in a win for the bot,
0.5 if the game is a draw,
0 if it results in a loss.


-Helper Methods:

get_valid_moves: Returns all columns where a move is possible.
get_next_open_row: Finds the next available row in a given column.
winning_move: Checks for win conditions on the board, similar to our game’s win-check logic.


##________________________________________________________________________________________________________________________________##

The last thing i used is make the class for the simulation. [Running_simulation](run_game_class) is the code that i used.


**How This Simulation Script Works**

-run_game Function:

Initializes a new Connect4Game for each game.
Instantiates two bots with the appropriate player_id based on the ordering parameter.
Runs the game loop until the game ends (either by a win or when the board is full).
Determines the winner from the last move and packages the game’s move log along with metadata (including bot IDs, game number, and ordering) into a dictionary.

-run_simulation Function:

Sets up a directory (simulation_game_logs) where each game’s log is saved as a JSON file.
Iterates over each distinct pairing of the four bots. For each pairing, it runs 1000 games (500 with one ordering, 500 with the reversed ordering) so that each bot plays as Player 1 in 50% of the games.
Each game’s log is saved with a filename that includes the bot names, the ordering, and the game number.

-Execution:

Running this script will start the simulation and, once complete, print the total number of games played (which should be 6000 if there are 6 distinct pairings).

**Note**: i run this script like 30 hours, and its maybe was caused by two thing. first is the code that i use is still inefficient. the second one maybe is the time limit of 2 second, with resulted in the long time of each game when the MinimaxBot and MCSTBot play agains each other. i still dont test how effective the bot is, against another bot that already available since the main objective of my code is to get a game notation to analyze later.


