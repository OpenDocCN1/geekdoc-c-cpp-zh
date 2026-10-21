The constructor is now secure because any dimension that the user of the class tries to set to a negative number or zero is set to 1 in the constructor. You might also consider displaying a message for a negative or zero dimension because there’s obviously an error when this occurs, and arbitrarily and silently setting a dimension to 1 might not be the best solution.

The default copy constructor is satisfactory for our class because you have no dynamic memory allocation for data members, and the default assignment operator will also work as you would like. The default destructor also works perfectly well in this case so you don’t need to define it. Perhaps now you should consider what is required to support comparisons of objects of our class.

# Comparing CBox Objects

You should include support for the operators >, >=, ==, < and <= so that they work with both operands as CBox objects, as well between a CBox object and a value of type double. You can implement these as ordinary global functions because they don’t need to be member functions. You can write the functions that compare the volumes of two CBox objects in terms of the functions that compare the volume of a CBox object with a double value, so let’s start with the latter. You can start by repeating the operator>() function that you had before:

```
```cpp
// Function for testing if a constant is > a CBox object
int operator>(const double& value, const CBox& aBox)
{
  return value > aBox.Volume();
}
```
```

You can now write the operator<() function in a similar way:

```
```cpp
// Function for testing if a constant is < CBox object
int operator<(const double& value, const CBox& aBox)
{
  return value < aBox.Volume();
}
```
```

You can code the implementations of the same operators with the arguments reversed in terms of the two functions you have just defined:

```
```cpp
// Function for testing if CBox object is > a constant
int operator>(const CBox& aBox, const double& value)
{ return value < aBox; }
```
```

```
```cpp
// Function for testing if CBox object is < a constant
int operator<(const CBox& aBox, const double& value)
{ return value > aBox; }
```
```

You just use the appropriate overloaded operator function that you wrote before, with the arguments from the call to the new function switched.