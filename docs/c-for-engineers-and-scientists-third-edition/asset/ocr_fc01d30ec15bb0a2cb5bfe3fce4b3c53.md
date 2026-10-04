# 346 Modularity Using Functions

# 6.5 Variable Scope

Now that you have begun to write programs more than one function, you can look more closely at the variables declared in each function and their relationship to variables in other functions. By their nature, C++ functions are constructed to be independent modules. As you have seen, values are passed to a function by using the function's parameter list, and a value is returned from a function using a return statement. In this light, a function can be thought of as a closed box, with slots at the top to receive values and a single slot at the bottom to return a value (see Figure 6.14).

Values passed to the function

![](bbox=[0.303, 0.325, 0.595, 0.473])

Figure 6.14 A function can be considered a closed box

The metaphor of a closed box is useful because it emphasizes what goes inside the function, including all variable declarations in the function body, is hidden from the view of all other functions. The variables created in a function are conventionally available only to the function, they are said to be local to the function, or local variables. This term refers to the scope of an identifier; scope is the section of the program where the identifier, such as a variable, is valid or "known". This section of the program is also referred to as where the variable is "visible".

A variable can have a local scope or a global scope. A variable with a local scope is simply one with storage locations set aside for it by a declaration statement in the function body. Local variables are meaningful only when used in expressions or statements inside the function declared them. This means the same variable name can be declared and used in more than one function. For each function that declares the variable, a separate and distinct variable is created.

All the variables you have used until now have been local variables, a result of placing declaration statements that cause the computer to reserve storage for the declared variable. As you will see in the next section, declaration statements can be placed outside functions and also need not act as definitions that reserve new storage for the declared variable.

A variable with global scope, more commonly termed a global variable, has storage created for it by a declaration statement located outside any function. These variables can be used by all functions that are placed after the global declaration. Program 6.15 shows using this, and the same variable name has been used on purpose inside both functions in the program.