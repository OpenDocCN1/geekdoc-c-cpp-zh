# Chapter 23. Pointers III: Pointers to Pointers and More

Now that we know how to declare a variable, how do we know what to assign to it? How do we get the address of a function?

Turns there's a shortcut just like getting a pointer to an array: you can just refer to the bare function without parents. (You can put an & in front of this, but it's unnecessary and not idiomatic.)

Once you have a pointer to a function, you can just call it by adding parents and an argument list.

Let's do a simple example where I effectively make an alias for a function by setting a pointer to it. Then we'll call it.

This code prints 3490:

```
#include <stdio.h>

void print_int(int n) {
    printf("%d\n", n);
}

int main() {
    // Assign p to print_int:
    void (*p)(int) = print_int;
    p(3490); // Call print_int via the pointer
}
```

Notice how the type of p returns the return value and parameter types of print_int. It has to, or else C will complain about incompatible pointer types.

One more example shows how we might pass a pointer to a function as an argument to another function. We'll write a function that takes a couple integer arguments, plus a pointer to a function that operates on those two arguments. Then it prints the result.

```
#include <stdio.h>

int add(int a
```