---
title: "Sorting Visualization"
date: 2021-07-21
image: "images/images/sorting.png"
categories: ["design", "OOP"]
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
This is a visualization of 4 sorting algorithms, commonly used to sort lists. This shows the difference in speed and space between each algorithm, really showing how much faster quicksort/the faster sorting algorithms are compared to other linear ones. I used pygame to make the GUI. 

## Time Complexxity

Each Sorting algorithm has its own complexity, determining the effectiveness of the algorithm. The quickest of the sorting algorithms used in the visualization, quicksort, has an average time complexity of `O(n*log(n))` where is the size of the input list.  

Displayed here:

<!-- display quicksort -->

For the slowest algorithm used in the visualization, bubblesort, the time complexity is `O(n^2)`. This means that bubblesort is signifigantly slower that quicksort on average and does many more comparison of average. 

Displayed here:

<!-- display bubblesort -->


## Implementation

To create this I made a sorting class which had attributes such as the list that needed to be sorted, the speed at which to sort it, the size of each bar, etc. All the sorting algorithms were put into this class and to display them onto the screen I put used a method called 'paint()' each time the sorting method would make comparison. Most of the other code is just he basic pygame implementation with a few addtitions like the custom buttons that change color when pressed. 


```python
def paint(self):
        pygame.event.pump()
        
        
        for i in range(len(self.list)):
            pygame.draw.rect(self.surface, self.color, pygame.Rect(self.x + (self.size+self.space) * i, self.y-self.list[i], self.size, self.list[i]))
            
            #sized = self.Font.render_to(self.surface, ((self.x + 49 * i)+15,self.y + 30), str(self.list[i]), (0,0,0))
            
        pygame.draw.line(self.surface, self.color, (40,500), (760,500), 1)
        comparisond = self.Font.render_to(self.surface, (700,540), str(self.iterations), (255,255,255))

    def bubble_sort(self):
        for i in range(len(self.list) - 1):
            for j in range(len(self.list) - i - 1):
                if self.list[j] > self.list[j + 1]:
                    t = self.list[j]
                    self.list[j] = self.list[j + 1]
                    self.list[j + 1] = t
                self.surface.fill(self.surfColor)
                
                self.paint()
                self.highlight(j+1)

                
                if(len(self.list) > 75):
                    pygame.time.delay(int(1))
                else:
                    pygame.time.delay(int(self.speed))

                pygame.display.update()
                self.iterations += 1
        
```
## All Sorting Algorithms on the same list

<!--show a gif of each algorithm on the same list-->

## Future Plans
 - Add more sorting algorithms, merge sort, heap sort
 - Add more customization like buttons for changing the size of the list instead of using keyboard input



You can find my Github link for the code [here](https://github.com/Andrew1OOO/Andrew-Projects)
***
