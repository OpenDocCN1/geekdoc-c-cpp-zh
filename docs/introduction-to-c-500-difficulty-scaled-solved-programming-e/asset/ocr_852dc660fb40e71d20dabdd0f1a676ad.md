clear that they are nested inside the function. Also, I use blank lines to divide the program into logical blocks, making it easier for the reader to understand the structure of the program.

Before ending this let's briefly explain the declaration and definition. A declaration is a statement that declares a name (e.g., variable) within a scope. A declaration that also sets aside memory is called definition. Then, when we write:

```
int i; this declaration is also a definition since memory is reserved for the variable. However, not all declarations are definitions. For example, we'll see such declarations when we discuss about extern
Chapter 11.
```

# Assignment of Values

The traditional way to assign a value to a variable is by using the assignment operator =. For example, the following code assigns the value 2 to a:

```
int a;
a = 2;
```

Alternatively, a variable can be initialized together with its declaration:

```
int a = 2;
```

We could also write int a = {2}; As we'll see in the next chapters, the braced {} syntax is usually used to initialize the elements of an array or structure. The braces can be left empty, in which case the variable initialized to 0.

We can also initialize more than one variable of the same type when declared. For example, the following statement declares the a, b, c, and d variables and initializes the first three with the values 2, 3, and 4, respectively. variable d is initialized with a garbage value.

```
int a = 2, b = 3, d, c = 4;
```

We could have written:

```
int a = 2, b = a+1, c = b+1;
```

The assignments take place from left to right, meaning that a first becomes 2, then b becomes 3, and then c becomes 4. Here is another way:

```
int a(2), b(a+1), c(a+2)
```

Their values become 2, 3, and 4, respectively. As you can see there are many alternatives to initialize a variable. For better readability, my preference is to initialize each variable in a separate statement after its declaration. In some examples I'm not consistent and initialize it when declared; the reason is to save space.

In an assignment, the expression on the right side can be a number, a variable, or a more complex expression, such as an expression that uses arithmetic operators. The value of expression is first evaluated and then assigned to the variable. Also, the same variable can be used on both sides of.

```
int a = 2;
a = a-5; // a becomes -3.
```