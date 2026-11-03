The following parameter appears in the function header for bubble (line 49)

int (*compare)(int a, int b)

This tells bubble to expect a parameter (compare) that's a pointer to a function that receives two integer parameters and returns an integer result. Parentheses are needed around *compare to group the * with compare to indicate that compare is a *pointer*. If we had not included the parentheses, the declaration would have been

int *compare(int a, int b)

which declares a function that receives two integers as parameters and returns a pointer to an integer.

The function prototype for bubble is shown in line 7. The third parameter in the prototype could have been written as

int (*)(int, int);

without the function-pointer name and parameter names.

The function passed to bubble is called in an if statement (line 60) as follows:

if ((*compare)(work[count], work[count + 1]))

Just as a pointer to a variable is dereferenced to access the value of the variable, *a pointer to a function is dereferenced to use the function.*

The call to the function could have been made without dereferencing the pointer as in

if (compare(work[count], work[count + 1]))

which uses the pointer directly as the function name. We prefer the first method of calling a function through a pointer because it explicitly illustrates that compare is a pointer to a function that's dereferenced to call the function. The second method of calling a function through a pointer makes it appear as if compare is an *actual* function. This may be confusing to a programmer reading the code who would like to see the definition of function compare and finds that it's *never defined* in the file.



# ### 7.12.2 Using Function Pointers to Create a Menu-Driven System

A common use of function pointers is in text-based *menu-driven systems*. A user is prompted to select an option from a menu (possibly from 1 to 5) by typing the menu item's number. Each option is serviced by a different function. Pointers to each function are stored in an array of pointers to functions. The user's choice is used as an index in the array, and the pointer in the array is used to call the function.

Figure 7.28 provides a generic example of the mechanics of defining and using an array of pointers to functions. We define three functions—function1, function2 and function3—that each take an integer argument and return nothing. We store pointers to these three functions in array f, which is defined in line 14. The definition is read beginning at the leftmost set of parentheses, *f is an array of 3 pointers to functions that each take an int as an argument and return void.* The array is initialized with the names of the three functions. When the user enters a value between 0 and 2, the value is used as the index into the array of pointers to functions. In the function call (line 25), f[choice] selects the pointer at location choice in the array. *The pointer is dereferenced to call the func-*