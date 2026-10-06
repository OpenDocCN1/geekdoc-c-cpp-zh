# Functions

value of the declaration. If you declared functions in the file, you can call them in the REPL after the file has been loaded. For this reason, files you load into the REPL do not always need statements at the end that call functions, and they often do not print statements to display output.

Basically, the REPL gives you the ability to "play around" with the code. Using a script simply runs it and does what it says. You should ask your instructor about this, but odds are good that any code you submit for grading should be in the form of a script that includes calls that demonstrate the functionality of the script and prompt users for input. In this case, you can use the :load option in the REPL when you are working on the program, before you turn it in, make sure it runs properly and does what you want used as a script.

# ## 4.10 End of Chapter Material

# ### 4.10.1 Problem Solving Approach

The material covered in this chapter adds significant flexibility to our approach to problem solving. It also adds a number of choices you can consider when you think about what you might write for any particular line of code. You can now write functions. Technically, function declarations can go anywhere, including inside of other functions. It is best that they have some logical organization to them. In the text we will tend to group top level functions together at the top of scripts.

We also learned in this chapter about functions that are called only for their side effects. Technically this was part of our list previously in the form of calls to `print` and `println`. We now know these are special cases of a general class of options. Given what we have learned, there is a revised list of what any productive line of code might be doing.

+   1. Call a function for the side effects. Previously `print` and `println` were the only examples of what we had, but we can now be more general.
2. Declare something:
    * A variable with `var`.
    * A function with `def`. Inside of the function will be statements that can pull any of these rules. The last statement of the function should be an expression that gives the result value.
    * A declaration with `type` to give something a more meaningful name.
3. Assign a value to a variable.
4. Write an if statement.

# ### 4.10.2 Summary of Concepts

+   * Functions are used to break problems up into smaller pieces.
    * Help solve problems.