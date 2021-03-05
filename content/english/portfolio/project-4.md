---
title: "Suduko Backtracking"
date: 2019-08-20
image: "images/portfolio/suduko.gif"
categories: ["database"]
description: "This is a Suduko Backtracking algorithm written in python."
draft: false
project_info:
- name: "Andrew"
  icon: "fas fa-user"
  content: "Software Developer"
- name: "Suduko"
  icon: "fas fa-link"
  content: "https://github.com/Andrew1OOO/Games/"
---

# Description

  Sudoku is a logic-based, combinatorial number-placement puzzle. In classic sudoku, the objective is to fill a 9×9 grid with digits so that each column, each row, and each of the nine 3×3 subgrids that compose the grid (also called "boxes", "blocks", or "regions") contain all of the digits from 1 to 9. To have a computer solve a sudoku board, I used the method of backtracking. Backtracking is a general algorithm for finding all solutions to some computational problems, notably constraint satisfaction problems, that incrementally builds candidates to the solutions, and abandons a candidate as soon as it determines that the candidate cannot possibly be completed to a valid solution. 

## Implementation
  These are the main function used in the code. This is pretty simple to follow, the backTrack(board) function finds the next possible empty space, then puts the numbers 1-10 in that position, seeing which numbers work. If you get to a point where the number can't work, then it goes back through, backtracking its steps. 
  ```python
    def backTrack(board):
      find = find_empty(board)
      if not find:
          return True;
      else:
          row, col = find;
      for i in range(1,10):
          if(check_number(board,i,(row,col))):
              board[row][col] = i;
              if(backTrack(board)):
                  return True
              board[row][col] = 0;
      return False;""


    def check_number(board, number, position):
      for i in range(len(board[0])):
          if board[position[0]][i] == number and position[1] != i:
            return False
      for i in range(len(board)):
        if board[i][position[1]] == number and position[0] != i:
          return False
        boxX = position[1] // 3
        boxY = position[0] // 3
      for i in range(boxY*3, boxY*3 + 3):
          for j in range(boxX * 3, boxX*3 + 3):
            if board[i][j] == number and (i,j) != position:
              return False
      return True

  ```
## Conclusion
  This was a pretty simple project, I didn't have a bit of trouble with the check_number method, but once that was sorted, I thought it was pretty smooth.

You can find my code [here](https://github.com/Andrew1OOO/Andrew-Projects/blob/master/TicTacToe.Java)
