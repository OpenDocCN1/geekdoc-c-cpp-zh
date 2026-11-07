corresponding actual parameter, which is **num**, and the variable **val** copies the value of its corresponding actual parameter, which is also **num**. Thus, both **num** and **ref** refer to the same memory location, which is **num**. Figure 7–19 illustrates this situation.

![](bbox=[0.182, 0.178, 0.912, 0.316])

**FIGURE 7-19**  Parameters of the function `squareFirst`

Any changes that **ref** makes immediately change **num**. Any changes made by **val** do not affect **num**. (Note that the value of **num** before the function `squareFirst` executes is 14.)

We recommend that you walk through the program in Example 7–8. The output shows the order in which the statements execute.

# Reference Parameters and Value-Returning Functions

In Chapter 6, in the discussion of value-returning functions, you learned how to use value parameters only. You can also use reference parameters in a value-returning function, although this approach is not recommended. By definition, a value-returning function returns a single value; this value is returned via the return statement. If a function needs to return more than one value, you should change it to a void function and use the appropriate reference parameters to return the values.

# Scope of an Identifier

The previous sections and Chapter 6 presented several examples of programs with user-defined functions. Identifiers are declared in a function heading, within a block, or outside a block. A question naturally arises: Are you allowed to access any identifier anywhere in the program? The answer is no. You must follow certain rules to access an identifier. The **scope** of an identifier refers to where in the program an identifier is accessible (visible). Recall that an identifier is the name of something in C++, such as a variable or function name.

This section examines the scope of an identifier. First, we define the following two terms:

**Local identifier:** Identifiers declared within a function (or block).

Local identifiers are not accessible outside of the function (block).

**Global identifier:** Identifiers declared outside of every function definition.

Also, C++ does not allow the nesting of functions. That is, you cannot include the definition of one function in the body of another function.