# TicTacToe
Python basic project
## Setup (print) the board
Print the board based on board list.
```Python
from IPython.display import clear_output

def display_board(board):
    clear_output()  # Clears the screen for a cleaner display
    print(f" {board[7]} | {board[8]} | {board[9]} ")
    print("---|---|---")
    print(f" {board[4]} | {board[5]} | {board[6]} ")
    print("---|---|---")
    print(f" {board[1]} | {board[2]} | {board[3]} ")

initial_board = [' ',' ',' ',' ',' ',' ',' ',' ',' ',' ']
display_board(initial_board)
```
## Welcome message
Check if the player want to start the game.
```Python
def welcome():
    ready ='wrong'
    while ready not in ['Y','N']:
        ready = input('Are you ready to play the game? Y or N')
        if ready not in ['Y','N']:
            print ('Invalid, type Y or N')
        if ready == 'Y':
            return True
        if ready == 'N':
            return False
```
## Intake position
```Python
def player_input():
    position='wrong'
    while position not in range (1,10):
        position = int(input('pick a new position from number 1-9'))
        if position not in range (1,10):
            print ('sorry invalid position')
    print(f"Position selected: {position}")        
    return position
```
## Display position and marker in board
This function takes in the board list object, a marker ('X' or 'O'), and a desired position (number 1-9) and assigns it to the board.
```Python
def place_marker(board, marker, position):
    # board_initial = ['#',' ',' ',' ',' ',' ',' ',' ',' ',' ']
    board[position] = marker
    pass
```
## Check if anyone wins
This function takes in a board and a mark (X or O) and then checks to see if that mark has won.
```Python
def win_check(board, marker):
        # Define winning combinations
    winning_combinations = [
        [1, 2, 3], [4, 5, 6], [7, 8, 9],  # Horizontal wins
        [1, 4, 7], [2, 5, 8], [3, 6, 9],  # Vertical wins
        [1, 5, 9], [3, 5, 7]              # Diagonal wins
    ]

    # Find the indices where the board matches the marker
    indices = [i for i, value in enumerate(board) if value == marker]

    # Check if any winning combination is a subset of the player's indices
    for combination in winning_combinations:
        if all(pos in indices for pos in combination):
            return True

    return False
```
## Randomly decide the first player
I use this function to decide the first player sitting on left or right should play first.
```Python
import random

def choose_first():
    player=['#', 'left', 'right']
    first=player[random.randint(1,2)]
    print(f'Player who sit on {first} should go first and put X')
```
## Check if the position is available
This function returns a boolean indicating whether a space on the board is freely available.
```Python
def space_check(board, position):
    if board[position] == ' ':
        return True
    else:
        return False
    pass
```
## Check if the board still have space
I didn't use this function in the main code; I used a while statement to make sure the rounds is under 9.
```Python
def full_board_check(board):
    if ' ' in board:
        return True
    else:
        return False
```
## Replay Check
Ask the player if they want to play again and returns a boolean True if they do want to play again.
```Python
def replay():
    replay = 'wrong'
    while replay not in ['Y','N']:
        replay=input('Do you want to play again? Y or N')
        if replay not in['Y','N']:
            print ('Invalid choice, type Y or N')
    if replay =="Y":
        return True
    else:
        return False
```
## Put it together
```Python
from IPython.display import clear_output
#Welcome Setting
print('The system will pick a random player to go first. \nNo.1 player use X as marker and No.2 player use O')

while welcome() == True:
    # initial setting 
    print("Starting game setup")
    display_board(initial_board)
    position = 'wrong'
    position_picked=[]
    marker = "X"
    marker_list = ['#',"X","O","X","O","X","O","X","O","X"]
    rounds = 0
    board = [' ',' ',' ',' ',' ',' ',' ',' ',' ',' ']
    
    # Game started 
    while rounds<9:
        position = player_input()
        position_picked.append(position) 
        rounds = rounds +1
        marker = marker_list[rounds]
        print(f"Rounds: {rounds}, Marker: {marker}, Positions Picked: {position_picked}")
        
        
        #display new board
        board[int(position)] = marker
        display_board(board)
        
        
        #win check 
        if win_check(board,marker) == True:
            print('congratulations! You won!')
            break
        else:
            pass
    
    #replay check
    if replay()== False:
        print('See you next time!')
        break
    else:
        clear_output()
```










