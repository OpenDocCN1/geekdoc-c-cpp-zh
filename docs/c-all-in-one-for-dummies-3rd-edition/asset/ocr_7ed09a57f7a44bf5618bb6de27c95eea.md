![](bbox=[0.144, 0.143, 0.231, 0.206])

If you really have this kind of data structure, consider redesigning it. Any data stored like this would be downright confusing. And fortunately, the compiler will stop you from going totally overboard. Just for fun we tried this giant monster:

```
```c
int GiantMonster[18][16][10][16][15][17][12][14];
```
```

This is the error we got:

```
```text
error: size of array 'GiantMonster' is too large
```
```

(That would be 1,974,067,200 bytes: more than a gigabyte!)

# Initializing multidimensional arrays

Just as you can initialize a single-dimensional array by using braces and separating the elements by commas, you can initialize a multidimensional array with braces and commas and all that jazz, too. But to do this, you combine arrays inside arrays, as in this code:

```
```c
int Numbers[5][6] = {
    {1,2,3,4,5,6},
    {7,8,9,10,12},
    {13,14,15,16,17,18},
    {19,20,21,22,23,24},
    {25,26,27,28,29,30}
};
```
```

The hard part is remembering whether you put in five batches of six or six batches of five. Think of it like this: Each time you add another dimension, it goes inside the previous dimension. That is, you can write a single-dimensional array like this:

```
```c
int MoreNumbers[5] = {
    100,
    200,
    300,
    400,
    500,
};
```
```

Then, if you add a dimension to this array, each number in the initialization is replaced by an array initializer of the form {1,2,3,4,5,6}. Then you end up with a properly formatted multidimensional array.

# Passing multidimensional arrays

If you have to pass a multidimensional array to a function, things can get just a bit hairy. That’s because you don’t have as much freedom in leaving off the array sizes as you do with single-dimensional arrays. Suppose you have this function: