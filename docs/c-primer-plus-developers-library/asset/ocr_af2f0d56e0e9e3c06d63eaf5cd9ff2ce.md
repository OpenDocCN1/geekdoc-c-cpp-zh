It simply provides a comma-separated list of values (the *initialization list*) enclosed in braces. The spaces in the list are optional. If you don't initialize an array that's defined inside a function, the element values remain undefined. That means the element takes on whatever value previously resided at that location in memory.

Next, the program uses the array values in a few calculations. This part of the program looks cluttered with all the subscripts and brackets. The *for* loop, coming up in Chapter 5, “Loops and Relational Expressions,” provides a powerful way to deal with arrays and eliminates the need to write each index explicitly. For the time being, we'll stick to small arrays.

As you should recall, the `sizeof` operator returns the size, in bytes, of a type or data object. Note that if you use the `sizeof` operator with an array name, you get the number of bytes in the whole array. But if you use `sizeof` with an array element, you get the size, in bytes, of the element. This illustrates that *yams* is an array, but *yams[1]* is just an int.

# ## Initialization Rules for Arrays

C++ has several rules about initializing arrays. They restrict when you can do it, and they determine what happens if the number of array elements doesn't match the number of values in the initializer. Let's examine these rules.

You can use the initialization form *only* when defining the array. You cannot use it later, and you cannot assign one array wholesale to another:

```
```cpp
int cards[4] = {3, 6, 8, 10};        // okay
int hand[4];                          // okay
hand[4] = {5, 6, 7, 9};               // not allowed
hand = cards;                         // not allowed
```
```

However, you can use subscripts and assign values to the elements of an array individually.

When initializing an array, you can provide fewer values than array elements. For example, the following statement initializes only the first two elements of `hotelTips`:

```
```cpp
float hotelTips[5] = {5.0, 2.5};
```
```

If you partially initialize an array, the compiler sets the remaining elements to zero. Thus, it's easy to initialize all the elements of an array to zero—just explicitly initialize the first element to zero and then let the compiler initialize the remaining elements to zero:

```
```cpp
long totals[500] = {0};
```
```

Note that if you initialize to `{1}` instead of to `{0}`, just the first element is set to 1; the rest still get set to 0.

If you leave the square brackets (`[]`) empty when you initialize an array, the C++ compiler counts the elements for you. Suppose, for example, that you make this declaration:

```
```cpp
short things[] = {1, 5, 3, 8};
```
```

The compiler makes `things` an array of four elements.