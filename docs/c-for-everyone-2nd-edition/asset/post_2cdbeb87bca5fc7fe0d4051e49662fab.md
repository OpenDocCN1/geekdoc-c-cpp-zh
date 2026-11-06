
| Expression | Value | Comment |
|---|---|---|
| Assume the following declarations: `int m = 10;` // Assumed to be at address 20300<br>`int n = 20;` // Assumed to be at address 20304<br>`int* p = &m;` |  |  |
| `p` | 20300 | The address of m. |
| `*p` | 10 | The value stored at that address. |
| `&n` | 20304 | The address of n. |
| `p = &n;` |  | Set p to the address of n. |
| `*p` | 20 | The value stored at the changed address. |
| `m = *p;` |  | Stores 20 into m. |
| `m = p;` | Error | m is an int value; p is an int* pointer. The types are not compatible. |
| `&10` | Error | You can only take the address of a variable. |
| `&p` | The address of p, perhaps 20308 | This is the location of a pointer variable, not the location of an integer. |
| `double x = 0;`<br>`p = &x;` | Error | p has type int*, &x has type double*. These types are incompatible. |

## 7.1.3 Initializing Pointers

With pointers, it is particularly important that you pay attention to proper initialization.

When you initialize a pointer, be sure that the pointer and the memory address have the same type. For example, the following initialization would be an error:

```cpp
int balance = 1000;
double* account_pointer = &balance; // Error!
```

The address &balance is a pointer to an int value, that is, an expression of type int*. It is never legal to initialize a double* pointer with an int*.

If you define a pointer variable without providing an initial value, the pointer contains a random address. Using that random address is an error. In practice, your program will likely crash or mysteriously misbehave if you use an uninitialized pointer:

It is an error to use an uninitialized pointer.

```cpp
double* account_pointer;
// Forgot to initialize
*account_pointer = 1000;
// NO! account_pointer contains an unpredictable value
```

The NULL pointer does not point to any object.

There is a special value, NULL, that you should use to indicate a pointer that doesn't point anywhere. If you define a pointer variable and are not ready to initialize it quite yet, set it to NULL.

```cpp
double* account_pointer = NULL;  // Will set later
```

You can later test whether the pointer is still NULL. If it is, don't use it.

```cpp
if (account_pointer != NULL) { cout << *account_pointer; }  // OK
```

Trying to access data through a NULL pointer is illegal, and it will cause your program to terminate.

The following program demonstrates the behavior of pointers. We execute the same withdrawal statement twice, but with different values for account_pointer. Each time, a different account is modified.

**ch07/accounts.cpp**

```cpp
#include <iostream>

using namespace std;

int main()
{
    double harrys_account = 0;
    double joint_account = 2000;
    double* account_pointer = &harrys_account;

    *account_pointer = 1000;  // Initial deposit

    *account_pointer = *account_pointer - 100;  // Withdraw $100
    cout << "Balance: " << *account_pointer << endl;  // Print balance

    // Change the pointer value
    account_pointer = &joint_account;

    // The same statements affect a different account
    *account_pointer = *account_pointer - 100;  // Withdraw $100
    cout << "Balance: " << *account_pointer << endl;  // Print balance

    return 0;
}
```

**Program Run**

```
Balance: 900
Balance: 1900
```

![](img/23fb3582e93ebc95909e1de029c3d388_339_0.png)

- 1. Consider this set of statements. What is printed?

```cpp
int a = 1;
int b = 2;
int* p = &a;
cout << *p << endl;
p = &b;
cout << *p << endl;
```

- 2. Consider this set of statements. What is printed?

```cpp
int a = 1;
int b = 2;
```

**Table 2** Arrays and Pointers

| Expression | Value | Comment |
|---|---|---|
| `a` | 20300 | The starting address of the array, here assumed to be 20300. |
| `*a` | 0 | The value stored at that address. (The array contains values 0, 1, 4, 9, ...) |
| `a + 1` | 20308 | The address of the next double value in the array. A double occupies 8 bytes. |
| `a + 3` | 20324 | The address of the element with index 3, obtained by skipping past 3 × 8 bytes. |
| `*(a + 3)` | 9 | The value stored at address 20324. |
| `a[3]` | 9 | The same as `*(a + 3)` by array/pointer duality. |
| `*a + 3` | 3 | The sum of `*a` and 3. Since there are no parentheses, the `*` refers only to `a`. |
| `&a[3]` | 20324 | The address of the element with index 3, the same as `a + 3`. |

readers the illusion that an entire array is passed to the function, but in fact the function receives only the starting address for the array.

Now consider this statement in the body of the function:

