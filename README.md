# Chess-game
# This code provides a basic structure for a command-line chess game. 

class ChessGame:
    def __init__(self):
        self.board = self.create_board()
        self.current_player = "white"

    def create_board(self):
        # Initialize an empty chess board
        board = []
        for _ in range(8):
            row = [""] * 8
            board.append(row)
        # Place pieces on the board
        board[0] = ["r", "n", "b", "q", "k", "b", "n", "r"]
        board[1] = ["p"] * 8
        board[6] = ["P"] * 8
        board[7] = ["R", "N", "B", "Q", "K", "B", "N", "R"]
        return board

    def print_board(self):
        # Print the chess board
        for row in self.board:
            print(" ".join(row))

    def make_move(self, move):
        # Parse the move string and update the board
        piece, start, end = move[0], move[1:3], move[3:5]
        start_row, start_col = int(start[1]) - 1, ord(start[0]) - ord("a")
        end_row, end_col = int(end[1]) - 1, ord(end[0]) - ord("a")

        if self.validate_move(start_row, start_col, end_row, end_col):
            self.board[end_row][end_col] = self.board[start_row][start_col]
            self.board[start_row][start_col] = ""
            self.current_player = "black" if self.current_player == "white" else "white"
        else:
            print("Invalid move! Try again.")

    def validate_move(self, start_row, start_col, end_row, end_col):
        # Basic move validation
        piece = self.board[start_row][start_col]
        if piece == "":
            return False

        # Check if it's the correct player's turn
        if piece.islower() and self.current_player != "black":
            return False
        if piece.isupper() and self.current_player != "white":
            return False

        # TODO: Implement more sophisticated move validation logic

        return True

    def play(self):
        while True:
            self.print_board()
            print(f"\nCurrent player: {self.current_player}")
            move = input("Enter your move (e.g., e2e4): ")
            self.make_move(move)

            # TODO: Implement checkmate/stalemate detection

            print("\n----------------------------------\n")

# Create and start the game

game = ChessGame()
game.play()
