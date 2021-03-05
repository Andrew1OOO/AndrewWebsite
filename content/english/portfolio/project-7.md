---
title: "Binteger"
date: 2020-11-10
image: "images/portfolio/binteger.png"
categories: ["OOP","Software", "Algorithms"]
description: "This is meta description."
draft: false
project_info:
- name: "Andrew Diab"
  icon: "fas fa-user"
  content: "Software Developer"
- name: "Mathmatical Expression Evaluator"
  icon: "fas fa-link"
  content: "https://github.com/Andrew1OOO/Calculator"

---

# Description
This proejct is a copy of the actual java library, Big Integer. This library is able to handle numbers greater than what is supported by Java's int and double types. Although without operations the number is quite useless, so the Class must also be able to do basic operations, such as +, -, *, /, %. This was the tough bit. 

## Implementation
The implementation for each operation would be different. We decided to represent the large number as an long array. This was probably not the greatest strategy to start with as it provided a few memory issues down the line, instead we should have used bytes to decrease the amount of memory used. 

```java
    public Binteger(String n) {
        asString = n;
        isNegative = n.charAt(0) == '-';
        
        char[] split = n.toCharArray();

        if (isNegative) {
            val = new int[split.length-1];
            for (int i=1; i<split.length; i++) {
                val[i-1] = Character.getNumericValue(split[i]);
            }
        }
        else {
            val = new int[n.length()];
            for (int i=0; i<split.length; i++) {
                val[i] = Character.getNumericValue(split[i]);
            }
        }
    }

    public Binteger(int[] a, boolean negative) {
        val = reduce(a);
        isNegative = negative;
        asString = null;

    }

```
The hardest operation to think about was division. Our solution for division involved converting each number into a smaller decimal double, so a large number such as 456789 would be represented as 4.56789. This worked, although their is a bit of precision loss as the numbers are not staying completely consistent throughout. 
```java
division
```
## Conclusion
This project was really hard as it made us(Rayyan and I were partners) think about the lower level of operations between numbers. It also forced us to think about the efficiency as the numbers were too long to take an inefficient approach.  

You can find my code [here](https://github.com/)