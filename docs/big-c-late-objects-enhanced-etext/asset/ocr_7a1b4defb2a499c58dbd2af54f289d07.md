# 1.7.4 From Algorithms to Programs

In Section 1.7.2, we developed pseudocode for finding how long it takes to double an investment. Let’s double-check that the pseudocode represents an algorithm; that is, that it is unambiguous, executable, and terminating.

Our pseudocode is unambiguous. It simply tells how to update values in each step. The pseudocode is executable because we use a fixed interest rate. Had we said to use the actual interest rate that will be charged in years to come, and not a fixed rate of 5 percent per year, the instructions would not have been executable. There is no way for anyone to know what the interest rate will be in the future. It requires a bit of thought to see that the steps are terminating: With every step, the balance goes up by at least $500, so eventually it must reach $20,000.

Therefore, we have found an algorithm to solve our investment problem, and we know we can find the solution by programming a computer. The existence of an algorithm is an essential prerequisite for programming a task. You need to first discover and describe an algorithm for the task before you start programming (see Figure 9). In the chapters that follow, you will learn how to express algorithms in the C++ language.

![](bbox=[0.75, 0.18, 0.9, 0.58])

Figure 9 The Software Development Process

![](bbox=[0.1, 0.7, 0.22, 0.85])

# HOW TO 1.1 Describing an Algorithm with Pseudocode

This is the first of many “How To” sections in this book that give you step-by-step procedures for carrying out important tasks in developing computer programs.

Before you are ready to write a program in C++, you need to develop an algorithm—a method for arriving at a solution for a particular problem. Describe the algorithm in pseudocode—a sequence of precise steps formulated in English. To illustrate, we’ll devise an algorithm for this problem:

# Problem Statement

You have the choice of buying one of two cars. One is more fuel efficient than the other, but also more expensive. You know the price and fuel efficiency (in miles per gallon, mpg) of both cars. You plan to keep the car for ten years. Assume a price of $4 per gallon of gas and usage of 15,000 miles per year. You will pay cash for the car and not worry about financing costs. Which car is the better deal?

![](bbox=[0.78, 0.88, 0.92, 0.98])

© dlewis33/Getty Images.

# Step 1 Determine the inputs and outputs.

In our sample problem, we have these inputs:

+   - *purchase price1* and *fuel efficiency1*, the price and fuel efficiency (in mpg) of the first car
+   - *purchase price2* and *fuel efficiency2*, the price and fuel efficiency of the second car