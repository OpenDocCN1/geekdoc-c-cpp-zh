inadvertently change data stored in a variable. The function gets a copy of the data to use. It can change its copy and, of course, change any variables declared inside it. However, unless specific steps to do so are taken, a function isn't allowed to change the contents of variables declared in other functions.

![](bbox=[0.23, 0.28, 0.88, 0.56])

Figure 6.3 The findMax() function receives actual values

Next, you begin writing the findMax() function to process the values passed to it.

# Defining a Function

A function is defined when it's written. Each function is defined once (that is, written once) in a program and can then be used by any other function in the program that declares it suitably.

Like the main() function, every C++ function consists of two parts, a function header and a function body, as shown in Figure 6.4. The function header's purpose is to identify the data type of the value the function returns, give the function a name, and specify the number, order, and type of arguments the function expects. The function body's purpose is to operate on the passed data and return, at most, one value directly back to the calling function. (In Section 6.3, you see how a function can be made to return multiple values indirectly by using its arguments.)

The function header is always the first line of a function and contains the function's return value type, its name, and the names and data types of its arguments. Because findMax() doesn't formally return any value and receives two integer values, the following function header can be used:

```
void findMax(int x, int y)
```

no semicolon