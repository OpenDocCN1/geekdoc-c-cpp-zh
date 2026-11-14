

```cpp
if (x % 2 == 1)    // odd
    x = 3 * x + 1;
else               // even
    x = x / 2;
```

Like the if-statement, the loop can be written without braces when there is only one statement.

C++ also offers a do-while-loop. In this case, the condition for continuation is tested at the end:

```cpp
double eps = 0.001;
do {
    cout << "eps = " << eps << '\n';
    eps /= 2.0;
} while (eps > 0.0001);
```

The loop is performed at least one time—even with an extremely small value for eps in our example.

### 1.4.4.2 for-Loop

The most common loop in C++ is the for-loop. As a simple example, we add two vectors5 and print the result afterward:

```cpp
double v[3], w[3] = {2., 4., 6.}, x[] = {6., 5., 4};
for (int i = 0; i < 3; ++i)
    v[i] = w[i] + x[i];
for (int i = 0; i < 3; ++i)
    cout << "v[" << i << "] = " << v[i] << '\n';
```

The loop head consists of three components:

- The initialization;
- A Continuation criterion; and
- A step operation.

The example above is a typical for-loop. In the initialization, we typically declare a new variable and initialize it with 0—this is the start index of most indexed data structures. The condition usually tests whether the loop index is smaller than a certain size and the last operation typically increments the loop index. In the example, we pre-incremented the loop variable i. For intrinsic types like int, it does not matter whether we write ++i or i++. However, it does for user types where the post-increment causes an unnecessary copy; cf. §3.3.2.5. To be consistent in this book, we always use a pre-increment for loop indices.

It is a very popular beginners' mistake to write conditions like i <= size(...). Since indices are zero-based in C++, the index i == size(...) is already out of range. People with experience in Fortran or MATLAB need some time to get used to zero-based indexing. One-based indexing seems more natural to many and is also used in mathematical literature. However, calculations on indices and addresses are almost always simpler with zero-based indexing.

5. Later we will introduce true vector classes. For the moment we take simple arrays.

As another example, we like to compute the Taylor series of the exponential function:

![](img/ba4defb7bf504868bf19451f3cd4b9bb_51_0.png)

up to the tenth term:

```cpp
double x = 2.0, xn = 1.0, exp_x = 1.0;
unsigned long fac = 1;
for (unsigned long i = 1; i <= 10; ++i) {
    xn *= x;
    fac *= i;
    exp_x += xn / fac;
    cout << "e^x is " << exp_x << '\n';
}
```

Here it was simpler to compute term 0 separately and start the loop with term 1. We also used less-equal to assure that the term $x^{10}/10!$ is considered.

The for-loop in C++ is very flexible. The initialization part can be any expression, a variable declaration, or empty. It is possible to introduce multiple new variables of the same type. This can be used to avoid repeating the same operation in the condition, e.g.:

```cpp
for (int i = xyz.begin(), end = xyz.end(); i < end; ++i) ...
```

Variables declared in the initialization are only visible within the loop and hide variables of the same names from outside the loop.

The condition can be any expression that is convertible to a bool. An empty condition is always true and the loop is repeated infinitely. It can still be terminated inside the body as we will discuss in the next section. We already mentioned that a loop index is typically incremented in the third sub-expression of for. In principle, we can modify it within the loop body as well. However, programs are much clearer if it is done in the loop head. On the other hand, there is no limitation that only one variable is increased by 1. We can modify as many variables as wanted using the comma operator (§1.3.5) and by any modification desired such as

```cpp
for (int i = 0, j = 0, p = 1; ...; ++i, j += 4, p *= 2) ...
```

This is of course more complex than having just one loop index but still more readable than declaring/modifying indices before the loop or inside the loop body.

### 1.4.4.3 Range-Based for-Loop

A very compact notation is provided by the new feature called Range-Based for-Loop. We will tell you more about its background once we come to the iterator concept (§4.1.2).

