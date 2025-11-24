#Creating a simple tic-tac-toe game using python
#Creating a board
def create_board():

    return [
        [' ', ' ', ' '],
        [' ', ' ', ' '],
        [' ', ' ', ' ']
    ]

#Printing the board
def print_board(board):
    print("    0   1   2")
    for counter, row in enumerate(board):

        print(f"{counter}  " + " | ".join(row))
        if counter < 2:
            print("   ---|---|---")
    print()

#Checking for a win
def check_win(board, player):
    for r in range(3):
        if all(board[r][c]  ==player for c in range(3)):
            return True

    for c in range(3):
        if all(board[r][c]  ==player for r in range(3)):
            return True

    if all(board[counter][counter]  ==player for counter in range(3)):
        return True

    if all(board[counter][2 - counter]  ==player for counter in range(3)):
        return True

    return False

#Checking for a draw
def check_draw(board):

    for r in range(3):
        for c in range(3):
            if board[r][c]  ==' ':
                return False

    return True

#Getting the player's input
def get_player_input(player, board):

    while True:
        user_input = input(f"Player '{player}', enter move (row col): ")
        parts = user_input.split()

        if len(parts) != 2:
            print("Invalid input. Please enter TWO numbers separated by a space.")
            continue

        row_str, col_str = parts

        if not (row_str.isdigit() and col_str.isdigit()):
            print("Invalid input. Please enter NUMBERS for row and col.")
            continue

        row = int(row_str)
        col = int(col_str)

        if not (0 <= row <= 2 and 0 <= col <= 2):
            print("Coordinates out of range. Must be 0, 1, or 2.")
            continue

        if board[row][col] != ' ':
            print("That cell is already taken! Try again.")
            continue

        return row, col

#Starting the game
def play_game():

    print("--- Welcome to Tic-Tac-Toe! ---")

    board = create_board()
    current_player = 'X'
    game_over = False

    while not game_over:

        print_board(board)

        row, col = get_player_input(current_player, board)

        board[row][col] = current_player

        if check_win(board, current_player):
            print_board(board)
            print(f"Player '{current_player}' wins! Congratulations!")
            game_over = True

        elif check_draw(board):
            print_board(board)
            print("It's a draw!")
            game_over = True

        else:
            current_player = 'O' if current_player  =='X' else 'X'

if __name__  =="__main__":
    play_game()
