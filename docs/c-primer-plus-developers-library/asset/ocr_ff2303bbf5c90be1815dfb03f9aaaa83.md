ios_base::fixed and ios_base::floatfield are constants provided by including iostream.

# Listing 3.8　**floatnum.cpp**

```
```cpp
// floatnum.cpp -- floating-point types
#include <iostream>
int main()
{
    using namespace std;
    cout.setf(ios_base::fixed, ios_base::floatfield); // fixed-point
    float tub = 10.0 / 3.0;     // good to about 6 places
    double mint = 10.0 / 3.0;   // good to about 15 places
    const float million = 1.0e6;

    cout << "tub = " << tub;
    cout << ", a million tubs = " << million * tub;
    cout << ",\nand ten million tubs = ";
    cout << 10 * million * tub << endl;

    cout << "mint = " << mint << " and a million mints = ";
    cout << million * mint << endl;
    return 0;
}
```
```

Here is the output from the program in Listing 3.8:

```
```text
tub = 3.333333, a million tubs = 3333333.250000,
and ten million tubs = 33333332.000000
mint = 3.333333 and a million mints = 3333333.333333
```
```

# **Program Notes**

Normally cout drops trailing zeros. For example, it would display 3333333.250000 as 3333333.25. The call to `cout.setf()` overrides that behavior, at least in new implementations. The main thing to note in Listing 3.8 is how float has less precision than double. Both tub and mint are initialized to 10.0 / 3.0. That should evaluate to 3.3333333333333333...(etc.). Because cout prints six figures to the right of the decimal, you can see that both tub and mint are accurate that far. But after the program multiplies each number by a million, you see that tub diverges from the proper value after the seventh three. tub is good to seven significant figures. (This system guarantees six significant figures for float, but that's the worst-case scenario.) The type double variable, however, shows 13 threes, so it's good to at least 13 significant figures. Because the system guarantees 15, this shouldn't surprise you. Also note that multiplying a million tubs by 10 doesn't quite result in the correct answer; this again points out the limitations of float precision.