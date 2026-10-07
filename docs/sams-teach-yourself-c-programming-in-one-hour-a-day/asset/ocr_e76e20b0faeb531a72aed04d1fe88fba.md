Each function is called once by main(). First, the three variables to be passed are assigned values other than o on line. Line 12 prints these values to the screen. Line 15 calls the first of the two functions, by_value(). Line 17 prints the three variables again. Notice that they are not changed. The by_value() function receives the variables by value and, therefore, it can't change their original content. Line 20 calls by_ref(), and line 22 prints the values again. This time, the values have changed to o. Passing the variables by reference gives by_ref() access to the actual contents of the variables.

You can write a function that receives some arguments by reference and others by value. Just remember to keep them straight inside the function, using the redirection operator (*) to dereference arguments by reference.

| DO | DON'T |
|---|---|
 DO pass variables by value if you don't want the original value altered. | DON'T pass large amounts of data by value if it isn't necessary. You can run out of stack space. |
 DO remember to use the redirection operator to dereference the variable passed by a function. | DON'T forget that a variable passed by reference should be a pointer |

# Type void Pointers

You've seen the void keyword used in a function declaration to specify that the function either doesn't take arguments or doesn't return a value. You can also use the void keyword to create a generic pointer—pointer that can point to any type of data object. For example, the statement

```
*ptr;
```

The most common use for type void pointers is in declaring parameters. You might want to write a function that can handle different types of arguments. You can pass it type int one time, a type float the next, and so on. By declaring the function takes a void pointer as an argument, you don't restrict it to accepting a single data type. If you declare the function to take a void pointer as an argument, you can pass the function to pointer anything.

Here's a simple example: You want to write a function that accepts a numeric variable as an argument and divides it by two, returning the answer in the argument variable. Thus, if the variable val holds the value 4, after a call to half(val), the variable val is equal