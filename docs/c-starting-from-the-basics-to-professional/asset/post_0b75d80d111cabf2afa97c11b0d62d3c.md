
the argument types. If you specify a function argument of a type that doesn't correspond to the parameter type, then the compiler inserts an implicit conversion of the argument to the type of the parameter where possible. The rules for automatic conversions of this kind are the same as those for automatic conversions in an assignment statement. If an automatic conversion is not possible, you'll get an error message from the compiler. If such implicit conversions result in potential loss of precision, compilers generally issue a warning. Examples of such narrowing conversions are conversions from long to int, double to float, or int to float (see also Chapter 2).

There are two mechanisms by which arguments are passed to functions, *pass-by-value* and *pass-by-reference*. We'll explain the pass-by-value mechanism first.

## Pass-by-Value

With the pass-by-value mechanism, the values of variables or constants you specify as arguments are not passed to a function at all. Instead, copies of the arguments are created, and these copies are transferred to the function. This is illustrated in Figure 8-2, using the power() function again.

```cpp
double value {20.0};
int index {3};
double result {power(value, index)};
```

![](img/020c376b6cc4874983a4344f51a256de_280_0.png)

*Figure 8-2. The pass-by-value mechanism for arguments to a function*

Each time you call the power() function, the compiler arranges for copies of the arguments to be stored in a temporary location in the call stack. During execution, all references to the function parameters in the code are mapped to these temporary copies of the arguments. When execution of the function ends, the copies of the arguments are discarded.

We can demonstrate the effects of this with a simple example. The following calls a function that attempts to modify one of its arguments, and of course, it fails miserably:

```cpp
// Ex8_03.cpp
// Failing to modify the original value of a function argument
import <iostream>;

double changeIt(double value_to_be_changed);    // Function prototype

int main()
{
    double it {5.0};
    double result {changeIt(it)};

    std::cout << "After function execution, it = " << it
              << "\nResult returned is " << result << std::endl;
}

// Function that attempts to modify an argument and return it
double changeIt(double it)
{
    it += 10.0;                    // This modifies the copy
    std::cout << "Within function, it = " << it << std::endl;
    return it;
}
```

This example produces the following output:

```text
Within function, it = 15
After function execution, it = 5
Result returned is 15
```

The output shows that adding 10 to it in the changeIt() function has no effect on the variable it in main(). The it variable in changeIt() is local to the function, and it refers to a copy of whatever argument value is passed when the function is called. Of course, when the value of it that is local to changeIt() is returned, a copy of its current value is made, and it’s this copy that’s returned to the calling program.

Pass-by-value is the default mechanism by which arguments are passed to a function. It provides a lot of security to the calling function by preventing the function from modifying variables that are owned by the calling function. However, sometimes you do want to modify values in the calling function. Is there a way to do this when you need to? Sure there is; one way is to use a pointer.

## Passing a Pointer to a Function

When a function parameter is a pointer type, the pass-by-value mechanism operates just as before. However, a pointer contains the address of another variable; a copy of a pointer contains the same address and therefore points to the same variable.

If you modify the definition of the first changeIt() function to accept an argument of type double*, you can pass the address of it as the argument. Of course, you must also change the code in the body of changeIt() to dereference the pointer parameter. The code is now like this:

```cpp
// Ex8_04.cpp
// Modifying the value of a caller variable
import <iostream>;

double changeIt(double* pointer_to_it);    // Function prototype

int main()
{
    double it {5.0};
    double result {changeIt(&it)};          // Now we pass the address

    std::cout << "After function execution, it = " << it
              << "\nResult returned is " << result << std::endl;
}

// Function to modify an argument and return it
double changeIt(double* pit)
{
    *pit += 10.0;                           // This modifies the original double
    std::cout << "Within function, *pit = " << *pit << std::endl;
    return *pit;
}
```

This version of the program produces the following output:

```text
Within function, *pit = 15
After function execution, it = 15
Result returned is 15
```

![](img/020c376b6cc4874983a4344f51a256de_282_0.png)

