generate a different sequence of numbers every time we run the program, we use an object of type `random_device`, to obtain a seed, as follows.

```
random_device rddevice{};
default_random_engine num{ rddevice() };
```

Consider the following program:

```
//C++11: Random number generator.

#include <iostream>
#include <random>

using namespace std;

int main()
{
    random_device rddevice{};
    default_random_engine num{ rddevice() };
    uniform_int_distribution<unsigned int> randomNum{1, 6};

    for (unsigned int count = 1; count <= 10; count++)
        cout << randomNum(num) << " ";
    cout << endl;

    return 0;
}
```

# Sample Runs:

# Sample Run 1:

```
3 2 5 6 5 2 5 5 5 3
```

# Sample Run 2:

```
2 1 6 1 2 5 4 5 3 6
```

The statements to declare the objects `rddevice`, `num`, and `randomNum` work as explained before. The `for` loop executes 10 times generating a sequence of 10 random numbers using the objects `randomNum` and `num`.

To generate random real numbers we use the class `uniform_real_distribution` as follows:

```
random_device rddevice{};
default_random_engine num{ rddevice() };
uniform_real_distribution<double> randomRealNum {1, 40};
```

The first two statements are the same as before. In the third statement, the object `randomRealNum` randomly generates a random number between 1 and 40 of type `double`.

Note that the C++11 standard library provides 25 distribution types in five categories. For example, `uniform_int_distribution` and `uniform_real_distribution` fall in the category of uniform distributions.