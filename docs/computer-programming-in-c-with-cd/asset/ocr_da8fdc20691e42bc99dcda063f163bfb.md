In the preceding code snippet, `a` is a variable that holds a value, which is passed in the `radius()` function from the calling function. Now, if we assume that `a` is equal to 4, the preceding code snippet will look like this:

```
```cpp
result = (3.14*4*4)
```
```

The output of the preceding code snippet is:

```
```text
50.24
```
```

Now, let’s consider Listing 12 to know how macros work in a program. Listing 12 shows how to create a variable macro, PI, and a function macro, radius (a) (you can find the Preprocessor.cpp file on the code/chapter1 folder):

# ▶ Listing 12: Using Preprocessor Directives

```
```cpp
#include <iostream.h>
#define PI 3.14
#define radius(a) (PI*a*a)

int main()
{
        double p = PI;
        double result;
        cout << "value of p is " << p << endl;
        result = radius(4);
        cout << "value of function macro is " << result << endl;
        return 0;
}

Output:

value of p is 3.14
value of function macro is 50.24
```
```

In Listing 12, we define a macro, PI, and assign it the value 3.14. We then define a function, `radius()`, with a parameter, `a`. In the `main()` function we declare two double type variables, `p` and `result`, and assign the value of the PI macro to the variable `p`. Next, we call the `radius()` function and pass the parameter value 4, which returns the value and stores it to the result variable. Finally, the value of both the variables, `p` and `result`, are displayed.

> > **TEST YOUR KNOWLEDGE**
> >
> > **Q5.** Write a program to implement the `#define` preprocessor directive.
> >
> > **Ans.**
> >
> > ```cpp
> > #include <iostream.h>
> > #define cel(v) (((v-32)*5)/9
> > ```