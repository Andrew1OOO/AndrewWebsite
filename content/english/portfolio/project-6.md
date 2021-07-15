---
title: "Math Expression Evaluator"
date: 2020-10-15
image: "images/portfolio/shunting.png"
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
  This project is a mathematical String evalutor. It takes in expression as a string, "(3+3)/10*40+5", and evalutates it to the correct answer, using correct order of operations. This repository features 2 solutions, one implmented by me, and the other implemneted by my partner Rayyan Shaik. [Partner's website (Rayyan Shaik)](https://rayyanshaik.com/). The Solution I came up with is similar to the Shunting Yard algorithm, created by Edsges Dijstrka. This can be found in subdirecty called ```Dijstrka```. The Solution Rayyan came up with is a ```Recursive``` solution, which calls the ```simpleSolve()``` over and over until a solution is found. ```simpleSolve()``` is a main component of both solutions, this method takes in a equation and follows (P)EMDAS to evalute a solution. This method though can not work on large complex expression, it is only for ```simple``` expressions.

### Goals

- Work with a partner efficently and cleanly to get a good finished product
- Create an expression solver without external resources
- Have multiple solutions, as to not limit each persons workflow

## Pseudo-Code
  ```java
while there are tokens to be read:
    read a token.
    if the token is a number, then:
        push it to the output queue.
    else if the token is a function then:
        push it onto the operator stack 
    else if the token is an operator then:
        while ((there is an operator at the top of the operator stack)
              and ((the operator at the top of the operator stack has greater precedence)
                  or (the operator at the top of the operator stack has equal precedence and the token is left associative))
              and (the operator at the top of the operator stack is not a left parenthesis)):
            pop operators from the operator stack onto the output queue.
        push it onto the operator stack.
    else if the token is a left parenthesis (i.e. "("), then:
        push it onto the operator stack.
    else if the token is a right parenthesis (i.e. ")"), then:
        while the operator at the top of the operator stack is not a left parenthesis:
            pop the operator from the operator stack onto the output queue.
        /* If the stack runs out without finding a left parenthesis, then there are mismatched parentheses. */
        if there is a left parenthesis at the top of the operator stack, then:
            pop the operator from the operator stack and discard it
        if there is a function token at the top of the operator stack, then:
            pop the function from the operator stack onto the output queue.
/* After while loop, if operator stack not null, pop everything to output queue */
if there are no more tokens to read then:
    while there are still operator tokens on the stack:
        /* If the operator token on the top of the stack is a parenthesis, then there are mismatched parentheses. */
        pop the operator from the operator stack onto the output queue.
exit.

  ```
## Implementation
  Since the pseudocode was written with the thought of using stacks and queues, and I was not sure how to use them. I basically used arrayLists as a stack and a queue. It is not as efficent, but it is easier to implement. 
  ```java
    public double solve() {
        String equ = this.equation;
        String operators = "^*/+-";
        char operator;
        Double num1;
        Double num2;
        String x;
        ArrayList<Character> equArray = new ArrayList<Character>(10);
        ArrayList<Double> numArray = new ArrayList<Double>(10);
        ArrayList<Character> opArray = new ArrayList<Character>(10);
        for (char c : equ.toCharArray()) {
            equArray.add(c);
        }
        try{
        for(int i = 0; i < equArray.size(); i++){
            if(Character.isDigit(equArray.get(i)) || equArray.get(i) == '.') {
                
                x = String.valueOf(equArray.get(i));

                for(int j = i+1; j < equArray.size(); j++){
                    if(Character.isDigit(equArray.get(j)) || equArray.get(j) == '.'){
                        x += equArray.get(j);
                        
                        equArray.remove(j);
                        j--;
                        }
                    else{
                        break;
                    }
                }
                numArray.add(Double.parseDouble(x));

            }
            else if(equArray.get(i) == '('){
                opArray.add(equArray.get(i));
                
            }
            
            else if(equArray.get(i) == ')'){
                while(opArray.get(opArray.size() -1) != '('){
                    if(numArray.size() >= 2){
                        operator = pop(opArray);
                        num1 = pop(numArray, numArray.size());
                        num2 = pop(numArray, numArray.size());
                        numArray.add(simpleSolve(Double.toString(num2) + operator + Double.toString(num1)));
                    }
                    else{
                        return numArray.get(0);
                    }
                    
                }
                opArray.remove(opArray.size() -1);
            }
            else if(containsChar(operators, equArray.get(i))){
                while(opArray.size() != 0 && checkPrecedence(opArray.get(opArray.size() -1), equArray.get(i))){
                    operator = pop(opArray);
                    num1 = pop(numArray, numArray.size());
                    num2 = pop(numArray, numArray.size());
                    numArray.add(simpleSolve(Double.toString(num2) + operator + Double.toString(num1)));
                }
                opArray.add(equArray.get(i));
            }

        }
        while(opArray.size() != 0){
            operator = pop(opArray);
            num1 = pop(numArray, numArray.size());
            num2 = pop(numArray, numArray.size());
            numArray.add(simpleSolve(Double.toString(num2) + operator + Double.toString(num1)));
        }
        return numArray.get(0);
    }
    catch(NumberFormatException e){
        System.out.println("Equation is invalid!");
        return 0.0;
    }
    }
  ```
## Driver Code
  ```java
  e = new Equation("("+input+")");
  System.out.println("Output: " + e.solve()); 
  ```

## Output

```java
Your expression (+ - / * ^ !): 
    (-2)((((2+2)*3/9-4)*3-1) + (3) + -1^3)/9 + (-10 - (-3))
---------------------
Evaluating: ((-2)((((2+2)*3/9-4)*3-1) + (3) + -1^3)/9 + (-10 - (-3))) >>>
---------------------
Output: -5.444444444444445
Calculation time (ms): 2
Would you like to exit? (y/n) :
    yes
```

## Conclusion
  This project helped me develope my skill of working with a team, as I had to corrdinate and make decisions with my partner. We both thought of 2 different solutions, and we both implemented them. 

  
You can find my code [here](https://github.com/Andrew1OOO/Andrew-Projects/blob/master/TicTacToe.Java)