Let's see an example of memory leak:

```
void f()
{
    int *ptr = new int[10000];
    ptr = new int[200];
    ...
    delete[] ptr;
}
```

In this example we forget to release the first memory block before the new allocation. This is a memory leak, which occurs every time f() is called.
Another common example of memory leak is when we allocate memory in one place and forget to release it in another place where it is supposed to do so. For example:

```
double* f(int size)
{
    return new double[size];
}
```

```
void g()
{
    double* p = f(10000);
    /* Do some stuff with p, but then we forget to release the memory allocated in f(). */
}
```

When g ends, the local variable p is automatically destroyed, the memory it points to is not automatically released. We have to do it explicitly by calling delete[] p. As you guess, in complex and large programs when memory is allocated in one part of the program and released in another part, the programmer may forget to do so and create a memory leak that is difficult to sort. To avoid such leaks, we'll see in Chapter 25, a safer practice is the use of smart pointers. That is, if we use a smart pointer in place of p the memory will be released automatically.

Another usual of memory leak occurs when we assign one pointer to another, but we forget to release the memory to which the original pointed. For example, find the errors in the following program and fix them:

```
#include <iostream> // Example 14.6
int main()
{
    char *p1, *p2;

np1 = new char[10];
    p2 = new char[10];
    p1 = p2;
    delete[] p1;

    p2[0] = 'a';
    delete[] p2;
    return 0;
}
```