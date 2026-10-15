A function can be defined in the form

# Return name (parameters)

**Return** is the value that will return the function and can be a data type (int, float ...) or **void** that is used to indicate that no value returns.

**Name** is the identifier of the function

**Parameters** is a separate list with commas of variables that we will pass to the function.

Eg.
float CalculateVat (float price, float vat)

# Parameter by value

The most common way to pass parameters to a function is to pass them by value.

Constants or variables are passed that will not change value in the execution of the function.

```
float CalculateVAT (float price, float vat)
{
    return price * vat/100;
}

int main()
{
    float vat;

    vat = CalculateVAT(1000, 21);
}
```

# Parameters by reference

If we want a parameter of a function to be modified within the function and return the modified value, the parameter can be used by reference.