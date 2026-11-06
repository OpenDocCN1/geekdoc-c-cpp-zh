
## CHAPTER SUMMARY

## Define and use pointer variables.

- A pointer denotes the location of a variable in memory.
- The type `T*` denotes a pointer to a variable of type `T`.
- The `&` operator yields the location of a variable.
- The `*` operator accesses the variable to which a pointer points.
- It is an error to use an uninitialized pointer.
- The `NULL` pointer does not point to any object.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_366_0.png)

## Understand the relationship between arrays and pointers in C++.

- The name of an array variable is a pointer to the starting element of the array.
- Pointer arithmetic means adding an integer offset to an array pointer, yielding a pointer that skips past the given number of elements.
- The array/pointer duality law states that `a[n]` is identical to `*(a + n)`, where `a` is a pointer into an array and `n` is an integer offset.
- When passing an array to a function, only the starting address is passed.

## Use C++ string objects with functions that process character arrays.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_366_1.png)

- A value of type `char` denotes an individual character. Character literals are enclosed in single quotes.
- A literal string, enclosed in double quotes, is an array of `char` values with a zero terminator.
- Many library functions use pointers of type `char*`.
- The `c_str` member function yields a `char*` pointer from a `string` object.
- You can initialize C++ `string` variables with C strings.
- You can access characters in a C++ `string` object with the `[]` operator.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_366_2.png)

## Allocate and deallocate memory in programs whose memory requirements aren't known until run time.

- Use dynamic memory allocation if you do not know in advance how many values you need.
- The `new` operator allocates memory from the heap.
- You must reclaim dynamically allocated objects with the `delete` or `delete[]` operator.
- Using a dangling pointer, a pointer that points to memory that has been deleted, is a serious programming error.
- Every call to `new` should have a matching call to `delete`.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_366_3.png)

## Work with arrays and vectors of pointers.

## Draw diagrams for visualizing pointers and the data to which they point.

- Draw the data that is being processed, then draw the pointer variables. When drawing the pointer arrows, illustrate a typical situation.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_367_0.png)

## Use structures to aggregate data items and work with pointers to structures.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_367_1.png)

- A structure combines member values into a single value.
- You use the dot notation to access members of a structure.
- Use the `->` operator to access a structure member through a pointer.

## REVIEW EXERCISES

**R7.1** Trace the following code. Assume that `a` and `b` are stored at 20300 and 20308. Your trace table should have entries for `a`, `b`, and `p`.

```cpp
double a = 1000;
double b = 2000;
double* p = &a;
*p = 3000;
p = &b;
a = *p * 2;
```

**R7.2** Trace the following code. Assume that `a` and `b` are stored at 20300 and 20308. Your trace table should have entries for `a`, `b`, `p`, and `q`.

```cpp
double a = 1000;
double b = 2000;
double* p = &a;
double* q = &b;
*p = *q;
p = q;
*p = 3000;
```

**R7.3** What does the following code print?

```cpp
double a = 1000;
double b = 2000;
double* p = &a;
double* q = p;
b = *q;
p = &b;
a = *p + *q;
cout << a << " " << b << endl;
```

**R7.4** Explain the mistakes in the following code. Not all lines contain mistakes. Each line depends on the lines preceding it.

```cpp
1   double a = 1000;
2   double* p = a;
3   int* p = &a;
4   double* q;
5   *q = 2000;
```

```c
int* r = NULL;
*r == 3000;
```

**R7.5** Suppose that a system allows the use of any string as a password, even the empty string. However, when a user connects to the system for the first time, no password has been assigned. Describe how you can use a `string*` variable and the `NULL` pointer to distinguish unassigned passwords from empty ones.

**R7.6** Given the definitions

```cpp
double primes[] = { 2, 3, 5, 7, 11, 13 };
double* p = primes + 3;
```

draw a diagram that explains the meanings of the following expressions:

- a. `primes[1]`
- b. `primes + 1`
- c. `*(primes + 1)`
- d. `p[1]`
- e. `p + 1`

**R7.7** Suppose the array `primes`, defined as

```cpp
double primes[] = { 2, 3, 5, 7, 11, 13 };
```

starts at memory location 20300. What are the values of

- a. `primes`
- b. `*primes`
- c. `primes + 4`
- d. `*(primes + 4)`
- e. `primes[4]`
- f. `&primes[4]`

**R7.8** Suppose the array `primes` is defined as

```cpp
double primes[] = { 2, 3, 5, 7, 11, 13 };
```

Consider the `sum` function discussed in Section 7.2.3. What are the values of

