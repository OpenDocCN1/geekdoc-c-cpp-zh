That is, a type (the return type), followed by an identifier (the name of the function), followed by a list of parameters in parentheses, followed by the body of the function (the statements to be executed). The list of arguments required by the function is called a *parameter list* and its elements are called *parameters* (or *formal arguments*). The list of parameters can be empty, and if we don't want to return a result we give **void** (meaning “nothing”) as the return type. For example:

```
    void write_sorry()           // take no argument; return no value
    {
        cout << "Sorry\n";
    }
```

The language-technical aspects of functions will be examined more closely in Chapter 8.

# ### 4.5.1 Why bother with functions?

We define a function when we want a separate computation with a name because doing so

+   ·   Makes the computation logically separate
·   Makes the program text clearer (by naming the computation)
·   Makes it possible to use the function in more than one place in our program
·   Eases testing

We'll see many examples of each of those reasons as we go along, and we'll occasionally mention a reason. Note that real-world programs use thousands of functions, some even hundreds or thousands of functions. Obviously, we would never be able to write or understand such programs if their parts (e.g., computations) were not clearly separated and named. Also, you'll soon find that many functions are repeatedly useful and you'd soon tire of repeating equivalent code. For example, you might be happy writing `x*x` and `7*7` and `(x+7)*(x+7)`, etc. rather than **square(x)** and **square(7)** and **square(x+7)**, etc. However, that's only because **square** is a very simple computation. Consider square root (called **sqrt** in C++): you prefer to write **sqrt(x)** and **sqrt(7)** and **sqrt(x+7)**, etc. rather than repeating the (somewhat complicated and many lines long) code for computing square root. Even better: you don't have to even look at the computation of square root because knowing that **sqrt(x)** gives the square root of **x** is sufficient.

In §8.5 we will address many function technicalities, but for now, we'll just give another example.

![](bbox=[0.885, 0.43, 0.925, 0.47])