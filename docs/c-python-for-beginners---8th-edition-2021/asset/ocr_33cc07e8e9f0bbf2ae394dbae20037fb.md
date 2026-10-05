# Using Comments

When you write your code, the flow of it, what each variable does, the overall program will operate and is all inside of your head. Another programmer could follow the code line by line over time, it can become difficult to read.

# #COMMENTS!

Programmers use a method of keeping their code readable by commenting on sections. If a variable is used, the programmer comments on what it's supposed to do, for example. It's just good practice.

+   * STEP 1 Start by creating a new instance of the IDLE Editor (File -> New File) and create a simple variable and print command:

```
a=10
print("The value of A is", a)
```

Save the file and execute.

+   * STEP 3 Resave the code and execute it. You can see that the output in the IDLE Shell is still the same as before, despite the lines being added. Simply put, the hash symbol (#) a line of text that the programmer can insert to inform them, and others, of what's going on without the user aware.

![](bbox=[0.518, 0.463, 0.931, 0.638])

+   * STEP 2 Running the code will return the line: The value of A is 10 to the IDLE Shell window, which is what we expect. Now, add some of the comments you'd normally see within code:

```
# Set the value of A to 10
a=10
# Print the current value of A
print("The value of A is", a)
```

+   * STEP 4 Let's assume that the variable A we've created is the number of lives in a game. Every time the player dies, the variable is decreased by 1. The programmer could insert an input line like the following:

```
a-=1
print("You just lost a life!")
print("You now have", a, "lives left!")
```

![](bbox=[0.518, 0.797, 0.931, 0.913])