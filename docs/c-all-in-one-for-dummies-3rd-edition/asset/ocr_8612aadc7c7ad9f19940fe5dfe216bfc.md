When the transform() is complete, Result contains a list of bool values that indicate whether the individual numbers in vect are greater than 3. To see these values as true or false text output, rather than numbers, you need to call cout.setf(ios::boolalpha). The code then uses a for_each() loop to display the individual values in Result. Here is the output you see when you run this example.

```
```
false
false
false
true
```
```

Given that the input values in vect are 1, 2, 3, and 4, it's true that the last element of vect, 4, is greater than the number 3. Using a transform() with a lambda expression, as shown here, is a great way to reduce the code required to perform various kind of bulk comparisons (among other transformation-specific tasks).

# ### Using a specific return type

Sometimes a lambda expression is complex enough that the compiler can't figure out what return type to use. Often you see an error message during the compilation process when this occurs. Fortunately, it's easy to fix this problem by simply telling the compiler what sort of return type to expect. The ReturnType02 example shown in Listing 7-4 demonstrates how to perform this task.

# #### Listing 7-4: Using a Specific Return Type

```
```cpp
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

void ProcessVector(vector<int>& vect)
{
    vector<bool> Result;
    Result.resize(vect.size());

    transform(vect.begin(), vect.end(), Result.begin(),
              [](int x)->bool{return x > 3;});

    cout.setf(ios::boolalpha);
    for_each(Result.begin(), Result.end(),
             [](bool x){cout << x << endl;});
}
```
```