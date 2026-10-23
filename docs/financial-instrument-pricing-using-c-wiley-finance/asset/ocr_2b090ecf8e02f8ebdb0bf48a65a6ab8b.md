```
```cpp
int i=20;                  // Create an int.
double d=3.16;             // Create a double.

decltype(i) j=i;           // j is an int.
decltype(d) k=d;           // k is a double.

// Promote float * int to double
float f = 3.3F;
int n= 4;
decltype(d) d2 = f*n;
```
```

In the last example we are stating that variable d2 should be of type double. We can check the validity of this statement by calling `std::is_same` type trait (that we discuss in more detail in Chapter 6):

```
```cpp
std::cout << "Check decltype:  " << std::is_same<double,
decltype(d)>::value; // true
```
```

(using the same variables as above).

Another example using the same variables as above is:

```
```cpp
// What is the result of int*double. With decltype we
// don't need to know anymore.
decltype(j*k) l=j*k; // Result of int*double is double.
std::cout<<j<<"*"<<k<<"="<<l<<std::endl;

std::cout << "Check decltype:  "
          << std::is_same<double, decltype(j*k)>::value;   // true
```
```

Finally, decltype can be applied to lambda functions as the following code shows:

```
```cpp
// decltype and lambda functions
auto f2 = [](double x, double y) -> int
{
    int result = std::floor(x + y);
    return result;
};

auto f3 = [](double x, double y) -> double
{
    double result = x + y;
    return result;
};

// Lambda function types are unique and unnamed
std::cout << std::boolalpha
          << "Type of lambda function, not its return type:  "
          << std::is_same<int, decltype(f2)>::value;  // false
```
```