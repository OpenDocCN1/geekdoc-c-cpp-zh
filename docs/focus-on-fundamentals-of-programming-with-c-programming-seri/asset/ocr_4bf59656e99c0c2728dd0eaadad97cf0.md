Note that even though the first argument is named `length` and the second argument is named `width`, there is no connection between these names and the names of the actual arguments passed in the call to the function itself! More on this soon.

When the function is invoked, storage for the formal parameters, `length` and `width`, will be allocated and the storage will be initialized to the values that were passed into the function when the function was called. .

Note that the arguments, `length` and `width`, are local variables that are “visible” inside the function and can be used within the function but nowhere else in the program.

Note that while the names of the formal parameters are optional in the function prototype, they must be included in the function header.

+   • The function body contains the statements that will be executed when the function is called or used. The function uses curly braces { } to indicate the beginning and ending of the function body. Note that there is no semi-colon at the end of the function body!

In our function, the executable statements include the declaration of an `int` variable called `area`. The function also performs a calculation of the area of the rectangle. The calculated value of the rectangle’s area is assigned to variable `area`.

+   • The return value is the value returned by the function to the calling program code. Our function returns an `int` to the calling program code.

In summary, our function body declares a variable named `area`, calculates the area using the height and width passed in as arguments and returns the calculated area to the calling program code. Note that the function is placed in the program after the end of the `main()` function.