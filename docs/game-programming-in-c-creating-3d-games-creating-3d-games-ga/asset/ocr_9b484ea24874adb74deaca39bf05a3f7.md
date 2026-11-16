Dereferencing a null pointer crashes the program. The error message varies depending on the operating system, but typically “access violation” or “segmentation fault” errors occur when dereferencing a null pointer.

# Arrays

An **array** is a collection of multiple elements of the same type. The following code declares an array of 10 integers called `a` and then sets the first element in the array (index 0) to 50:

```
int a[10];
a[0] = 50;
```

By default, the elements in an array are uninitialized. While you could manually initialize each element in an array, it’s more convenient to use either the initializer syntax or a loop. The initializer syntax uses braces, like this:

```
int fib[5] = { 0, 1, 1, 2, 3 };
```

Alternatively, you could use a loop. The following initializes each of the 50 elements in `array` to 0:

```
int array[50];
```