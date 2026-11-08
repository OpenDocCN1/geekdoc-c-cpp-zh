# # Function Overloading

You’ll often find that you need two or more functions that do essentially the same thing, but with parameters of different types. The largest() and smallest() functions in Ex8_13.cpp are likely candidates. You would want these operations to work with arrays of different types such as int[], double[], float[], or even string[]. Ideally, all such functions would have the same name, largest() or smallest(). Function overloading makes that possible.

Function overloading allows several functions in a program to have the same name as long as they all have a parameter list that is different from each other. You learned earlier in this chapter that the compiler identifies a function by its signature, which is a combination of the function name and the parameter list. Overloaded functions have the same name, so the signature of each overloaded function must be differentiated by the parameter list alone. That allows the compiler to select the correct function for each function call based on the argument list. Two functions with the same name are different if at least one of the following is true:

+   - The functions have different numbers of parameters.
+   - At least one pair of corresponding parameters is of different types.

> **Note**  The return type of a function is not part of the function’s signature. To decide which function overload to use, the compiler looks only at the number and types of the function parameters and arguments. If you declare two functions with the same name and parameter list but with a different return type, your program will fail to compile.

Here’s an example that uses overloaded versions of the largest() function:

```
```cpp
// Ex8_14.cpp
// Overloading a function
import <iostream>;
import <string>;
import <vector>;

// Function prototypes
double largest(const double data[], size_t count);
double largest(const std::vector<double>& data);
int largest(const std::vector<int>& data);
std::string largest(const std::vector<std::string>& words);
// int largest(const std::vector<std::string>& words);
             /* Above function overload would not compile: overloaded functions
                must differ in more than just their return type! */

int main()
{
    double array[] {1.5, 44.6, 13.7, 21.2, 6.7};
    std::vector<int> numbers {15, 44, 13, 21, 16, 8, 5, 2};
    std::vector<double> data{3.5, 5, 6, -1.2, 8.7, 6.4};
    std::vector<std::string> names {"Charles Dickens", "Emily Bronte",
                                    "Jane Austen", "Henry James", "Arthur Miller"};
    std::cout << "The largest of array is " << largest(array, std::size(array))
              << std::endl;
}
```
```