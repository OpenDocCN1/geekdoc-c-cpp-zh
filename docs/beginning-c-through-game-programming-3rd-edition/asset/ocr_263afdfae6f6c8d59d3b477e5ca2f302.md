# # Trap

A reference always refers to the variable with which it was initialized. You can't reassign a reference to refer to another variable so, for example, the results of the following code might not be obvious.

```
```cpp
int myScore = 1000;
int& mikesScore = myScore;
int larrysScore = 2500;
mikesScore = larrysScore; //may not do what you think!
```
```

The line mikesScore = larrysScore; does not reassign the reference mikesScore so it refers to larrysScore because a reference can't be reassigned. However, because mikesScore is just another name for myScore, the code mikesScore = larrysScore; is equivalent to myScore = larrysScore;, which assigns 2500 to myScore. And after all is said and done, myScore becomes 2500 and mikesScore still refers to myScore.

# # Passing References to Alter Arguments

Now that you've seen how references work, you might be wondering why you'd ever use them. Well, references come in quite handy when you are passing variables to functions because when you pass a variable to a function, the function gets a copy of the variable. This means that the original variable you passed (called the argument variable) can't be changed. Sometimes this might be exactly what you want because it keeps the argument variable safe and unalterable. But other times you might want to change an argument variable from inside the function to which it was passed. You can accomplish this by using references.

# # Introducing the Swap Program

The Swap program defines two variables—one that holds my pitifully low score and another that holds your impressively high score. After displaying the scores, the program calls a function meant to swap the scores. But because only copies of the score values are sent to the function, the argument variables that hold the scores are unchanged. Next, the program calls another swap function. This time, through the use of references, the argument variables’ values are successfully exchanged—giving me the great big score and leaving you with the small one. Figure 6.2 shows the program in action.