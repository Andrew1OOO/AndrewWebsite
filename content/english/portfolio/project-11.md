---
title: "Pathfinding"
date: 2021-07-27
image: "images/images/astar2.gif"
categories: ["design", "OOP","algorithms"]
description: "This is meta description."
draft: false
project_info:
- name: "Andrew"
  icon: "fas fa-user"
  content: "Software Developer"
- name: "Pathfinding Visualization"
  icon: "fas fa-link"
  content: "https://github.com/Andrew1OOO"

-----------

# Description
<!--more-->
This project is a visualization of what the `Dijkstra's` and `A*` pathfinding algorithms do to find the shortests path to a target node from a starting node. Dijkstra's Algorithm is less complex in that it doesn't use `heuristics` to influences its successor nodes, this means it doesn't need to know where the ending node is to be able to find the shortest path, however it is much slower. A* uses heuristics called `f`,`g`,`h`. These heuristics are just values that influence the nodes decisions in choosing a new successor node. The `g` is the distance from the starting point and `h` is the distance from the ending point. `h` can be calculated using many approaches. The way I did it was useing the exact distance, finding it with simple trig.(pythagorean theorem) Once `g` and `h` are calculated, `f` is just the sum of `g` and `h` and the nodes are picked based on the lowest `f` number. 

## Dijkstra's Algorithm
Dijkstra's algorithm is quite simple, Here is how it works:

Start with the `initial` node, and let the distance of node `X` be the distance from the initial node to node `X`. Assign all initial distance to infinity, besides the `initial` nodes distance, which is `0`.

- Create an unvisted list, with all node in the graph added to the list. (Unvisted list)
- Create a current node and set it to the start/intial node
- For the current node, consider all of its unvisited neighbours and calculate their tentative distances through the current node. Compare the newly calculated tentative distance to the current assigned value and assign the smaller one. For example, if the current node A is marked with a distance of 6, and the edge connecting it with a neighbour B has length 2, then the distance to B through A will be 6 + 2 = 8. If B was previously marked with a distance greater than 8 then change it to 8. Otherwise, the current value will be kept.
When we are done considering all of the unvisited neighbours of the current node, mark the current node as visited and remove it from the unvisited set. A visited node will never be checked again.
- If the destination node has been marked visited or if the smallest tentative distance among the nodes in the unvisited set is infinity, then stop. The algorithm has finished.
- Otherwise, select the unvisited node that is marked with the smallest tentative distance, set it as the new "current node", and go back to step 3.



```python

def dijkstra(self,diagonals, screen):
        self.grid[self.startingPos[0]][self.startingPos[1]].distance = 0
        spt = []
        endNode = self.grid[self.endPos[0]][self.endPos[1]]
        unexplored = self.copy(self.grid)
        count = 0
        #print(self.grid[self.startingPos[0]][self.startingPos[1]])
        while(len(unexplored) != 0):
            currentNode = self.minDis(unexplored)
            for event in pygame.event.get():
                if event.type==pygame.QUIT:
                    return [] 
            try:
                unexplored.remove(currentNode)
            except(ValueError):
                print("could not find path")
                return []
            if(currentNode == endNode):
                
                path = []
                current = currentNode
                count = 0
                path.append(current)
                while (current != self.grid[self.startingPos[0]][self.startingPos[1]]):
                    path.append(current.parent)
                    current = current.parent
                    
                return path[::-1]
        
            
            neighbors = [self.grid[currentNode.pos[0]+1][currentNode.pos[1]],self.grid[currentNode.pos[0]-1][currentNode.pos[1]],self.grid[currentNode.pos[0]][currentNode.pos[1]+1],self.grid[currentNode.pos[0]][currentNode.pos[1]-1]]

            suc = []
            for i in range(len(neighbors)):
                if(currentNode != None and neighbors[i] not in spt and neighbors[i].active != 1 ):
                    suc.append(neighbors[i])
            
            for i in range(len(suc)):
                suc[i].parent = currentNode
            
            for neighbor in unexplored and suc:
                
                weight = 1
                if(currentNode.distance + weight < neighbor.distance):
                    neighbor.distance = (currentNode.distance +  weight)
                    spt.append(neighbor)
                pygame.event.pump()
                neighbor.draw(screen)
                self.draw(screen)
                pygame.display.update()
                pygame.display.flip()
            count +=1
```
## A* Star
Explain A star

```python
def astar(self, diagonals, screen):
        open_list = [self.grid[self.startingPos[0]][self.startingPos[1]]]

        closed_list = []
        
        count=0
        endNode = self.grid[self.endPos[0]][self.endPos[1]]
        while(len(open_list) > 0):

            q = open_list[0]
            q_i = 0
            for index, item in enumerate(open_list):
                if item.f < q.f:
                    q = item
                    q_i = index
            

            open_list.pop(q_i)           


            neighbors = [self.grid[q.pos[0]+1][q.pos[1]],self.grid[q.pos[0]-1][q.pos[1]],self.grid[q.pos[0]][q.pos[1]+1],self.grid[q.pos[0]][q.pos[1]-1], self.grid[q.pos[0]+1][q.pos[1]+1],self.grid[q.pos[0]+1][q.pos[1]-1],self.grid[q.pos[0]-1][q.pos[1]-1],self.grid[q.pos[0]-1][q.pos[1]+1]]
            suc = []
            for i in range(len(neighbors)):
                if(q != None and neighbors[i] not in closed_list and neighbors[i] not in open_list and neighbors[i].active != 1):
                    suc.append(neighbors[i])
            
            for i in range(len(suc)):
                suc[i].parent = q
            
            
            
            for i in range(len(suc)):
                for event in pygame.event.get():
                    if event.type==pygame.QUIT:
                        return [] 
                if(q == endNode):
                    path = []
                    current = q
                    count = 0
                    path.append(current)
                    while (current.parent != None):
                        
                        path.append(current.parent)
                        current = current.parent
                        count +=1
                    return path[::-1]
                
                    
                suc[i].g = abs(suc[i].pos[0] - self.startingPos[0])+ abs(suc[i].pos[1] - self.startingPos[0] )
                suc[i].h = ((suc[i].pos[0] - self.endPos[0])**2) + ((suc[i].pos[1] - self.endPos[1])**2)
                suc[i].f = suc[i].g + suc[i].h
                pygame.event.pump()
                suc[i].draw(screen)
                
                
                pygame.time.delay(5)
                pygame.display.update()
                pygame.display.flip()
                if(self.samePos(suc[i], open_list)):
                    continue
            
                if(self.samePos(suc[i], closed_list)):
                    continue
                else:
                    open_list.append(suc[i])



            closed_list.append(q)
```
## Demostration

Dijkstra's: 

![Dijkstra](https://andrew1ooo.github.io/AndrewWebsite/images/portfolio/dijkstra.gif)

A* Star: 

![astar](https://andrew1ooo.github.io/AndrewWebsite/images/images/astar2.gif)
## Future Plans
 - Add more pathfinding algorithms, BFS
 - Add more customization like buttons for changing the size of the graph, erasable walls



You can find my Github link for the code [here](https://github.com/Andrew1OOO/Andrew-Projects)
***
