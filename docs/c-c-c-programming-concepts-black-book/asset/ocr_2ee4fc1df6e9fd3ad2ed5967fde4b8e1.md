The preceding statement tells the function pointer exactly which function it needs to point at. Eventually, the following function call is executed:

```
(*func_ptr)();
```

While calling the function with the help of function pointers, we should be careful about the usage of parenthesis. A typical erroneous call would be as follows:

```
*func_ptr()  -  Error.
```

This would mean that we call the func_ptr() function that will return a pointer. We can also pass an argument to the intended function using function pointers.

To handle function pointers, it is worth mentioning that one should know the correct way to declare, assign, and call function pointers; otherwise, it might lead to major ambiguity. The easiest definition of a function pointer would be as follows:

```
int (*func_ptr)()
```

The preceding statement declares func_ptr as a pointer to a function, which is going to return an integer. It is evident from the declaration that the * operator signifies the involvement of a pointer and the parenthesis indicates a function. However, one intriguing factor is the usage of the parenthesis around *func_ptr. The reason behind this is just to ensure the precedence relationship in declarations. If we do not provide the parenthesis, then the declaration would be as follows:

```
int *func_ptr() /* Incorrect declaration */
```

The preceding statement would mean that func_ptr is a function returning a pointer to an integer. Therefore, the parenthesis helps in signifying that func_ptr is first a pointer and then a pointer to a function, which returns an integer. To get rid of any such syntactical anomalies, it is better to use typedef as follows:

```
typedef int (*func_ptr)()
```

The preceding statement implies that func_ptr is synonymous to pointer to a function returning an integer.

Let's now discuss various characteristics of a function pointer assignment with the help of an example. Consider the preceding function pointer declaration containing typedef. In this case, we want to assign the following functions to a function pointer:

```
int my_function1();
int my_function2();
```

We can assign the address of the first function directly as follows:

```
func_ptr = &my_function1;
```

Otherwise, the assignment can be conditional as follows:

```
if(cond)
    func_ptr = &my_function1;
else
    func_ptr = &my_function2;
```

One of the most interesting aspects of a function pointer assignment is that it is not always mandatory to use the & operator while assigning a function to a function pointer. When we are using the name of a function and not calling the function itself, it is interpreted as we are using it for the sake of assigning it to a function pointer. Most of the function pointer assignments are made with the standard syntax, where the usage of & is skipped. Therefore, the following piece of code would compile without giving any error:

```
func_ptr = my_function1;
```

Now, let's discuss some complex declarations of function pointers. The following code snippet shows a function pointer declaration.

```
typedef int (*func_ptr)(float, float)
func_ptr fp1;
```

In the preceding code snippet, fp1 becomes a pointer to a function that takes two float variables as its arguments and returns an integer.