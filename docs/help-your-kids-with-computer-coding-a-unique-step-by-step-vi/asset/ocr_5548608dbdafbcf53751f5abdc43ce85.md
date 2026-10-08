# # Functions

A function is a piece of code that performs a specific task. It bundles the code, gives it a name, and can be used any time by “calling” it. A function can be used to avoid entering the same lines of code more than once.

SEE ALSO
Silly 132–123 > sentences
Variables and 138–139 > functions

# ## Useful functions

Python contains lots of useful functions for performing certain tasks. When a function is called, Python retrieves the code for that function and then runs it. When the function is finished, the program returns to the line of code that called it and runs the next command.

![](bbox=[0.063, 0.423, 0.28, 0.463])

![](bbox=[0.368, 0.423, 0.585, 0.463])

![](bbox=[0.673, 0.423, 0.89, 0.463])

“print()” function
This function lets the program send output to the user by printing instructions or results on the screen.

“input()” function
This function is the offset of “print()” function. It lets the user give instructions or data to the program by typing them in.

“randint()” function
This function gives a random number (like throwing a dice). It can be used to add an element of chance to programs.

# ## Making and calling functions

The functions that come with Python aren’t the only ones that can be used. To make a new function, collect the code you want to use in a special “wrapper” and give it a name. This name allows the function to be called whenever it is needed.

![](bbox=[0.693, 0.587, 0.873, 0.706])

+   1 Define a function
The definition of a function will always have the keyword “def” and the function’s name at the beginning of the code.

+   2 Call the function
Typing the function name followed by parentheses into the shell window calls the function and shows the output.

```
def greeting():
    print('Hello!')
```

A colon marks the end of the function’s name and the start of the code it contains

```
>>> greeting():
Hello!
```

This is the code within the function

The “greeting” function is called and the output is displayed

Parentheses show that this is a function call, not a variable