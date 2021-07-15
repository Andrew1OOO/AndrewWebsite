---
title: "Othello"
date: 2019-03-05
image: "images/portfolio/Reversi.png"
categories: ["design","Software", "games"]
description: "This is meta description."
draft: false
project_info:
- name: "Andrew"
  icon: "fas fa-user"
  content: "Software Developer"
- name: "Othello AI"
  icon: "fas fa-link"
  content: "https://github.com/Andrew1OOO/Games"

---

# What is Othello/Reversi?
<!--more-->
Reversi is a strategy board game for two players, played on an 8×8 uncheckered board. There are sixty-four identical game pieces called disks (often spelled "discs"), which are light on one side and dark on the other. Players take turns placing disks on the board with their assigned color facing up. During a play, any disks of the opponent's color that are in a straight line and bounded by the disk just placed and another disk of the current player's color are turned over to the current player's color.

The object of the game is to have the majority of disks turned to display your color when the last playable empty square is filled.
***


## Implementation

  I this project out by creating all the necessary tools, setting up for the rest of the code. The board is represent as a 2D list, which can be access by [row][column]. I then created a copy of the board for the computer to go through each possibble move and find the best possible move. The set_starting_position is quite self explanitory, and the print board prints the 2D list to the terminal nicely.  
```python
def make_board(board):
  for i in range(8):
      for c in range(8):
          board[i][c] = " "

def copy_board(board,copy):
    for i in range(8):
        for c in range(8):
            copy[i][c] = board[i][c]
    # makes a copy of the board to find the best possible move for the AI

def set_starting_position(board):
    board[3][3] = "X"
    board[4][4] = "X"
    board[3][4] = "O"
    board[4][3] = "O"
    # sets the starting positions

def print_board(board):
    print(" |A|B|C|D|E|F|G|H|")
    print(" |---------------|")
    for i in range(8):
        rowstring = str(i + 1)
        for c in range(8):
            rowstring = rowstring + "|" + board[c][i]
        print(rowstring + "|")
        print(" |---------------|")
```
This next method gets a bit complicated. The ultimate goal of the method is to take the move from the player, check if it is legal, and play it on the board. Most of it is simple, if the players move is not one of the rows or columns then it can't be a move. It is passes that if, then it asks the user for a move, then calls the method check_if_valid_move()
```python
def get_move(board, player):
    row = 0
    column = 0
    inputplay = "Z0"
    # if the users inputs is either not ABCDEFGH 123456789 then it will ask the user for another input
    while inputplay[1] not in ("1", "2", "3", "4", "5", "6", "7", "8") or inputplay[0] not in ("A", "B", "C", "D", "E", "F", "G", "H"):
        if player == "X":
            inputplay = input("Mr.X, What is your play A1-H8? ")
        else:
            inputplay = input("Mr.O, What is your play A1-H8? ")

        if inputplay[1] in ("1", "2", "3", "4", "5", "6", "7", "8") and inputplay[0] in ("A", "B", "C", "D", "E", "F", "G", "H"):
            row = int(inputplay[1]) - 1
            column = ord(inputplay[0]) - 65
            # turn the letters into an ascii value and subtracts by the appropriate amount
            move_good = 0
            move_good = check_if_valid_move(board, column, row, player)
            #makes sure the move the user inputed is valid
            if move_good == 0:
                inputplay = "Z0"
            # if it isn't ask the user for another input
            else:
                board[column][row]= player
                letter_change(board, row, column, player)
            # if it is put it in and change the letters in between
```
This is where some of the methods get quite complicated, so instead of trying to explain it as a broad method, I added comments to the code so that it should be easier to track.
```python
def check_if_valid_move(board, column, row, player):

    movement_direction_steps = [[0,-1],[0,1],[-1,-1],[1,1],[-1,0],[1,0],[-1,1],[1,-1]]
    # this is what happens to the cordinates if you move 1 way in each direction
    if player=="X":
        opponent="O"
    else:
        opponent="X"

    valid_move = 0
    if board[column][row] == (" "):
        for direction in range(8):

            if (valid_move == 0):
                # only lopping if valid move is 0 because we are checking to see if it is a valid move
                square_to_examine_row = row
                square_to_examine_column =column
                this_direction_column_chg=movement_direction_steps[direction][0]
                this_direction_row_chg=movement_direction_steps[direction][1]
                # variables that we want to look at and move towards
                might_be_valid_move=0
                end_walk = 0
                while ((square_to_examine_row >= 0) and (square_to_examine_row <= 7) and
                       (square_to_examine_column >= 0) and (square_to_examine_column <= 7) and # keeping it inside the board
                       (end_walk == 0)):

                    square_to_examine_row = square_to_examine_row + this_direction_row_chg
                    square_to_examine_column = square_to_examine_column + this_direction_column_chg

                    if ((square_to_examine_row >= 0) and (square_to_examine_row <= 7) and
                           (square_to_examine_column >= 0) and (square_to_examine_column <= 7)):

                           if ((might_be_valid_move==1) and (board[square_to_examine_column][square_to_examine_row] == player)):
                               valid_move = 1
                               end_walk = 1
                               # walking out and seeing if the piece after an oppenents piece is your piece becuase if it is than the move is valid
                               # we do this 8 times so that if you walk out and keep seeing an oppenents piece for 7 tiles but on the 8th tiles you find your piece, it will still work
                           if ((might_be_valid_move==1) and (board[square_to_examine_column][square_to_examine_row] == " ")):
                               valid_move = 0
                               end_walk = 1
                               # if it is walking out finds an opponents piece but then finds a space the move is invalid


                           if ((might_be_valid_move==0) and (board[square_to_examine_column][square_to_examine_row] in (" ", player))):
                               end_walk = 1
                               # if it is at the start of walking out and the first thing it hits is a space or a player then the move is invalid

                           if ((might_be_valid_move==0) and (board[square_to_examine_column][square_to_examine_row] == opponent)):
                               might_be_valid_move = 1
                               # if it is at the start of walking out and the first thing it hits is an oppents player then the move might be valid
    return valid_move
```

## Conclusion
  This was the hardest project in my first year of programming and I thought it showed in my programming. It was a bit sloppy and not a great implmenetation of AI. I can definetly improve on this and make something better in the future.  

You can find my Github link for the code [here](https://github.com/Andrew1OOO/Andrew-Projects/blob/master/OthelloAI.py)
***
