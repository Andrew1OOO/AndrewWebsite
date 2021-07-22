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
  content: "https://github.com/Andrew1OOO"

---

# Description
This proejct is a copy of the actual java library, Big Integer. This library is able to handle numbers greater than what is supported by Java's int and double types. Although without operations the number is quite useless, so the Class must also be able to do basic operations, such as `+`, `-`, `*`, `/`, `%`. This was the tough bit. 

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
private String rawDivide(long[] a, long[] b) {
        double aDouble = Math.abs(toDouble(a))*-1;
        double bDouble = Math.abs(toDouble(b))*-1;
        double sum = 0;
        if(bDouble < aDouble){ // if the first number is less than the seconds the output will always be 0
            sum =  0.0;
        }
        else if(bDouble > aDouble && b.length == a.length){ // this is for a case, if the first number is greater than the second and the lengths are the same meaning the output will be very small
            sum = Math.floor(aDouble/bDouble);
        }
        else if(bDouble > aDouble && b.length != a.length){ // this is for a case, if the first number is greater than the second, but lengths are not the same meaning the output will be larger than 10
            int periodIndex = 0; // point in the string where the '.' is 
            int[] x = new int[a.length]; // array of all the numbers in the string
            int difference = Math.abs(b.length - a.length); // the difference in size between the 2 numbers, the difference for 345 and 3 would be 2
            sum = aDouble/bDouble;
            int k = 0;
            String y = Double.toString(sum);
            for(int i = 0; i < y.length() ; i++){ // adding the values of the string into the array
                if(y.charAt(i) != '.'){ // if it is not a '.' add the numbers
                    x[i] = Integer.parseInt(String.valueOf(y.charAt(i)));
                }
                else{ // if it is a '.' add a number that we can diffentiate from the other numbers, such as any number >= 10
                    periodIndex = i;
                    x[i] = 10;
                }
            }
            for(int i = periodIndex; i < y.length(); i++){ // moveing the period over by the amount of difference
                if(i - periodIndex == difference){ 
                    break;
                }
                if(x[i] == 10){ // if the number is 10, if it is the period, move the period over to the right one
                    k = x[i];
                    x[i] = x[i+1];
                    x[i+1] = k;
                }
            }
            String quotient = "";
            for(int i = 0; i < y.length(); i++){ //adding the array back into a string
                if(x[i] < 10){
                    quotient += Integer.toString(x[i]);
                }
                else if(x[i] == 10){ // change the differentiating value back to a '.'
                    quotient += ".";
                }
            }
        return quotient;
        }
        else{ // if the numbers are the same the return will always be 1
            sum =  1.0;
        }
        return Double.toString(sum); // return the string of the sum we had figured out
    }
```
## Conclusion
This project was really hard as it made us(Rayyan and I) think about the lower level of operations between numbers. It also forced us to think about the efficiency as the numbers were too long to take an inefficient approach.  

You can find my code [here](https://github.com/)