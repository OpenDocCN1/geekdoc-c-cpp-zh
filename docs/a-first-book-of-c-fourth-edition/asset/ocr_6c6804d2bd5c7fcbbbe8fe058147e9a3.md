```
int firstnum, secnum;

cout << "\nEnter a number: ";
cin >> firstnum;
cout << "Great! Please enter a second number: ";
cin >> secnum;

findMax(firstnum, secnum); // the function is called here

return 0;
}
```

This program would be complete if there were a function definition for findMax(). However, you really don’t need a correct findMax() function to test and run what has been written; you just need a function that acts as though it is. A "fake" findMax() that accepts the correct number and types of parameters and returns values of the proper form for the function call is all you need for initial testing. This fake function, called a stub, is the beginning of a final function and can be used as a placeholder for the final function until it’s completed. A stub for findMax() is as follows:

```
void findMax(int x, int y)
{
    cout << "In findMax()\n";
    cout << "The value of x is " << x << endl;
    cout << "The value of y is " << y << endl;
}
```

This stub function can now be compiled and linked with the previously completed code to produce an executable program. The code for the function can then be further developed with the "real" code when it’s completed, replacing the stub portion.

The minimum requirement of a stub function is that it compiles and links with its calling module. In practice, it’s a good idea to have a stub display a message that it has been entered successfully and display the values of its received parameters, as in the stub for findMax(). As the function is refined, you let it do more, perhaps allowing it to return intermediate or incomplete results. This incremental, or stepwise, refinement is an important concept in efficient program development that gives you the means to run a program that doesn’t yet meet all its final requirements.

# Functions with Empty Parameter Lists

Although useful functions having an empty parameter list are extremely limited, they can occur. (You see one such function in Exercise 15 at the end of this section.) The function prototype for this type of function requires writing the keyword void or nothing at all between the parentheses following the function’s name. For example, both these prototypes

```
int display();
```

and

```
int display(void);
```