of g_moon’s const status, so C++ prohibits you from assigning the address of a const to a non-const pointer. (If you are really desperate, you can use a type cast to override the restriction; see Chapter 15, “Friends, Exceptions, and More,” for a discussion of the `const_cast` operator.)

The situation becomes a bit more complex if you have pointers to pointers. As you saw earlier, assigning a non-const pointer to a const pointer is okay, provided that you’re dealing with just one level of indirection:

```
```cpp
int age = 39;        // age++ is a valid operation
int * pd = &age;     // *pd = 41 is a valid operation
const int * pt = pd; // *pt = 42 is an invalid operation
```
```

But pointer assignments that mix const and non-const in this manner are no longer safe when you go to two levels of indirection. If mixing const and non-const were allowed, you could do something like this:

```
```cpp
const int **pp2;
int *p1;
const int n = 13;
pp2 = &p1; // not allowed, but suppose it were
*pp2 = &n; // valid, both const, but sets p1 to point at n
*p1 = 10;  // valid, but changes const n
```
```

Here the code assigns a non-const address (`&p1`) to a const pointer (`pp2`), and that allows p1 to be used to alter const data. So the rule that you can assign a non-const address or pointer to a const pointer works only if there is just one level of indirection—for example, if the pointer points to a fundamental data type.

> **Note**
> 
> You can assign the address of either const data or non-const data to a pointer-to-const, provided that the data type is not itself a pointer, but you can assign the address of non-const data only to a non-const pointer.

Suppose you have an array of const data:

```
```cpp
const int months[12] = {31,28,31,30,31,30, 31, 31,30,31,30,31};
```
```

The prohibition against assigning the address of a constant array means that you cannot pass the array name as an argument to a function by using a non-constant formal argument:

```
```cpp
int sum(int arr[], int n); // should have been const int arr[]
...
int j = sum(months, 12);   // not allowed
```
```

This function call attempts to assign a const pointer (`months`) to a non-const pointer (`arr`), and the compiler disallows the function call.