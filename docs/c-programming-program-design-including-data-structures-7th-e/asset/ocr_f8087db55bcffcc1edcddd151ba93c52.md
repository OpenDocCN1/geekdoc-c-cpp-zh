```
```cpp
for (dataType identifier : arrayName)
    statements
```
```

where `identifier` is a variable and the data type of `identifier` is the same as the data type of the array elements. This form of the `for` loop is called a **range-based for** loop.

For example, suppose you have the following declarations:

```
```cpp
double list[25];
double sum;
```
```

The following code finds the sum of the elements of `list`:

```
```cpp
sum = 0;                  //Line 1

for (double num : list)   //Line 2
    sum = sum + num;      //Line 3
```
```

The `for` statement in Line 2 is read as “for each `num` in `list`.” The variable `num` is initialized to `list[0]`. In the next iteration, the value of `num` is `list[1]`, and so on. It follows that the variable `num` is assigned the contents of each array element, *not* its index value, and that the loop by default starts at 0 and traverses the entire array.

You can also use `auto` declaration in a range-based loop to process the elements of an array. For example, using the range-based `for` loop, the `for` loop to find the largest element in the array `list` can be written as:

```
```cpp
for (auto num : list)
{
    if (max < num)
        max = num;
}
```
```

Suppose that `list` is declared as a formal parameter to a function to process an array. To be specific, consider the following declaration:

```
```cpp
void doSomething(int list[])
{
    //code to process list
}
```
```

Then in the definition of the function `doSomething`, a range-based `for` loop cannot be applied to `list`. Recall that in C++, arrays are parameters passed by reference. Therefore, when the function `doSomething` is called, `list` gets the base address of the actual parameters, that is, the base address of the actual parameter is copied into the memory space `list`. So a formal parameter `list` is, in fact, *not* an array, it is a variable to store the address of a memory location, so it has no first (that is, `list[0]`) and last elements.

# ## C-Strings (Character Arrays)

Until now, we have avoided discussing character arrays for a simple reason: Character arrays are of special interest, and you process them differently than you process other arrays. C++ provides many (predefined) functions that you can use with character arrays.