For now, we will consider it as a concise form to iterate over all entries of an array or other containers:

```cpp
int primes[] = {2, 3, 5, 7, 11, 13, 17, 19};
for (int i : primes)
    std::cout << i << " ";
```

This will print out the primes from the array separated by spaces.

### 1.4.4.4 Loop Control

There are two statements to deviate from the regular loop evaluation:

- break
- continue.

A break terminates the loop entirely, and continue ends only the current iteration and continues the loop with the next iteration, for instance:

```cpp
for (....; ....; ....) {
    ...
    if (dx == 0.0) continue;
    x += dx;
    ...
    if (r < eps) break;
    ...
}
```

In the example above we assumed that the remainder of the iteration is not needed when dx == 0.0. In some iterative computations it might be clear in the middle of an iteration (here when r < eps) that work is already done.

### 1.4.5 goto

All branches and loops are internally realized by jumps. C++ provides explicit jumps called goto. However:

> **Advice**
> Do not use goto! Never! Ever!

The applicability of goto is more restrictive in C++ than in C (e.g., we cannot jump over initializations); it still has the power to ruin the structure of our program.

## 1.5 Functions

Functions are important building blocks of C++ programs. The first example we have seen is the main function in the hello-world program. We will say a little more about main in Section 1.5.5.

The general form of a C++ function is

```cpp
[inline] return_type function_name (argument_list)
{
    body of the function
}
```

In this section, we discuss these components in more detail.

### 1.5.1 Arguments

C++ distinguishes two forms of passing arguments: by value and by reference.

#### 1.5.1.1 Call by Value

When we pass an argument to a function, it creates a copy by default. For instance, the following function increments x but not visibly to the outside world:

```cpp
void increment(int x)
{
    x++;
}

int main()
{
    int i = 4;
    increment(i);    // Does not increment i
    cout << "i is " << i << '\n';
}
```

The output is 4. The operation x++ within the increment function only increments a local copy of i but not i itself. This kind of argument transfer is referred to as Call-by-Value or Pass-by-Value.

#### 1.5.1.2 Call by Reference

To modify function parameters, we have to Pass the argument by Reference:

```cpp
void increment(int& x)
{
    x++;
}
```

Now, the variable itself is incremented and the output will be 5 as expected. We will discuss references in more detail in §1.8.4.

Temporary variables—like the result of an operation—cannot be passed by reference:

```cpp
increment(i + 9); // Error: temporary not referable
```

since we could not compute (i + 9)+ any way. In order to call such a function with some temporary value, we need to store it first in a variable and pass this variable to the function.

Larger data structures like vectors and matrices are almost always passed by reference to avoid expensive copy operations:

```cpp
double two_norm(vector& v) { ... }
```

An operation like a norm should not change its argument. But passing the vector by reference bears the risk of accidentally overwriting it. To make sure that our vector is not changed (and not copied either), we pass it as a constant reference:

```cpp
double two_norm(const vector& v) { ... }
```

If we tried to change v in this function the compiler would emit an error.

Both call-by-value and constant references ascertain that the argument is not altered but by different means:

- Arguments that are passed by value can be changed in the function since the function works with a copy.⁶
- With const references we work directly on the passed argument, but all operations that might change the argument are forbidden. In particular, const-reference arguments cannot appear on the left-hand side (LHS) of an assignment or be passed as non-const references to other functions (in fact, the LHS of an assignment is also a non-const reference).

In contrast to mutable⁷ references, constant ones allow for passing temporaries:

```cpp
alpha = two_norm(v + w);
```

This is admittedly not entirely consequential on the language design side, but it makes the life of programmers much easier.

#### 1.5.1.3 Defaults

If an argument usually has the same value, we can declare it with a default value. Say we implement a function that computes the n-th root and mostly the square root, then we can write

```cpp
double root(double x, int degree = 2) { ... }
```

