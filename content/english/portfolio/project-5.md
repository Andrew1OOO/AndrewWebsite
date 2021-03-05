---
title: "TicTacToe Solver"
date: 2019-03-09
image: "images/portfolio/tictactoe.gif"
categories: ["games","Software"]
description: "This is meta description."
draft: false
project_info:
- name: "Andrew Diab"
  icon: "fas fa-user"
  content: "John Doe"
- name: "TicTacToe"
  icon: "fas fa-link"
  content: "https://github.com/Andrew1OOO/Games/"

---

# Description
  TicTacToe is a paper-and-pencil game for two players, X and O, who take turns marking the spaces in a 3×3 grid. The player who succeeds in placing three of their marks in a diagonal, horizontal, or vertical row is the winner. It is a solved game with a forced draw assuming best play from both players. This project was written in java.

## Implementation
  I wrote this TicTacToe game in Java using the JFrame class. The GUI is pretty basic and their really isn't any advanced learning that the computer is doing. I didn't really understand anything about constructors or OOP when writing this, that is why most of the code is in the constructer. Definetly not my best work. 
  ```java
    public void mouseClicked(MouseEvent e) {

            int chosen_square = 0;

            if (game_over == 0) {

            mousex = e.getX();
            mousey = e.getY();
            if (mousey >= 250) {
                chosen_square +=6;
            }
            else if (mousey >= 150) {
                chosen_square +=3;
            }

            if (mousex >= 250) {
                chosen_square +=2;
            }
            else if (mousex >= 150) {
                chosen_square +=1;
            }
            squares[chosen_square] = current_player;

        }
         if (((squares[0] == current_player) && (squares[1] == current_player) && (squares[2] == current_player)) ||
            ((squares[3] == current_player) && (squares[4] == current_player) && (squares[5] == current_player)) ||
            ((squares[6] == current_player) && (squares[7] == current_player) && (squares[8] == current_player)) ||
            ((squares[0] == current_player) && (squares[3] == current_player) && (squares[6] == current_player)) ||
            ((squares[1] == current_player) && (squares[4] == current_player) && (squares[7] == current_player)) ||
            ((squares[2] == current_player) && (squares[5] == current_player) && (squares[8] == current_player)) ||
            ((squares[0] == current_player) && (squares[4] == current_player) && (squares[8] == current_player)) ||
            ((squares[2] == current_player) && (squares[4] == current_player) && (squares[6] == current_player))){
            game_over = 1;
            setBackground(Color.YELLOW);
            setForeground(Color.RED);

            }
  ```

  ## Conclusion
    This project was my first ever attempt at using java. Due to this, the code was very sloppy and in wierd places. I was used to writing in python, where their are no classes or object. Definetly not the best I could have done. 


  
You can find my code [here](https://github.com/Andrew1OOO/Andrew-Projects/blob/master/TicTacToe.Java)