*Figure 8-3. Passing a pointer to a function*

This version of changeIt() serves only to illustrate how a pointer parameter can allow a variable in the calling function to be modified—it is not a model of how a function should be written. Because you are modifying the value of it directly, returning its value is somewhat superfluous.

## Passing an Array to a Function

An array name is essentially an address, so you can pass the address of an array to a function just by using its name. The address of the array is copied and passed to the function. This provides several advantages:

- First, passing the address of an array is an efficient way of passing an array to a function. Passing all the array elements by value would be time-consuming because every element would be copied. In fact, you can't pass all the elements in an array by value as a single argument because each parameter represents a single item of data.
- Second, and more significantly, because the function does not deal with the original array variable but with a copy, the code in the body of the function can treat a parameter that represents an array as a pointer in the fullest sense, including modifying the address that it contains. This means you can use the power of pointer notation in the body of a function for parameters that are arrays. Before we get to that, let's try the most straightforward case first—handling an array parameter using array notation.

This example includes a function to compute the average of the elements in an array:

```cpp
// Ex8_05.cpp
// Passing an array to a function
import <iostream>;
import <array>;           // For std::size()

double average(double array[], size_t count);   // Function prototype

int main()
{
  double values[] {1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0, 10.0};
  std::cout << "Average = " << average(values, std::size(values)) << std::endl;
}

// Function to compute an average
double average(double array[], size_t count)
{
  double sum {};                       // Accumulate total in here
  for (size_t i {}; i < count; ++i)
    sum += array[i];                   // Sum array elements
  return sum / count;                  // Return average
}
```

This produces the following brief output:

```text
Average = 5.5
```

The average() function works with an array containing any number of double elements. As you can see from the prototype, it accepts two arguments: the array address and a count of the number of elements. The type of the first parameter is specified as an array of any number of values of type double. You can pass any one-dimensional array of elements of type double as an argument to this function, so the second parameter that specifies the number of elements is essential. The function will rely on the correct value for the count parameter being supplied by the caller. There’s no way to verify that it is correct, so the function will quite happily access memory locations outside the array if the value of count is greater than the array length. With this definition, it is up to the caller to ensure that this doesn’t happen.

And in case you were wondering, no, you cannot circumvent the need for the count parameter by using either the sizeof operator or std::size() inside the average() function. Remember, an array parameter such as array simply stores the address of the array, not the array itself. So, the expression sizeof(array) would return the size of the memory location that contains the address of the array and not the size of the entire array. A call of std::size() with an array parameter name will simply not compile because std::size() has no way of determining the array’s size either. Without the definition of the array, the compiler has no way to determine its size. It cannot do so from only the array’s address.

Within the body of average(), the computation is expressed in the way you would expect. There’s no difference between this and the way you would write the same computation directly in main(). The average() function is called in main() in the output statement. The first argument is the array name, values, and the second argument is an expression that evaluates to the number of array elements.

The elements of the array that is passed to average() are accessed using normal array notation. We’ve said that you can also treat an array passed to a function as a pointer and use pointer notation to access the elements. Here’s how average() would look in that case:

```cpp
double average(double* array, size_t count)
{
  double sum {};
  for (size_t i {}; i < count; ++i)
    sum += *array++;        // Accumulate total in here
  return sum / count;       // Return average
}
```

For all intents and purposes, both notations are completely equivalent. In fact, as you saw in Chapter 5, you can freely mix both notations. You can, for instance, use array notation with a pointer parameter:

```cpp
double average(double* array, size_t count)
{
  double sum {};                 // Accumulate total in here
  for (size_t i {}; i < count; ++i)
    sum += array[i];             // Sum array elements
  return sum / count;            // Return average
}
```

There really is no difference at all in the way any of these function definitions are evaluated. In fact, the following two function prototypes are considered identical by the compiler:

```cpp
double average(double array[], size_t count);
double average(double* array, size_t count);
```

We will revisit this later in the section on function overloading.
