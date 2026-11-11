![](bbox=[0.159, 0.109, 0.839, 0.261])

# ### 2.5.3 Initialization of variables

The process of storing a value inside a variable is called as *initialization* of the variable. Given below is the syntax to initialize a variable with the value returned by the expression.

```
variable-name = expression;
```

Note that, every variable must be declared before it is initialized using the above syntax. The operator `=` is called as an assignment operator, which is used to initialize a value of the expression to a particular variable. A key point to note here is that the declaration of any variable always happens at the time of compilation of the program whereas the initialization of the variable happens at the time of execution of the program. This means that it is compiler who allocates the memory for the variable which is created in the program; however, the value will actually be stored inside the variable at the time of execution of the program. For example, let us consider the two statements given below:

```
int age; /*Declaration of the variable named as 'age'*/
age=10; /*Initialization of the variable 'age' with a value 10*/
```

The first statement declares a variable named as age, which is of type integer and hence the compiler will allocate 2 bytes for the variable age in the main memory (RAM) of the computer system as shown in Figure 2.10. Furthermore, it is important to note that the variable age will contain junk value at the time of compilation as shown in Figure 2.10.

![](bbox=[0.601, 0.588, 0.889, 0.735])

The next statement stores the value 10 inside the variable age as shown in Figure 2.11. Note that the constant 10 will be stored inside the variable a at the time when the program executes and not at the time when the program compiles. Therefore, it is important to remember that, the value of any variable will always be unknown to the compiler because every initialization made in the program always happens when the program starts executing.

![](bbox=[0.599, 0.755, 0.894, 0.918])

The variable once declared can be initialized multiple times as and when the program executes. It is important