
# Passing by value

```
void sneezy(int x);
int main()
{
  int times = 20;
  sneezy(times);
  ...
}
void sneezy(int x)
{
  ...
}
```

creates a variable
called times, assigns
it the value of 20

![](img/cd111a87c1db9aff4db4b18834327463_401_0.png)

times
two variables,
two names

creates a variable
called x, assigns it
the passed value of 20

![](img/cd111a87c1db9aff4db4b18834327463_401_1.png)

x

# Passing by reference

```
void grumpy(int &x);
int main()
{
  int times = 20;
  grumpy(times);
}
void grumpy(int &x)
{
  ...
}
```

creates a variable
called times, assigns
it the value of 20

![](img/cd111a87c1db9aff4db4b18834327463_401_2.png)

one variable,
two names

times, x

makes x an
alias for times

![](img/cd111a87c1db9aff4db4b18834327463_401_3.png)

Figure 8.2 Passing by value and passing by reference.

# Listing 8.4 swaps.cpp

```
// swaps.cpp -- swapping with references and with pointers
#include <iostream>
void swap(int &a, int &b); // a, b are aliases for ints
void swap(int *p, int *q); // p, q are addresses of ints
void swap(int a, int b); // a, b are new variables
int main()
{
  using namespace std;
  int wallet1 = 300;
  int wallet2 = 350;
```

```
cout << "wallet1 = $" << wallet1;
cout << "wallet2 = $" << wallet2 << endl;
```

```
cout << "Using references to swap contents:\n";
swapr(wallet1, wallet2);   // pass variables
cout << "wallet1 = $" << wallet1;
cout << "wallet2 = $" << wallet2 << endl;
```

```
cout << "Using pointers to swap contents again:\n";
swapp(&wallet1, &wallet2); // pass addresses of variables
cout << "wallet1 = $" << wallet1;
cout << "wallet2 = $" << wallet2 << endl;
```

```
cout << "Trying to use pass by value:\n";
swapv(wallet1, wallet2);   // pass values of variables
cout << "wallet1 = $" << wallet1;
cout << "wallet2 = $" << wallet2 << endl;
}
```

```
void swapr(int a, int &b)   // use references
{
    int temp;

    temp = a;   // use a, b for values of variables
    a = b;
    b = temp;
}
```

```
void swapp(int *p, int *q)   // use pointers
{
    int temp;

    temp = *p;   // use *p, *q for values of variables
    *p = *q;
    *q = temp;
}
```

```
void swapv(int a, int b)   // try using values
{
    int temp;

    temp = a;   // use a, b for values of variables
    a = b;
    b = temp;
}
```

# Chapter 8 Adventures = Functions

Here's the output of the program in Listing 8.4:

```
wallet1 = $300 wallet2 = $350    << original values
Using references to swap contents:
wallet1 = $350 wallet2 = $300      << values swapped
Using pointers to swap contents again:
wallet1 = $300 wallet2 = $350    << values swapped again
Trying to use by value:
wallet1 = $300 wallet2 = $350      << swap failed
```

As you'd expect, the reference and pointer methods both successfully swap the two wallets, whereas the by value method fails.

# Program Notes

First, note how each function in Listing 8.4 is called:

```
swapr(wallet1, wallet2);      // pass variables
swap(&wallet1, &wallet2);      // pass addresses of variables
swapv(wallet1, wallet2)        // pass values of variables
```

