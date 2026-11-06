
![](img/5e58fb4c840712efd6ed6fa82bb97f57_351_0.png)

This array can hold strings with a length of at most 39, because one character is required for the null terminator.

Now copy the first name, using `strncpy`:

```cpp
strncpy(name, first, NAME_SIZE - 1);
```

You must be careful not to overrun the target array. It is unlikely that a first name is longer than 39 characters, but a hacker could supply a longer input in order to overwrite memory.

Now, if there is still room, add a space and the last name, again being careful not to overrun the array boundaries.

```cpp
int length = strlen(name);
if (length < NAME_SIZE - 1)
{
    strcat(name, " ");
    int n = NAME_SIZE - 2 - length; // Leave room for space, null terminator
    if (n > 0)
    {
        strncpy(name, last, n);
    }
}
```

As you can see, the C string code is over three times as long as the code using C++ strings, and it is not as capable—if the target array is not long enough to hold the result, it is truncated.

### Table 4 C String Functions

In this table, s and t are character arrays; n is an integer.

| Function | Description |
|---|---|
| `strlen(s)` | Returns the length of s. |
| `strcpy(t, s)` | Copies the characters from s into t. |
| `strncpy(t, s, n)` | Copies at most n characters from s into t. |
| `strcat(t, s)` | Appends the characters from s after the end of the characters in t. |
| `strncat(t, s, n)` | Appends at most n characters from s after the end of the characters in t. |
| `strcmp(s, t)` | Returns 0 if s and t have the same contents, a negative integer if s comes before t in lexicographic order, a positive integer otherwise. |

After you delete a memory block, you can no longer use it. The storage space may already be used elsewhere.

```cpp
delete[] account_array;
account_array[0] = 1000; // NO! You no longer own the memory of account_array
```

Heap arrays have one significant advantage over array variables. If you declare an array variable, you must specify a fixed array size when you compile the program. But when you allocate an array on the heap, you can choose the size at run time.

Moreover, if you later need more elements, you are not stuck. You can allocate a bigger heap array, copy the elements from the smaller array into the bigger array, and delete the smaller array (see Figure 7):

```cpp
double* bigger_array = new double[2 * n];
for (int i = 0; i < n; i++)
{
    bigger_array[i] = account_array[i];
}
delete[] account_array;
account_array = bigger_array;
n = 2 * n;
```

This is exactly what a vector does behind the scenes.

Heap allocation is a powerful feature, but you must be very careful to follow all rules precisely:

- Every call to `new` must be matched by exactly one call to `delete`.
- Use `delete[]` to delete arrays.
- Don’t access a memory block after it has been deleted.

If you don’t follow these rules, your program can crash or run unpredictably. Table 5 shows common errors.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_353_0.png)

*Be sure to recycle any heap memory that your program no longer needs.*

![](img/5e58fb4c840712efd6ed6fa82bb97f57_353_1.png)

**Figure 7** Growing a Dynamic Array

### Table 5 Common Memory Allocation Errors

| Statements | Error |
|---|---|
| `int* p;`<br>`*p = 5;`<br>`delete p;` | There is no call to `new int`. |
| `int* p = new int;`<br>`*p = 5;`<br>`p = new int;` | The first allocated memory block was never deleted. |
| `int* p = new int[10];`<br>`*p = 5;`<br>`delete p;` | The `delete[]` operator should have been used. |
| `int* p = new int[10];`<br>`int* q = p;`<br>`q[0] = 5;`<br>`delete p;`<br>`delete q;` | The same memory block was deleted twice. |
| `int n = 4;`<br>`int* p = &n;`<br>`*p = 5;`<br>`delete p;` | You can only delete memory blocks that you obtained from calling `new`. |

![](img/5e58fb4c840712efd6ed6fa82bb97f57_354_0.png)

- 16. What does this statement sequence print?

  ```cpp
  int* p = new int;
  *p = 3;
  cout << *p << endl;
  delete p;
  ```

