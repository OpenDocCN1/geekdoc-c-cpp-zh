This example uses the EvenPair structure to hold two variables that contain the original value you want to check and show whether that value is even. In `main()`, you begin by creating two vectors: one input, `Values`, and one output, `Evens`. The Evens vector will contain a list of the original values and a Boolean showing whether each value is even.

![](bbox=[0.163, 0.202, 0.226, 0.269])

The call to `Transform()` takes pointers to the beginning and ending of Values, the beginning of Evens, and the name of a function to use for the transformation. In this case, `IsEven()` receives an individual Value, determines whether it’s even using the mod operator `Value % 2`, and then outputs a Value and Even pair.

After the transformation completes, a foreach loop checks each value in Evens and outputs an appropriate string. Here are the results:

```
1 is odd.
2 is even.
3 is odd.
4 is even.
```

# Using Lambda Expressions for Implementation

A lambda expression is an unnamed function that you can use in place of a regular function reference. Using a lambda expression can make your code more readable by placing the function inline. Chapters 2 and 3 of this minibook cover lambda expressions in detail, but the Lambda example, shown in Listing 1-10, shows an alternative way to create the code displayed in Listing 1-9 in a shorter way.

# LISTING 1-10: Performing a Transform Using a Lambda Expression

```
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct EvenPair {
    int Value;
    bool Even;
};
```