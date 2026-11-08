by an opening curly brace and a closing curly brace. The statements in the loop body display the word “Hello” and then increment `count`, which adds 1 to the counter variable.

# EXERCISE 5-3: USING A COUNTER-CONTROLLED WHILE LOOP

In this exercise, you use what you have learned about counter-controlled loops to answer questions about the following code:

```
```cpp
number1 = 0;
number2 = 0;
while(number1 < 5)
    number1++;
    number2 += number1;
```
```

+   1. What is the value of `number1` when the loop exits? ________________________________
+   
+   2. What is the value of `number2` when the loop exits? ________________________________
+   
+   3. If the statement `number1++` is changed to `++number1`, what is the value of `number1` when the loop exits? ________________________________
+   
+   4. What could you do to force the value of `number2` to be 15 when the loop exits? ________________________________

> **NOTE**
> 
> Incrementing the counter variable is an important statement. Each time through the loop, the counter variable must be incremented or the expression `count < 4` would never be false. This would result in an infinite loop.

# LAB 5-1: USING A COUNTER-CONTROLLED WHILE LOOP

In this lab, you use a counter-controlled while loop in a C++ program provided with the data files for this book. When completed, the program should print the numbers 0 through 10, along with their values doubled and tripled. The data file contains the necessary variable declarations and output statements.

+   1. Open the source code file named `DoubleTriple.cpp` using Notepad or the text editor of your choice.
+   
+   2. Write a counter-controlled `while` loop that uses the loop control variable to take on the values 0 through 10. Remember to initialize the loop control variable before the program enters the loop.
+   
+   3. In the body of the loop, calculate the double and the triple using the value of the loop control variable. Remember to change the value of the loop control variable in the body of the loop.
+   
+   4. Save the source code file in a directory of your choice and then make that directory your working directory.
+   
+   5. Compile the source code file `DoubleTriple.cpp`.
+   
+   6. Execute the program.

> **NOTE**
> 
> Remember that `number2 = number2 + number1;` is the same as `number2 += number1;`.