something more than twice, you should convert it into a function. You want your code to be as simple, efficient, and readable as possible. Therefore, you should write functions that include the code that you need to use multiple times throughout your program. When you need to execute it, instead of writing the section again, you simply call the function.

+   3. Another advantage is when working in a team of programmers. By splitting the application into manageable sections, each programmer can work on one independently. This way you can finish the project at a much faster rate because at the end you easily connect all the pieces.

Now, let’s take a look at a new project that’s been written with the help of functions.

As you already know, the best way to learn is by having a project in front of you. In this section we’re going to work on a simple tic tac toe game where the user will play against the computer. We’re going to start with the game instructions which are written as a separate program. We’re going to analyze the code in order to gain a better understanding of user defined functions. Let’s get to it! Here’s the code:

```
```python
# game guide
# illustrating user defined functions
def gameGuide ():
    ‘‘‘Display instructions. ’’’
    print (
    ‘‘‘ Welcome to most epic game you will ever play!

    This will be a battle of wits between you, the fleshy creature
    Against I, the all-knowing computer!
    You will start by entering a number from 0 to 8,
which will correspond to the following positions on the game board:
0 | 1 | 2
3 | 4 | 5
```
```