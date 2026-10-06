# 2.8 Designing Your First Program

# Batting Average

In baseball, batting average is used to measure a player's batting ability. You use the following formula to calculate a player's batting average:

Batting Average = Hits + Times at Bat

In the formula, Hits is the number of successful hits made by the player, and Times at Bat is the number of times the player was at. For example, if a player is at 500 times during a season, and gets 150 hits, that player's batting average is .300. Design a program to calculate any player's batting average.

Recall from Section 2.2 what a program's actions can typically be divided into three phases:

+   1. Input is received.
2. Some process (such as a calculation) is performed on the input.
3. Output is produced.

Your first step is to determine what is required in each phase. Usually these requirements are not stated directly in the program description. For example, the previously shown batting average problem explains what batting average is, and merely instructs you to design a program to calculate any player's batting average. It is up to you to brainstorm and determine the requirements of each phase. Let's take a closer look at each phase of the batting average problem.

# 1. Input is received.

To determine a program's inputs, you must determine the pieces of data that are required for the program to complete its task. If we look at the batting average formula, we see that two values are needed to perform the calculation:

+   * The number of hits
* The number of times at bat

Because these values are unknown, the program will prompt the user to enter them.

Each piece of input will be stored in a variable. You will have to declare these variables when it is helpful in this phase to think about each variable's name and data type. In the batting average program we will use `hits` for the variable that stores the number of hits, and `atBat` for the variable that holds the number of times at bat. Both of these values will be numbers, so these variables will be declared as `Integers`.

# 2. Some process (such as a calculation) is performed on the input.

Once the program has gathered the required input, it can proceed to use in any necessary calculations, or other operations. The batting average program will divide the number of hits by the number of times at bat. The result of the calculation is the player's batting average.

Keep in mind that when a mathematical calculation is performed, you typically store the result of that calculation in a variable. You should think about the names and data types of variables that are needed in this phase. In this example, we will use the name `battingAverage` for the variable that stores the player's batting average. Because this variable will store the result of a division, we will declare it as a `Real`.