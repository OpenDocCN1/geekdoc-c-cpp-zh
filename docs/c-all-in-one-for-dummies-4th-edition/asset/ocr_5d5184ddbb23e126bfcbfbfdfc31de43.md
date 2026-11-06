# # USING AUTO FOR FUNCTIONS

In general, specifically defining the type of the variable you use to receive output from a function makes your code more readable. However, there are situations for which you may not know the precise output type or different versions of the function output different types (which is very confusing). In this case, you begin by setting GCC to use C++17, as described in the "Working with ranges" section of Book 1, Chapter 5. Then, you can write the Fabs2 example shown in Listing 6-2, as shown in the following UsingAuto example:

```
```cpp
#include <iostream>
#include <math.h>

using namespace std;

int main()
{
    auto mynumber = fabs(-23.87);
    cout << mynumber << endl;
    return 0;
}
```
```

The result is the same as the Fabs2 example. The difference is that mynumber is now of type auto, where C++ automatically detects the data type for you, instead of double, where you explicitly define the data type.

# ## Passing a variable

You can also pass the value of a variable into a function. The Fabs3 example in Listing 6-3 creates two variables: One is passed into the function, and the other receives the result of the function.

+   - **LISTING 6-3:** Seeing Yet Another Way to Use fabs()

```
```cpp
#include <iostream>
#include <math.h>

using namespace std;

int main()
```
```