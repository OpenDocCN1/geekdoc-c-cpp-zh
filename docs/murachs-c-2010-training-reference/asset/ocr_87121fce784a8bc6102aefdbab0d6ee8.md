# How to use optional parameters

When you code a method, you may occasionally provide default values for one or more parameters in case the user doesn't provide values for them. To do that, you can use a new feature of C# 2010 called optional parameters. 6-3 illustrates how optional parameters work.

To declare an optional parameter, you assign a default value to the parameter. Then, if a value is not passed to this parameter, the default value is used. In the FutureValue method in this figure, for example, the monthly investment parameter is required, but the interest rate and months parameters are optional.

The first statement that calls this method passes arguments for all three parameters. This works just like it would if all of the parameters were required. The second statement, however, omits the argument for the third parameter. Because of that, the default value for that parameter is used.

When you use optional parameters, you should realize that they must be coded after all required parameters. In addition, you can't omit an argument for one optional parameter and pass an argument for another optional parameter that appears later in the parameter list. At least, you can't do that if you omit optional parameter if you pass the arguments by position. However, you can omit an argument for any optional parameter if you pass the arguments by name.

# How to pass arguments by name

To pass arguments by name, you code the name of the parameter followed by a colon and the name of the argument. This is illustrated in the third and fourth statements in figure 6-3 that call the FutureValue method. Both of these statements pass arguments to the first and third parameters, but omit the argument for the second parameter. The only difference between the two is that the arguments are coded in a different sequence. This is another advantage of passing arguments by name.

You can also pass some arguments by position and some by name as illustrated in the last statement. Here, the first argument passes a value to the first parameter by position, and the second argument passes a value to the third parameter by name.