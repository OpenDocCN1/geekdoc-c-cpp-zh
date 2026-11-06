Here is the complete program. Note the comment that describes the behavior of the function. (Programming Tip 5.1 on page 199 describes the format of the comment.)

# ch05/cube.cpp

```
```cpp
#include <iostream>

using namespace std;

/**
  Computes the volume of a cube.
  @param side_length the side length of the cube
  @return the volume
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
    cout << "A cube with side length 10 has volume" << result2 << endl;

    return 0;
}
```
```

# Program Run

```
```text
A cube with side length 2 has volume 8
A cube with side length 10 has volume 1000
```
```

![](bbox=[0.077, 0.591, 0.226, 0.678])

+   5. What is the value of `cube_volume(3)`?
+   
+   6. What is the value of `cube_volume(cube_volume(2))`?
+   
+   7. Provide an alternate implementation of the body of the `cube_volume` function by calling the `pow` function.
+   
+   8. Define a function `square_area` that computes the area of a square of a given side length.
+   
+   9. Consider this function:
+   
+   ```cpp
+   int mystery(int x, int y)
+   {
+       double result = (x + y) / (y - x);
+       return result;
+   }
+   ```
+   
+   What is the result of the call `mystery(2, 3)`?

**Practice It**  Now you can try these exercises at the end of the chapter: R5.2, P5.2, P5.7.