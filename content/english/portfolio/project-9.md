---
title: "2048 AI"
date: 2021-07-10
image: "images/portfolio/2048.gif"
categories: ["design", "games", "OOP"]
description: "This is meta description."
draft: false
project_info:
- name: "Andrew"
  icon: "fas fa-user"
  content: "Software Developer"
- name: "Chess"
  icon: "fas fa-link"
  content: "https://github.com/Andrew1OOO"

-----------

# Description
<!--more-->
2048 is a tile/board game in which the user moves tiles back, forth, and vertically around a `4x4` grid to create the number `2048`. The numbers going up by `2^n`, where n is the amount of merges. So to get 8 you have to merge 3 times, `2-2=4`,`4-4=8`. With this project I decided to recreate the game, as well as create an `AI` for it. The AI uses Monte Carlo Simulation to quickly get to `2048`.

## Monte Carlo Simulations

Monte Carlo Simulations are used to find the best move in `2048`. The Monte Carlo method is the idea of using a large number of random simulations of an experiment to gain insights into the experiment's end results. In other words, Monte Carlo simulations are a way to estimate what will happen in a given experiment without having to implement any specific algorithms. To implement this into `2048`, I would cycle each move [left, right, up, down] for the amount of simulations given, so if `200` simulations were given, each move [left, right, up, down] would be simulated `50` times. After each move, I would then have the simulation move randomly until the game was over. So it would simulate `200` games before making a move, and score each first move and then at the end return the best first move, which would be the move in the actual game. 

Here is the code:

```python        
    for inter, m in enumerate(possible_moves):
        for i in range(int(amount)):
            simulation = Board(mode)
            simulation.board = copy.deepcopy(board)
                    
            simulation.move(m)
            simulation.add_block(Block(2 * random.randint(1,2), pg.Rect(0,0, 60, 60), mode))

            while((simulation.game_over() == False)):
                simulation.move(possible_moves[random.randint(0,3)])
                simulation.add_block(Block(2 * random.randint(1,2), pg.Rect(0,0, 60, 60), mode))


            simScore[inter] += simulation.score
    topScore = max(simScore)

    index = simScore.index(topScore)
    bestMove = possible_moves[index]

    return bestMove
    
```




## Game Implementation 

For the game I used pygame and Tkinter. Pygame was for the actual game and Tkinter was for the UI to choose weather to simulate or play the game. I created a Block class which was the super class of Board. To make it simplier I shifted a list in python and then updated the GUI based on the board. Here is the code for shifting left:


```python
    def shift_left(self):
        for i in range(len(self.board)):
            v=[]
            w=[]
            for j in range(len(self.board[0])):
                if(self.board[i][j] != 0):
                    v.append(self.board[i][j])

            j=0
            while(j < len(v)):
                if(j < len(v) - 1 and v[j].size == v[j+1].size):
                    v[j].set_size(v[j].size*2)
                    w.append(v[j])
                    self.score += v[j].size
                    j+=1
                else:
                    w.append(v[j])
                j += 1
                
            for j in range(len(self.board)):
                self.board[i][j] = 0
            j=0
            for it in w:
                self.board[i][j] = it

                j+=1
        
```

    And here is what it looks like:

![2048](https://andrew1ooo.github.io/AndrewWebsite/images/images/20481.png)


    I also created a dark mode for the GUI:

![2048](https://andrew1ooo.github.io/AndrewWebsite/images/images/20482.png)


## Final Product 

![2048](https://andrew1ooo.github.io/AndrewWebsite/images/portfolio/2048.gif) 

## Future Plans
 - Add other themes



You can find my Github link for the code [here](https://github.com/Andrew1OOO/Andrew-Projects)
***
