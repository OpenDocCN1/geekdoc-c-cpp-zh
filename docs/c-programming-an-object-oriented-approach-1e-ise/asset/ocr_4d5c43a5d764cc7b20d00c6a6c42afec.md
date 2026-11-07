# **Program 5.18**  Finding the product of a list of numbers (Continued)

```
Run:
Enter a non-negative integer value for n: 0
sum = 0.00
product = 1.00
```

The first run multiplies seven numbers. The second run shows that if the list is empty (size = 0), the result is the initial value for the variables *sum* and *product*. It is good practice to show that the list is empty.

# 5.7.2 Factorial

Another calculation that we encounter in programming is to find the **factorial** of a number.

# Understand the Problem

Factorial is a special kind of multiplication in which the numbers to be multiplied are positive integers (from 1 to the factorial number). In other words, we are looking for the result of (1 × 2 × 3 × ⋯ × n), where n is the size of the list. This is referred to as factorial n! in mathematics. The only information we need from the user is the last number in the series (n).

# Develop the Algorithm

The algorithm to find the factorial is the same as the one we discussed for multiplication in the previous problem. However, since in each iteration we must multiply the counter by the factorial, we must start the counter from 1 (not zero); otherwise the value of the factorial becomes zero in the first iteration and remains zero for the rest of the algorithm. Since we start the counter from 1, we need to come out of the loop when the counter is n + 1 instead of n.

+   1. **Input**
+      a. input *n*
+   2. **Initialize**
+      a. initialize factorial to 1
+      b. initialize counter to 1
+   3. **Repeat as long as the counter is less than n + 1**
+      a. set new factorial to previous factorial times counter
+      b. update counter
+   4. **Output**
+      a. output factorial

# Write the Program

Based on the program components, it is very simple to write the code for this problem. However, we must be concerned about one potential problem: overflow in the result value. Depending on the size of the *unsigned long* type in the system, the result could overflow with a large value for n (Program 5.19).