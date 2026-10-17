```
```cpp
{
.
.
.
}
```
```

# Way-3

Formal parameters as an unsized array as follows:

```
```cpp
void myFunction(int param[])
{
.
.
.
}
```
```

Now, consider the following function, which will take an array as an argument along with another argument and based on the passed arguments, it will return average of the numbers passed through the array as follows:

```
```cpp
double getAverage(int arr[], int size)
{
    int    i, sum = 0;
    double avg;

    for (i = 0; i < size; ++i)
    {
        sum += arr[i];
    }

    avg = double(sum) / size;

    return avg;
}
```
```

Now, let us call the above function as follows:

```
```cpp
#include <iostream>
```
```