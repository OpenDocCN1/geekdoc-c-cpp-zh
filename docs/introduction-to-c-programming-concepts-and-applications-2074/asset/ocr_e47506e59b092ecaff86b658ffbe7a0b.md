# # CREATING YOUR FUNCTIONS

Suppose you want to write a function that takes in a string and returns the number of words the string contains.

Then, there will be a pair of parentheses, inside of which will be the parameters (c). For now, you need to specify the type of the parameter being passed and give it a name. In this example, you are passing a string and are going to counting words in string, so the parameter is of type string and has the name `str_count`.

The first part of the definition of a function is the return type (a), which states what type of the return value will be. In this example, you're counting the number of words, you'll want to return an integer, so the type is `int`.

As you now writing your own functions, you'll again have values that are specified in parentheses, but now these values are called parameters.

The next part of the definition is the function (b)—the name you will use to call the function. You're writing a function that will count words, so `word_count` seems like a reasonable name for the function.

A part of function up to this point is called the function header (d), which contains the return type, name of the function, and the parentheses giving the parameter list. The function header contains all of the information needed for the block of function to interact with the larger program.

The parameters are directly tied to the arguments. The arguments that you put in parentheses when you call a function match one-to-one with the parameters you use inside the function itself. Because the arguments and parameters are linked together so closely, the terms are used interchangeably. But if you're being careful, arguments will be the values in the function call, and parameters will be the values that come inside the parentheses of the function.

Finally, there is a pair of braces, inside of which will be the actual instructions for the function (e). This is called the function body. These are the actual contents of the block-commands run whenever the function is called. (For initial code snippet, there are no specific commands for the function body.)

> When naming functions, you should take the same care as you do when naming variables. Use a descriptive, memorable, and consistent name.

![](bbox=[0.156, 0.796, 0.492, 0.903])

Sending in parameters is called passing. When you transfer a value from the calling side to the function, you say that you are "passing in" a parameter.