Passing by reference (swapr(wallet1, wallet2)) and passing by value (swapv(wallet1, wallet2)) look identical. The only way you can tell that swapr() passes by reference is by looking at the prototype or the function definition. However, the presence of the address operator (&) makes it obvious when a function passes by address ((swap(&wallet1, &wallet2)). (Recall that the declaration *p means p is a pointer to an int and the argument corresponding to p should be an address, such as &wallet1.)

Next, consider the code for the functions swap() (passing by reference) and swapv() (passing by value). The only outward difference between the two is how the function parameters are declared:

```
void swapr(int &a, int &b)
void swapv(int *a, int *b)
```

The internal difference, of course, is that in swap() the variables a and b serve as aliases for wallet1 and wallet2, so swapping a and b are new variables that copy the values of wallet1 and wallet2, so swapping a and b has no effect on wallet1 and wallet2.

Finally, compare the functions swap() (passing by reference) and swap() (passing by a pointer). The first difference is in how the function parameters are declared:

```
void swap(int &a, int &b)
void swapv(int *p, int *q)
```

The second difference is that the pointer version requires the * dereferencing operator throughout the function uses p and q.
Earlier, I would initialize a reference variable with argument values from the function call. So reference function arguments are initialized to the argument passed by the function call. That is, the

following function call initializes the formal parameter a to wallet1 and the formal parameter b to wallet2:

swapr(wallet1, wallet2);

# Reference Properties and Oddities

Using reference arguments has several twists you need to know about. First, consider Listing 8.5. It uses two functions to cube an argument. One takes a type double argument, and the other takes a reference to double. The actual code for cubing is purpose-fully bit odd to illustrate a point.

Listing 8.5 cubes.cpp

```
// cubes.cpp -- regular and reference arguments
#include <iostream>
double cube(double a);
double refcube(double &ra);
int main ()
{
    using namespace std;
    double x = 3.0;

    cout << cube(x) << " = cube of " << x << endl;
    cout << " = " << refcube(x);
    cout << " = " << cube of " << x << endl;
    return 0;
}

double cube(double a)
{
    a *= a * a;
    return a;
}

double refcube(double &ra)
{
    ra *= ra * ra;
    return ra;
}
```

Here is the output of the program in Listing 8.5:

27 = cube of 3
27 = cube of 27

# Reference Variables

Note that the refcube() function modifies the value of x in main() and cube () doesn't, reminds which why you passing by value is the norm.The variable a local to cube().It is initialized to the value of x, but changing a has no effect on x. But because refcube() uses a reference argument, it changes it to ra are actually made to x. If your intent is that function you use the information passed to it without modifying the information, and if you're using a reference, you should use a constant reference. Here, for example, you should use const double in the function prototype and header:

```
double refcube(const double&);
```

If you do this, the compiler generates an error message when it finds coding the value of ra.

Incidently, if you need to write a function along the lines of this example (that is, using a basic numeric type), you should use passing by value rather than more exotic passing by reference.Reference arguments become useful with larger data units, as structures and classes, you will soon see.

Functions that pass by value, as the cube () function in Listing 8.5, can use many kinds of actual arguments. For example, all the following are called:

```
double z = cube(x + 2.0); // evaluate x + 2.0, pass value
z = cube(8.0); // pass the value 8.0
int k = 10;
z = cube(k); // convert value of k to double, pass value
double yo[3] = { 2.2, 3.4, 4.4 }; = cube(yo[2]); // pass the value 4.4
```

Suppose you try similar arguments for a function to a reference parameter. It would seem that a passing reference should be more restrictive.After all, if ra is the alternative name for variable, then the actual argument should be variable. Something like the following doesn't make sense because the expression x + 3.0 is not a variable.

```
double z = refcube(x + 3.0); // should not compile
```

For example, you can't assign a value to this expression:

```
x + 3.0 = 5.0; // nonsensical
```

What happens if you try call refcube(x + 3.0)? In contemporary C++,it's an error, and most compilers will tell you you a warning along the following lines:

```
Warning: Temporary used for parameter 'ra' in call to refcube(double &)
```

The reason for this milder response is C++, in its early years, did allow you to pass references to a variable. In some cases, it does what. What happens is that x + 3.0 is not a type double, the program creates a temporary, nameless variable, initializing it to the value of the expression x + 3.0.Then ra becomes a reference to a temporary variable. Let's take a closer look at temporary variables and when they are and not created.