- 17. What does this statement sequence print?

  ```cpp
  int* p = new int[10];
  for (int i = 0; i < 10; i++) { p[i] = i * i; }
  cout << p << " " << (p + 1) << " " << p[2] << endl;
  delete[] p;
  ```

- 18. What is wrong with this sequence of statements?

  ```cpp
  int* p = new int[10];
  p[10] = 5;
  delete[] p;
  ```

- 19. Consider this function

  ```cpp
  int* grow(int a[], int size)
  {
      int* result = new int[2 * size];
      for (int i = 0; i < size; i++) { result[i] = a[i]; }
      for (int i = size; i < 2 * size; i++) { result[i] = 0; }
      return result;
  }
  ```

  What is the contents of the array to which `p` points after the following statements?

  ```cpp
  int primes[] = { 2, 3, 5, 7, 11 };
  int* p = grow(primes, 5);
  ```

- 20. Consider the grow function of Self Check 19. What must its caller remember to do?

**Practice It** Now you can try these exercises at the end of the chapter: R7.19, R7.21, P7.10.

### Common Error 7.3 Dangling Pointers

A very common pointer error is to use a pointer that points to memory that has already been deleted. Such a pointer is called a dangling pointer. The freed memory will be reused for other purposes, you can create real damage by using a dangling pointer. Consider this example:

> Using a dangling pointer (a pointer that points to memory that has been deleted) is a serious programming error.

```cpp
int* values = new int[n];
// Process values
delete[] values;
// Some other work
values[0] = 42;
```

This code will compile since the compiler does not track whether a pointer points to a valid memory location. However, the program may run with unpredictable results. If the program calls the new operator anywhere after deleting values, that call may allocate the same memory again. Now some other part of your program accesses the memory to which values points, and that program part will malfunction when you overwrite the memory. This can happen even if you don't see any call to new—such calls may occur in library functions.

Never use a pointer that has been deleted. Some programmers take the precaution of setting all deleted pointers to NULL:

```cpp
delete[] values;
values = NULL;
```

This is not perfect protection—you might have saved values into another pointer variable—but it is a reasonable precaution.

### Common Error 7.4 Memory Leaks

Another very common pointer error is to allocate memory on the heap and never deallocate it. A memory block that is never deallocated is called a **memory leak**.

If you allocate a few small blocks of memory and forget to deallocate them, this is not a huge problem. When the program exits, all allocated memory is returned to the operating system.

But if your program runs for a long time, or if it allocates lots of memory (perhaps in a loop), then it can run out of memory. Memory exhaustion will cause your program to crash. In extreme cases, the computer may freeze up if your program exhausted all available memory. Avoiding memory leaks is particularly important in programs that need to run for months or years, without restarting, and in programs that run on resource-constrained devices such as cell phones.

> Every call to new should have a matching call to delete.

Even if you write short-lived programs, you should make it a habit to avoid memory leaks. Make sure that every call to the new operator has a corresponding call to the delete operator.

## 7.5 Arrays and Vectors of Pointers

When you have a sequence of pointers, you can place them into an array or vector. An array and a vector of ten `int*` pointers are defined as

```cpp
int* pointer_array[10];
vector<int*> pointer_vector(10);
```

The expression `pointer_array[i]` or `pointer_vector[i]` denotes the pointer with index i in the sequence.

One application of such pointer sequences are two-dimensional arrays in which each row has a different length, such as the triangular array shown in Figure 8.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_356_0.png)

**Figure 8** A Triangular Array

In this situation, it would not be very efficient to use a two-dimensional array, because almost half of the elements would be wasted.

We will develop a program that uses such array for simulating a *Galton board* (Figure 9). A Galton board consists of a pyramidal arrangement of pegs, and a row of bins at the bottom. Balls are dropped onto the top peg and travel toward the bins. At each peg, there is a 50 percent chance of moving left or right. The balls in the bins approximate a bell-curve distribution.

The Galton board can only show the balls in the bins, but we can do better by keeping a counter for each peg, incrementing it as a ball travels past it.

We will simulate a board with ten rows of pegs. Each row requires an array of counters.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_356_1.png)

**Figure 9** A Galton Board