- a. `sum(primes, 6);`
- b. `sum(primes, 4);`
- c. `sum(primes + 2, 4);`
- d. `sum(primes, 0);`
- e. `sum(NULL, 4);`

**R7.9** Suppose the array `primes`, defined as

```cpp
double primes[] = { 2, 3, 5, 7, 11, 13 };
```

starts at memory location 20300. Trace the function call `sum(primes, 4)`, using the definition of `sum` from Special Topic 7.2 on page 318. In your trace table, show the values for `a`, `size`, `total`, `p`, and `i`.

**R7.10** Pointers are addresses and have a numerical value. You can print out the value of a pointer as `cout << (unsigned) (p)`. Write a program to compare `p`, `p + 1`, `q`, and `q + 1`, where `p` is an `int*` and `q` is a `double*`. Explain the results.

**R7.11** A pointer variable can contain a pointer to a single variable, a pointer to an array, `NULL`, or a random value. Write code that creates and sets four pointer variables `a`, `b`, `c`, and `d` to show each of these possibilities.

**R7.12** Implement a function `firstLast` that obtains the first and last values in an array of integers and stores the result in an array argument.

**R7.13** Explain the meanings of the following expressions:

- a. `"Harry" + 1`
- b. `*("Harry" + 2)`
- c. `"Harry"[3]`
- d. `4["Harry"]`

**R7.14** What is the difference between the following two variable definitions?

- a. `char a[6] = "Hello";`
- b. `char* b = "Hello";`

**R7.15** What is the difference between the following three variable definitions?

- a. `char* p = NULL;`
- b. `char* q = "";`
- c. `char r[1] = { '\0' };`

**R7.16** Consider this program segment:

```cpp
char a[] = "Mary had a little lamb";
char* p = a;
int count = 0;
while (*p != '\0')
{
    count++;
    while (*p != ' ' && *p != '\0') { p++; }
    while (*p == ' ') { p++; }
}
```

What is the value of `count` at the end of the outer `while` loop?

**R7.17** Consider the following code that repeats a C++ string three times.

```cpp
string a = "Hello";
string b = a + a + a;
```

Suppose `s` is a C string, and `t` is declared as

```cpp
char t[100];
```

Write the equivalent code for C strings that stores the threefold repetition of `s`, or as much of it as will fit, into `t`.

**R7.18** Which of the following assignments are legal in C++?

```cpp
void f(int p[])
{
    int* q;
    const int* r;
    int s[10];
    p = q;  // ①
    p = r;  // ②
    p = s;  // ③
    q = p;  // ④
    q = r;  // ⑤
    q = s;  // ⑥
    r = p;  // ⑦
    r = q;
    r = s;
    s = p;
    s = q;
    s = r;
}
```

**R7.19** What happens if you forget to delete an object that you obtained from the heap? What happens if you delete it twice?

**R7.20** Write a program that accesses a deleted pointer, an uninitialized pointer, and a `NULL` pointer. What happens when you run your program?

**R7.21** Find the mistakes in the following code. Not all lines contain mistakes. Each line depends on the lines preceding it. Watch out for uninitialized pointers, `NULL` pointers, pointers to deleted objects, and confusing pointers with objects.

```cpp
int* p = new int;
p = 5;
*p = *p + 5;
string s = "Harry";
s = "Sally";
delete &s;
int* a = new int[10];
*a = 5;
a[10] = 5;
delete a;
int* q;
*q = 5;
q = p;
delete q;
delete p;
```

**R7.22** How do you define a triangular two-dimensional array using just vectors, not arrays or pointers?

**R7.23** Rewrite the statements in Section 7.7.3 so that the street address and employee structures are allocated on the heap.

**R7.24** Design a structure type `Person` that contains the name of a person and pointers to the person’s father and mother. Write statements that define a structure value for yourself and your parents, correctly establishing the pointer links. Use `NULL` for your parents’ parents.

**R7.25** Draw a figure showing the result of a call to the maximum function in Exercise P7.4.

**R7.26** Draw a figure showing the pointers in the `lines` array in Exercise P7.13 after reading a few lines.

**R7.27** Section 7.6 described an arrangement where each item had a pointer to the user who had checked out the item. This makes it difficult to find out the items that a particular user checked out. To solve this problem, have an array of strings `user_names` and a parallel array `loaned_items`. `loaned_items[i]` points to an array of `char*` pointers, each of which is a name of an item that the user checked out. If the user didn’t check out any items, then `loaned_items[i]` is `NULL`. Draw a picture of this arrangement.
