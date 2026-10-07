# Function Review

# 309

```
double cube(double x); // function prototype
int main()
{
    double q = cube(1.2); // function call
    ...
    double cube(double x) // function definition
{
        return x * x * x;
    }
```

![](bbox=[0.138, 0.185, 0.725, 0.319])

cube() calculates
return value and
places it here:
function header
tells cube() to use
a type double value

main() looks here
for the return value
and assigns it to q;
cube() prototype
tells main() to
expect type double

| 1.728 |
| return value location |

Figure 7.1 A typical return value mechanism.

(Usually, having multiple return statements in a function is considered potentially confusing, and some compilers might issue a warning. However, the code here is simple enough to understand.)

Functions with return values are like functions in Pascal, FORTRAN, and BASIC. They return a value to the calling program, which can then assign that value to a variable, display the value, or otherwise use it. Here's a simple example that returns the cube of a type double:

```
double cube(double x) // x times x times x
{
    return x * x * x; // a type double value
```

For example, the function call cube (1.2) returns the value 1.728. Note that this return statement uses an expression. The function computes the value of the expression (1.728, in this case) and returns the value.

# Prototyping and Calling a Function

By now you are familiar with function calls, but you may be less comfortable with function prototyping because that's often hidden in the include files. Listing 7.2 shows the cheers() and cube() functions used in a program; notice the function prototypes.