# Syntax 5.1 Function Definition

![](bbox=[0.27, 0.16, 0.92, 0.45])

Here is the complete program. Note the comment that describes the behavior of the function. (Programming Tip 5.1 describes the format of the comment.)

# sec02/cube.cpp

```
```cpp
#include <iostream>

using namespace std;

/**
 * Computes the volume of a cube.
 * @param side_length the side length of the cube
 * @return the volume
 */
double cube_volume(double side_length)
{
    double volume = side_length * side_length * side_length;
    return volume;
}

int main()
{
    double result1 = cube_volume(2);
    double result2 = cube_volume(10);
    cout << "A cube with side length 2 has volume " << result1 << endl;
    cout << "A cube with side length 10 has volume " << result2 << endl;

    return 0;
}
```
```

# Program Run

```
A cube with side length 2 has volume 8
A cube with side length 10 has volume 1000
```