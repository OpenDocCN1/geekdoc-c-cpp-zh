
## 2. Write the Function Definition.

The second thing we must do in writing our own function is to provide the function definition or implementation. The function definition consists of comments, a header and a body. The general form of the function body is as follows:

```
// Function comments
returnType functionName (formal-argument-list) {
    executable-statements;
    return (return-value);
}
```

The function definition to calculate the area of a rectangle would look like this:

```
// calculateArea.c
// Calculates area of a rectangle given its length and width.
// Returns the area of a rectangle.
int calcRectArea(int length, int width) {
    int area;
    area = length * width;
    return area;
}
```

- The function comments describe what the function accomplishes as well as what the return value (if any) represents. The comments inform us what the function calculates the area of a rectangle given its length and width. The comments also inform us that the function returns an `int` that represents the area of the rectangle.
- The function returns the calculated area of the rectangle and the return value is of data type `int`.
- The function name is `calcRectArea()`.
- The function formal argument list consists of an `int` type in the first position, `length`, and an `int` type in the second position, `width`. This means that the function is expecting two input arguments with the first of type `int` and the second of type `int`.

Note that even though the first argument is named length and the second argument is named width, there is no connection between these names and the names of the actual arguments passed in the call to the function itself! More on this soon.

When the function is invoked, storage for the formal parameters, length and width, will be allocated and the storage will be initialized to the values that were passed into the function when the function was called.

Note that the arguments, length and width, are local variables that are "visible" inside the function and can be used within the function but nowhere else in the program.

Note that while the names of the formal parameters are optional in the function prototype, they must be included in the function header.

- The function body contains the statements that will be executed when the function is called or used. The function uses curly braces { } to indicate the beginning and ending of the function body. Note that there is no semi-colon at the end of the function body!

In our function, the executable statements include the declaration of an int variable called area. The function also performs a calculation of the area of the rectangle. The calculated value of the rectangle's area is assigned to variable area.

- The return value is the value returned by the function to the calling program code. Our function returns an int to the calling program code.

In summary, our function body declares a variable named area, calculates the area using the height and width passed in as arguments and returns the calculated area to the calling program code. Note that the function is placed in the program after the end of the main() function.

## 3. Write the Call(s) to the Function:

The third thing we need to do is call the function whenever we need it.

```
// calcAreaRect.c
// Calculates the area of a rectangle.
int main(void) {
    int length, width, area;

    length = 8;
    width = 6;
    area = calcRectArea(length, width);
    printf("The area is %d\n", area);
    return 0;
}
```

Here we declare variables length, width and area and assign values to length and width. A call is made to the function calcRectArea(), passing the two parameters, length and width. The value returned by the function is assigned to area, which is then output.

The function call can be used in the program code itself the same way that any other valid C statement can be used. Functions can be called in main() or any other function and can be called as often as necessary or not at all. Note that there is always just one function declaration and one implementation (definition), but there can be multiple calls to a given function.

Below is our complete code which include multiple examples of calls to our function to calculate the area of a rectangle:

```
//calcRectArea.c
// Calculates the areas of various rectangles.

int calcRectArea(int length, int width);

int main(void) {
    int length, width, area, l, w;

    // Function Call 1
    length = 8;
    width = 6;
    area = calcRectArea(length, width);
    printf("The area = %d\n", area);

    // Function Call 2
    l = 5;
    w = 3;
    area = calcRectArea(l, w);
    printf("The area = %d\n", area);

    // Function Call 3
    printf("The area = %d\n", calcRectArea(4, 8));

    // Function Call 4
    calcRectArea(2, 6);

    return 0;
}

// Calculates area of a rectangle given its length and width.
// Returns the area of a rectangle.

int calcRectArea(int length, int width) {
    int area;

    area = length * width;
    return area;
}
```

### Function Call 1:

Values are assigned to variables length and width and the variables are the arguments to the function calcRectArea( ). The function returns a calculated value that is assigned to area, which is then output.

### Function Call 2:

Values are assigned to variables `l` and `w` and the variables are the arguments to the function `calcRectArea()`. The function returns a calculated value that is assigned to `area`, which is then output.

Note that in this case the names of the arguments that are passed to the function (called the *actual parameters*) do not have the same name as the arguments that are received by the function (called the *formal parameters*). The names do not need to match! C simply passes the first actual parameter to the first formal parameter, the second actual parameter to the second formal parameter, etc.

However, the number of actual parameters must equal the number of formal parameters (i.e., the number of parameters that are passed to a function must be the same as the number of parameters that the function is declared to receive). Additionally, the data type of the first actual parameter must match the data type of the first formal parameter, the data type of the second actual parameter must match the data type of the second formal parameter, etc.

### Function Call 3:

The function return value is not assigned to a variable for output as the function call is itself included within the `printf()` statement! Here the return `int` value is substituted into the `printf()` string for the `%d` format specifier and the return value of the function is immediately output.

### Function Call 4:

This function call, while technically correct, does not use the value returned by the function because we're calling the function without assigning or using the return value in any way. The returned value is simply ignored! We'll see other examples of function calls in which the returned value goes unused.

### Function Advantages

- Programs become more readable.
- Function can be tested and debugged separately from the rest of the program.
- By isolating a logic step in a function, the parts of a program are more independent and the likelihood of errors are reduced.
- The same function can be invoked from different places in a program. Therefore, a commonly used chunk of logic needs to be written only once.

## Flow of Program Execution

The flow of execution of a program refers to the order in which the C code is executed. Execution always begins at the first statement in main() and statements are executed one after another, from first to last.

For example, consider the following program that swaps the value of two variables:

```
// flow.c

int main(void) {
    int x, y, temp;   // Statement 1

    x = 5;            // Statement 2
    y = 8;            // Statement 3

    temp = x;         // Statement 4
    x = y;            // Statement 5
    y = temp;         // Statement 6

    return 0;         // Statement 7
}
```

The statements in the program above are executed in the following order:

- Statement 1
- Statement 2
- Statement 3
- Statement 4
- Statement 5
- Statement 6
- Statement 7

Adding function definitions to a program does not alter the flow of execution of the program. However, the statements within the function are not executed until the function is called.

When a function call is made, control of the program jumps to the first statement in the program. All of the statements in the function are executed until either a return statement is reached or a closing brace to the function is reached. Control of the program returns to the location in the function where the function call was made.
