This version of changeIt() serves only to illustrate how a pointer parameter can allow a variable in the calling function to be modified—it is not a model of how a function should be written. Because you are modifying the value of it directly, returning its value is somewhat superfluous.

# ## Passing an Array to a Function

An array name is essentially an address, so you can pass the address of an array to a function just by using its name. The address of the array is copied and passed to the function. This provides several advantages:

+   - First, passing the address of an array is an efficient way of passing an array to a function. Passing all the array elements by value would be time-consuming because every element would be copied. In fact, you can't pass all the elements in an array by value as a single argument because each parameter represents a single item of data.
+   - Second, and more significantly, because the function does not deal with the original array variable but with a copy, the code in the body of the function can treat a parameter that represents an array as a pointer in the fullest sense, including modifying the address that it contains. This means you can use the power of pointer notation in the body of a function for parameters that are arrays. Before we get to that, let's try the most straightforward case first—handling an array parameter using array notation.

This example includes a function to compute the average of the elements in an array:

```
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

```
    Average = 5.5
```