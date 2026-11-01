# Hint

You don't have to use parameter names in a prototype; all you have to include are the parameter types. For example, the following is a perfectly valid prototype that declares askYesNo2(), a function with one string parameter that returns a char.

```
char askYesNo2(string);
```

Even though you don't have to use parameter names in prototypes, it's a good idea to do so. It makes your code clearer, and it's worth the minor effort.

From the header of askYesNo2(), you can see that the function accepts a string object as a parameter and names that parameter question.

```
char askYesNo2(string question)
```

Unlike prototypes, you must specify parameter names in a function definition. You use a parameter name inside a function to access the parameter value.

# Trap

The parameter types specified in a function prototype must match the parameter types listed in the function definition. If they don't, you'll generate a nasty compile error.

# Passing Values to Parameters

The askYesNo2() function is an improvement over askYesNo1(). The new function allows you to ask your own personalized question by passing a string prompt to the function. In main(), I call askYesNo2() with:

```
char answer2 = askYesNo2("Do you wish to save your game?");
```

This statement calls askYesNo2() and passes the string literal argument "Do you wish to save your game?" to the function.

# Using Parameter Values

askYesNo2() accepts "Do you wish to save your game?" into its parameter question, which acts like any other variable in the function. In fact, I display question with:

```
cout << question << " (y/n): ";
```