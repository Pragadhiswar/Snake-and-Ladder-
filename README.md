import random

# Define the board with snakes and ladders
# The keys are the starting positions, and the values are the ending positions
snakes = {16: 6, 47: 26, 49: 11, 56: 53, 62: 19, 64: 60, 87: 24, 93: 73, 95: 75, 98: 78}
ladders = {1: 38, 4: 14, 9: 31, 21: 42, 28: 84, 36: 44, 51: 67, 71: 91, 80: 100}

# Combine snakes and ladders into one dictionary
board = {**snakes, **ladders}

def roll_dice():
    return random.randint(1, 6)

def move_player(position, roll):
    position += roll
    if position > 100:
        position = 100 - (position - 100)  # Bounce back if overshooting
    return board.get(position, position)  # Move to the end of snake/ladder if applicable

def play_game():
    player1_position = 0
    player2_position = 0
    turn = 0  # 0 for player 1, 1 for player 2

    while player1_position < 100 and player2_position < 100:
        if turn == 0:
            input("Player 1's turn. Press Enter to roll the dice.")
            roll = roll_dice()
            print(f"Player 1 rolled a {roll}.")
            player1_position = move_player(player1_position, roll)
            print(f"Player 1 is now on square {player1_position}.")
            if player1_position == 100:
                print("Player 1 wins!")
                break
            turn = 1  # Switch to player 2
        else:
            input("Player 2's turn. Press Enter to roll the dice.")
            roll = roll_dice()
            print(f"Player 2 rolled a {roll}.")
            player2_position = move_player(player2_position, roll)
            print(f"Player 2 is now on square {player2_position}.")
            if player2_position == 100:
                print("Player 2 wins!")
                break
            turn = 0  # Switch to player 1

if __name__ == "__main__":
    play_game()
