---
title: "Hangman"
date: 2019-02-05
image: "images/portfolio/hangman.gif"
categories: ["Software", "games"]
description: "This is meta description."
draft: false
project_info:
- name: "Andrew Diab"
  icon: "fas fa-user"
  content: "Software Developer"
- name: "Hangman"
  icon: "fas fa-link"
  content: "https://github.com/Andrew1OOO/Games"

---


# Description
  Hangman is a classic game played by many board students and kids. Basically the aim of the game is to guess the word that a person chooses. 
  {{< figure src="https://andrew1ooo.github.io/Andrew-Diab-Website/gifs/Hangman.gif" alt="Hangman.gif" width=500 >}}


## Implementation
  This is the method I made to have the computer guess the word that is chosen to be the hidden word. 
  ```python
  def computer_play(possible_words, right_list, wrong_list):
    temp_possible_words = possible_words.copy()
    for loop in range (len(possible_words)):
        word_matches=1
        for loop2 in range(len(right_list)):
            if right_list[loop2] != "_" and possible_words[loop][loop2] != right_list[loop2]:
                word_matches = 0
        if word_matches == 0 and possible_words[loop] in temp_possible_words:
            temp_possible_words.remove(possible_words[loop])

        for loop2 in range(len(wrong_list)):
            if wrong_list[loop2] in possible_words[loop] and possible_words[loop] in temp_possible_words:
                temp_possible_words.remove(possible_words[loop])

    possible_words = temp_possible_words.copy()

    counters = [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0]
    for loop in range (len(possible_words)):
        for loop2 in range(len(possible_words[loop])-1):
            which_letter = ord(possible_words[loop][loop2]) - 97
            counters[which_letter] = counters[which_letter]+1

    found_guess = 0
    while (found_guess == 0):
        most_used_index = counters.index(max(counters))
        most_used_letter = chr(97+most_used_index)
        if ((most_used_letter not in right_list) and (most_used_letter not in wrong_list)):
            found_guess = 1
        else:
            counters[most_used_index] = 0

    guess = most_used_letter
    return guess

  ```
## Conclusion
  Obviously this is not some revolutionary GUI that is super complicated, neither is the logic behind the game. I just wanted to show some of my first programming projects and how far I have come from. This was probably the first large project I was assigned in my first ever computer science class and this is where I found my passion of programming. 

***



***

# Sourcecode

You can find my Github link for the code [here](https://github.com/Andrew1OOO/Andrew-Projects/blob/master/HangmanAdvanced.py)
***
