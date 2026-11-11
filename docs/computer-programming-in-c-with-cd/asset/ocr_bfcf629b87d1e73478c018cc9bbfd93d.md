the specified value: if you call the function without specifying value for the default argument, it takes its default value. The default value is specified at the time of defining the program. For example, if you declare a function as float convert(float cel=100.00F), the convert() function has a default argument (float cel=100.00F) and cel has a default value 100.00F. Now, if you call this function as convert(150.00F), the argument cel takes 150.00F as it value; and if you call this function as convert(), the argument cel takes the default value that is 100.00F. Listing 13 shows function with default argument (you can find the FuncB.cpp file on the CD in the code/chapter3 folder):

# ▶ Listing 13: Creating Function with Default Argument

```
    #include <iostream.h>

    float convert(float cel=100.00F)  // function definition
    {
        float fahrenheit;
        fahrenheit = (cel*9)/5 + 32 ;
        return fahrenheit;
    }
    int main()
    {
        float celsius;
        cout<<"The equivalent temperature in fahrenheit is :"<<convert(); // function call
        return 0;
    }
```

Output:

The equivalent temperature in fahrenheit is :212

In Listing 13, the convert() function is defined with a default argument cel. This convert() function converts the temperature from Celsius to Fahrenheit and returns temperature in Fahrenheit to the caller program. The default value of the cel argument is specified as 100.00F. Finally, the convert() function is called from the main() function and the value returned from the convert() function is displayed to the user.

# ■ Describing Call by Value and Call by Reference

Calling a function in C++ can be achieved in two ways – call by value and call by reference. In call by value, the copy of variables are passed to the function; and in call by reference, the memory address of variables are passed to the function.

Call by value means that the value of argument is passed to a function, where value is assigned to a new variable in memory before being passed to the function. For example, the following code snippet shows a function call with call by value: