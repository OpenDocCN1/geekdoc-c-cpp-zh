```
```cpp
std::cout << "Pick a lucky star! Enter a number between 1 and "
          << std::size(stars) << ": ";
std::cin >> choice;

if (choice >= 1 && choice <= std::size(stars))
{
    std::cout << "Your lucky star is " << stars[choice - 1] << std::endl;
}
else
{
    std::cout << "Sorry, you haven't got a lucky star." << std::endl;
}
```
```

This is some typical output from this program:

```
Pick a lucky star! Enter a number between 1 and 8: 6
Your lucky star is Mae West
```

Apart from its incredible inherent entertainment value, the main point of interest in the example is the definition of the array, stars. It’s a two-dimensional array of char elements, which can hold multiple strings, each of which can contain up to max_length characters, including the terminating null that’s automatically added by the compiler. The initializing strings for the array are enclosed between braces and separated by commas. Because the size of the first array dimension is omitted, the compiler creates the array with the number of rows necessary to accommodate all the initializing strings. As you saw earlier, you can omit the size of only the first dimension; you must specify the sizes of any other dimensions that are required.

The if statement arranges for the output to be displayed. Its condition checks that the integer that was entered is within range before attempting to display a name. When you need to reference a string for output, you only need to specify the first index value. A single index selects a particular 80-element subarray, and because this contains a string, the operation will output the contents of each element up to the terminating null character. The index is specified as choice-1 because the choice values start from 1, whereas the index values need to start from 0. This is quite a common idiom when you’re programming with arrays.

# Allocating an Array at Runtime

The C++ standard does not permit an array dimension to be specified at runtime. That is, the array dimension must be a constant expression that can be evaluated by the compiler. However, some current C++ compilers do allow setting variable array dimensions at runtime because the C standard permits this, and a C++ compiler will typically compile C code too.

These so-called variable-length arrays can be a useful feature, so in case your compiler supports this, we’ll show how it works with an example. Keep in mind, though, that this is not strictly in conformance with the C++ language standard. Suppose you want to calculate the average height for a group of people, and you want to accommodate as many people as the user wants to enter heights for. As long as the user can input the number of heights to be processed, you can create an array that is an exact fit for the data that will be entered, like this:

```
```cpp
size_t count {};
std::cout << "How many heights will you enter? ";
std::cin >> count;
int height[count];              // Create the array of count elements
```
```