```cpp
total = total + a[i];
```

The C++ compiler considers `a` to be a *pointer*, not an array. The expression `a[i]` is syntactic sugar for `*(a + i)`. That expression denotes the storage location that is `i` elements away from the address stored in the variable `a`. Figure 4 shows how `a[i]` is accessed when `i` is 3.

You can now understand why it is always necessary to pass the size of the array. The function receives a single memory address, which tells it where the array starts. That memory address enables the function to locate the values in the array. But the function also needs to know where to stop.

![](img/23fb3582e93ebc95909e1de029c3d388_344_0.png)

For Self Checks 6–9, draw the array and pointer as in Figure 3. Assume a starting address (20300 will work fine), and assume that each int value occupies 4 bytes.

- 6. What is the contents of the array after these statements?

```cpp
int a[] = { 2, 3, 5 };
int* p = a;
p++;
*p = 0;
```

- 7. What is the contents of the array after these statements?

```cpp
int a[] = { 2, 3, 5 };
int* p = a + 1;
*(p + 1) = 0;
```

- 8. What is the contents of the array after these statements?

```cpp
int a[] = { 2, 3, 5 };
int* p = a;
int* q = a + 2;
p++;
q--;
*p = *q;
```

- 9. What do the following statements print?

```cpp
int a[] = { 2, 3, 5 };
cout << *(a + 2) << " ";
cout << *(a + 2) << endl;
```

- 10. In Chapter 6, we defined a function

```cpp
void squares(int n, int result[])
```

Declare the parameter variable using pointer notation.

**Practice It** Now you can try these exercises at the end of the chapter: R7.7, R7.8, P7.4.

### Special Topic 7.2

![](img/23fb3582e93ebc95909e1de029c3d388_345_0.png)

### Using a Pointer to Step Through an Array

Consider again the sum function of Section 7.2.3. Now that you know that the first parameter variable of the sum function is a pointer, you can implement the function in a slightly different way. Rather than incrementing an integer index, you can increment a pointer variable to visit all array elements in turn:

```cpp
double sum(double* a, int size)
{
    double total = 0;
    double* p = a; // p starts at the beginning of the array
    for (int i = 0; i < size; i++)
    {
        total = total + *p; // Add the value to which p points
        p++; // Advance p to the next array element
    }
    return total;
}
```

Initially, the pointer p points to the element a[0]. The increment

```cpp
p++;
```

moves it to point to the next element (see Figure 5).

It is a tiny bit more efficient to use and increment a pointer than to access an array element as a[i]. For this reason, some programmers routinely use pointers instead of indexes to access array elements.

![](img/23fb3582e93ebc95909e1de029c3d388_345_1.png)

**Figure 5** A Pointer Variable Traversing the Elements of an Array

### Programming Tip 7.2

### Program Clearly, Not Cleverly

![](img/23fb3582e93ebc95909e1de029c3d388_346_0.png)

Some programmers take great pride in minimizing the number of instructions, even if the resulting code is hard to understand. For example, here is a legal implementation of the sum function:

```cpp
double sum(double* a, int size)
{
    double total = 0;
    while (size-- > 0) // Loop size times
    {
        total = total + *a++; // Add the value to which a points; increment a
    }
    return total;
}
```

This implementation uses two tricks. First, the function parameter variables a and size are variables, and it is legal to modify them. Moreover, the expressions size-- and a++ mean “decrement or increment the variable and return the old value”. In other words, the expression

```cpp
size-- > 0
```

combines two tasks: to decrement size, and to test whether size was positive before the decrement. Similarly, the expression

```cpp
*a++
```

increments the pointer to the next element, and it returns the element to which it pointed before the increment.

Please do not use this programming style. Your job as a programmer is not to dazzle other programmers with your cleverness, but to write code that is easy to understand and maintain.

### Common Error 7.2

### Returning a Pointer to a Local Variable

![](img/23fb3582e93ebc95909e1de029c3d388_346_1.png)

Consider this function that tries to return a pointer to an array containing two elements, the first and the last values of an array:

```cpp
double* firstlast(double a[], int size)
{
    double result[2];
    result[0] = a[0];
    result[1] = a[size - 1];
    return result; // Error!
}
```

The function returns a pointer to the starting element of the result array. However, that array is a local variable of the firstlast function. The local variable no longer exists when the function exits. Its contents will soon be overwritten by other function calls.

You can solve this problem by passing an array to hold the answer:

```cpp
void firstlast(const double a[], int size, double result[])
{
    result[0] = a[0];
    result[1] = a[size - 1];
}
```

Then it is the responsibility of the caller to allocate an array to hold the result.
