In the above example, we make an array of 4 floats. The value in the square brackets in the declaration lets us know that.

Later on subsequent lines, we access the values in the array, setting them or getting them, again with square brackets.

Hope this looks familiar from languages you already know!

# 6.2 Getting the Length of an Array

You can't...ish. C doesn't record this information³. You have to manage it separately in another variable.

When I say "can", I actually mean there are some circumstances where you can. There is a trick to get the number of elements in an array in the scope in which array is declared. But, generally speaking, this won't work the way you pass the array to a function.

Let's take a look at this. The basic idea is that you take the size of the array, and divide that by the size of each element to get the length. For example, if int/4 is 32 bytes, there must be room for 8 ints in there.

```
int x[12]; // 12 ints
```

```
printf("%zu\n", sizeof(x)); // 48 total bytes
printf("%zu\n", sizeof(int)); // 4 bytes per int
```

```
printf("%zu\n", sizeof(int)); // 48/4 = 12 ints!
```

If it's an array of chars, then sizeof is the number of elements, since sizeof(char) is defined to be 1. For anything else, you have to divide by the size of each element.

But this trick only works in the scope in which the array was defined. If you pass the array to a function, it doesn't work. If you make "big" in the function signature:

```
void foo(int x[12])\{
    printf("%zu\n", sizeof(x)); // 8! What happened to 48?
    printf("%zu\n", sizeof(int)); // 4 bytes per int
}
```

This is because when you "pass" arrays to functions, you're only passing a pointer to the first element, and that's what sizeof measures. More on this in the Passing Single Dimensional Arrays to Functions section, below.

One thing you can do with sizeof and arrays is get the size of an array of a fixed number of elements without declaring the array. This is like how you get the size of an int with sizeof(int).

For example, to see how many bytes would be needed for an array of 48 doubles, you can do this:

```
sizeof(double[48]);
```

# 6.3 Array Initializers

You can initialize an array with constants at ahead of time:

³Since arrays are just pointers to the first element of the array under the head, there's no additional information recording the length.
⁴Because you pass an array to a function, you're actually just passing a pointer to the first element of that array, not the "entire" array.