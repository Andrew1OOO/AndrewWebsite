---
title: "Sorting Visual"
date: 2020-11-20
image: "images/portfolio/sorting.gif"
categories: ["Algorithms", "Visualizations", "Complexity"]
description: "This is meta description."
draft: false
project_info:
- name: "Andrew"
  icon: "fas fa-user"
  content: "Software Developer"
- name: "Sorting Visualizer"
  icon: "fas fa-link"
  content: "https://github.com/Andrew1OOO"

---

## Sorting Algorithms 
  The sorting algorithms that are used in this are Bogo Sort, Bubble Sort, Selection Sort, Insertion Sort, Quick Sort, Merge Sort, Heap Sort. 


## Implementation

  The implementation of the project was pretty simple, we each had a sorting algorithm or 2 and then it would output the complexity and time taken a randomly generated array at a user inputted size in a text based way. For the quicksort, used a recursive method and follow the usually steps for a quicksort algorithm. The main code was made with arraylists so there was no need to return the sorted value as the parameter was passed by reference, meaning the value passed as the parameter would change when the the value in the method was changed. 

  The code below is the code for the QuickSort.
  ```java
    public static void quickSort(ArrayList<Integer> sortMe) {
		  quickSort(sortMe, 0, sortMe.size()-1);
	  }
    
    public static void quickSort(ArrayList<Integer> sortMe, int low, int high) {
        if (low < high+1) {
          int p = partition(sortMe, low, high);
          quickSort(sortMe, low, p-1);
          quickSort(sortMe, p+1, high);
		    }
    }

    public static int partition(ArrayList<Integer> sortMe, int low, int high){
        int split = low + 1;
		for (int i = split; i <= high; i++) {
			if (sortMe.get(i) < sortMe.get(low)) {
				swap(sortMe, i, split++);
			}
		}
		swap(sortMe, low, split-1);
        return split-1;
    }
  ```

## Conclusion
  This project was not a super difficult project, and I actually did not do it by myself. I did the quick sort and helped implement everything together, but my classmates work on some of the other sorts. This was just an exercise to understand the algorithms and see how each one compares to another. (Coded in Java)

***

# Sourcecode

You can find my Github link for the code [here](https://github.com/Andrew1OOO/Andrew-Projects/blob/master/HangmanAdvanced.py)
***
