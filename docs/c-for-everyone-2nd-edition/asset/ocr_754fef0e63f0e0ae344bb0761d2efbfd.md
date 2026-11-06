# Programming Tip 5.1

![](bbox=[0.13, 0.13, 0.28, 0.19])

# Function Comments

Whenever you write a function, you should *comment* its behavior. Comments are for human readers, not compilers, and there is no universal standard for the layout of a function comment. In this book, we will use the following layout:

```
/**
   Computes the volume of a cube.
   @param side_length the side length of the cube
   @return the volume
*/
double cube_volume(double side_length)
{
   double volume = side_length * side_length * side_length;
   return volume;
}
```

Function comments explain the purpose of the function, the meaning of the parameter variables and return value, as well as any special requirements.

This particular documentation style is borrowed from the Java programming language. It is widely supported by C++ tools as well, for example by the Doxygen tool (www.doxygen.org).

The first line of the comment describes the purpose of the function. Each @param clause describes a parameter variable and the @return clause describes the return value.

Note that the function comment does not document the implementation (how the function does what it does) but rather the design (what the function does, its inputs, and its results). The comment allows other programmers to use the function as a "black box".

# 5.3 Parameter Passing

Parameter variables hold the argument values supplied in the function call.

In this section, we examine the mechanism of passing arguments into functions. When a function is called, its *parameter variables* are created. (Another commonly used term for a parameter variable is *formal parameter*.) In the function call, an expression is supplied for each parameter variable, called the *argument*. (Another commonly used term for this expression is *actual parameter*.) Each parameter variable is initialized with the value of the corresponding argument.

Consider the function call illustrated in Figure 3:

```
double result1 = cube_volume(2);
```

![](bbox=[0.5, 0.72, 0.95, 0.85])

A recipe for a fruit pie may say to use any kind of fruit. Here, "fruit" is an example of a parameter variable. Apples and cherries are examples of arguments.