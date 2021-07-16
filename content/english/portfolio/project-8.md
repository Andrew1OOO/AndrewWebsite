---
title: "Chess"
date: 2021-06-10
image: "images/portfolio/chess.gif"
categories: ["design", "games"]
description: "This is meta description."
draft: false
project_info:
- name: "Andrew"
  icon: "fas fa-user"
  content: "Software Developer"
- name: "Chess"
  icon: "fas fa-link"
  content: "https://github.com/Andrew1OOO/Games"

---

# Description
<!--more-->
For this project I recreated the well known board game chess in python. I made 2 implementation of it, one which prints the output to the terminal and the other which has a GUI. Chess



***


## Implementation

  For the first implemenation, called 'chess.py', I used simple print to screen methods which would be seen in the terminal. However the pieces would still look like pieces as I used the chess unicode characters, ♔. I also used the bcolors ASCII escape codes, which allow for a string to change colors when printed. Here is some of the code that utilises these features:

```python
def print_b(board):
    list1 = [3,4,5,6]
    print(f"{bcolors.BOLD}  A|B|C|D|E|F|G|H{bcolors.ENDC}")
    for i in range(len(board)):
        print(bcolors.BOLD + str(i+1) + "|", bcolors.ENDC, *board[i], sep='')

def repaint(board):
    for i in range(len(board)):
        for j in range(len(board[0])):
            
            if('\033[95m' in board[i][j]):
                board[i][j] = board[i][j].replace('\033[95m',"").replace('\033[0m',"")
```

    And here is what it looks like printed to the screen:

![Chess Implementation 1](https://andrew1ooo.github.io/AndrewWebsite/images/images/chess1.png)


    The main bulk of the code is the same for both of them, like telling if they are in check, or which turn it is, or the driver code. For the GUI version I just went through the 2d array and "blited" as pygame calls it, or more elegently, rendered an piece to the screen for the specific piece in the array.

    Some of that code looks like this:

```python
for i in range(len(board)):
        for j in range(len(board[0])):
            if(board[i][j] == "♙"):
                screen.blit(wpawn, decrypt(j,i))
            if(board[i][j] == "♟︎"):
                screen.blit(bpawn, decrypt(j,i))
            if(board[i][j] == "♔"):
                screen.blit(wking, decrypt(j,i))
            if(board[i][j] == "♚"):
                screen.blit(bking, decrypt(j,i))
            if(board[i][j] == "♕"):
```

    The GUI looks like this:

![Chess Implementation 2](https://andrew1ooo.github.io/AndrewWebsite/images/images/chess2.png)

## Goals with this Project
 - get better at GUI building 
 - better understanding of 2d array manipulation

## Future Plans
 - At some point in the future I would also like to implement a minimax algorithm to play against the user.
 - I would also like to go back and update the GUI to look a bit better this implementation feels a bit rushed
 - Maybe give the user a darkmode option or a themes option

## Conclusion
2 years ago I tried to make a chess game with a friend and I was never able to do it. Now I am able to make it by myself in just under 5 days. That shows the progression of my programming skills from 9th-11th grade. This project is also not the best I have done this year. 

You can find my Github link for the code [here](https://github.com/Andrew1OOO/Andrew-Projects)
***
