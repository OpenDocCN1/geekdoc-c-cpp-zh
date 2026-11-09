# # Playing with loops

When you’re coding a game, you often need to run the same bit of code several times, but it would be pretty boring if you had to type it in every single time. Luckily, you can use a loop to run the same block of code over and over again. There are many different types of loops.

# ## “For” loops

When you know exactly how many times you want a loop to repeat, you can use a for loop. In this example, the code prints “You are the high scorer!” ten times. Try out the code for yourself in the shell window.

```
```python
>>> for count in range(1, 11):
        print("You are the high scorer!")
```
```

This is the loop variable.

The code that gets repeated is known as the “loop body.”

![](bbox=[0.589, 0.139, 0.965, 0.369])

# ### Loop variable

The loop variable keeps track of how many times the loop has run so far. At the start of the loop, it’s equal to the first number in the range. The second time around, it’s equal to the second number in the range, and so on. Once it completes the second-to-last number in the range, the loop stops.

![](bbox=[0.043, 0.649, 0.478, 0.872])

# ### Loop body

The block of code that gets repeated in a loop is called the loop body. You must always indent the commands in the body four spaces from the beginning of the line that starts the for loop.

# ## EXPERT TIPS
### Range

In Python, the word range followed by two numbers in parentheses stands for “all the numbers in the list from the first number to the second-to-last number.” Therefore, range(1, 5) contains the numbers 1, 2, 3, and 4, but not 5, so the loop runs four times.

![](bbox=[0.616, 0.819, 0.952, 0.968])