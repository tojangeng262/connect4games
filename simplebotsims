#For the next thing im using bot for simulation. 
For the simulation, First, i defined about the game board and the game condition. Heres the code i used


class Connect4Game:
    def __init__(self, rows=6, columns=7):
        """
        Initialize the Connect 4 board and game state.
        - rows: Number of rows (default 6).
        - columns: Number of columns (default 7).
        """
        self.rows = rows
        self.columns = columns
        # Create a rows x columns board initialized with zeros (empty cells)
        self.board = [[0 for _ in range(columns)] for _ in range(rows)]
        # List to store move notation for analysis
        self.move_log = []
        # Player 1 starts (we use 1 and 2 to represent players)
        self.current_player = 1
        # Game state
        self.game_over = False

    def is_valid_move(self, column):
        """Return True if the top cell in the column is empty (i.e., the move is valid)."""
        return self.board[0][column] == 0

    def get_next_open_row(self, column):
        """
        Return the next open row in the specified column.
        We fill from the bottom of the board upward.
        """
        for r in range(self.rows-1, -1, -1):
            if self.board[r][column] == 0:
                return r
        return None

    def drop_piece(self, row, column, piece):
        """Place a piece (1 or 2) in the board at the specified row and column."""
        self.board[row][column] = piece

    def make_move(self, column):
        """
        Attempt to make a move in the specified column.
        Returns True if move is successful; False if the column is full or invalid.
        Records the move in the move_log.
        """
        if column < 0 or column >= self.columns:
            raise ValueError("Column index out of range.")

        if not self.is_valid_move(column):
            print(f"Column {column} is full. Move invalid.")
            return False

        row = self.get_next_open_row(column)
        if row is None:
            print(f"No open row found in column {column}.")
            return False

        # Drop the piece on the board.
        self.drop_piece(row, column, self.current_player)

        # Record move notation
        move_entry = {
            "move_number": len(self.move_log) + 1,
            "player": self.current_player,
            "column": column,
            "row": row,
            "timestamp": datetime.datetime.now().isoformat()
        }
        self.move_log.append(move_entry)

        # Check for a win after the move.
        if self.winning_move(self.current_player):
            self.game_over = True
            

        # Switch player
        self.current_player = 2 if self.current_player == 1 else 1

        return True

    def winning_move(self, piece):
        """Check whether the current board has a winning move for the given piece."""
        # Check horizontal locations for win
        for c in range(self.columns - 3):
            for r in range(self.rows):
                if (self.board[r][c] == piece and self.board[r][c+1] == piece and
                    self.board[r][c+2] == piece and self.board[r][c+3] == piece):
                    return True

        # Check vertical locations for win
        for c in range(self.columns):
            for r in range(self.rows - 3):
                if (self.board[r][c] == piece and self.board[r+1][c] == piece and
                    self.board[r+2][c] == piece and self.board[r+3][c] == piece):
                    return True

        # Check positively sloped diagonals
        for c in range(self.columns - 3):
            for r in range(self.rows - 3):
                if (self.board[r][c] == piece and self.board[r+1][c+1] == piece and
                    self.board[r+2][c+2] == piece and self.board[r+3][c+3] == piece):
                    return True

        # Check negatively sloped diagonals
        for c in range(self.columns - 3):
            for r in range(3, self.rows):
                if (self.board[r][c] == piece and self.board[r-1][c+1] == piece and
                    self.board[r-2][c+2] == piece and self.board[r-3][c+3] == piece):
                    return True

        return False

    def print_board(self):
        """Print the current board state. (Row 0 is the top of the board)"""
        for row in self.board:
            print(row)
        print("\n")

    def save_game_log(self, filename="connect4_game_log.json"):
        """
        Save the recorded move log to a JSON file.
        This file can later be used for analysis.
        """
        with open(filename, "w") as f:
            json.dump(self.move_log, f, indent=4)
        print(f"Game log saved to {filename}")













There are 4 bot that i use in this simulation. this is the list of the bot
1. RandomBot
2. HeuristicBot
3. MinimaxBot
4. MCTSBot
I using some rules for every bot, like for the first simulation, 2 second is the most longer time that it have to think.
