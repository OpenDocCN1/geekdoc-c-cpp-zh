# Figure 3  
Execution of a `for` Loop

```
```cpp
// Initialize counter
counter = 1;

for (counter = 1; counter <= 10; counter++) {
    cout << counter << endl;
}

// Check condition
counter <= 10

// Execute loop body
cout << counter << endl;

// Increment counter
counter = counter + 1;

// Check condition again
counter <= 10
```
```

> **Progressive figures** trace code segments to help students visualize the program flow. Color is used consistently to make variables and other elements easily recognizable.

```
```cpp
// Function call
 double result1 = cube_value(2);
 result1 = 8;
 slide_length = 2;

// Initializing function parameter variable
 double result1 = cube_value();
 double result1 = cube_value();
 slide_length = 2;

// About to return the value
 double volume = slide_length * slide_length * slide_length;
 return volume;
 slide_length = 2;
 volume = 8;

// After function call
 double result1 = cube_value(2);
 result1 = 8;
```
```

# Figure 3  Parameter Passing

+   - The parameter variable `slide_length` of the `cube_value` function is created.
+   - The parameter variable is initialized with the value of the argument that was passed in the call. In our case, `slide_length` is set to 2.
+   - The function is then called and the value is returned.
+   - The variable receives the returned value.

> **Self-check exercises** at the end of each section are designed to make students think through the new material—and can spark discussion in lecture.

# SELF-CHECK

+   12. Write the `for` loop of the infinite `cpp` program as a `while` loop.
+   13. How many numbers does this loop print?
+   
+   ```cpp
+   for (int i = 10; i >= 0; i--) {
+       cout << i << endl;
+   }
+   ```
+   
+   14. Write a `for` loop that prints all even numbers between 10 and 20 (inclusive).
+   15. Write a `for` loop that computes the sum of the integers from 1 to n.
+   16. How would you modify the `for` loop of the `while` loop program to print all values until the investment has doubled?

**Practice it**  Now you can try these exercises at the end of the chapter: R4.2, R4.7, P4.12.

> **Optional engineering exercises** engage students with applications from technical fields.

**Engineering P7.20**  Write a program that simulates the control software for a “people mover” system, a set of driverless trains that move in two concentric circular tracks. A set of switches allows trains to switch tracks.

In your program, the outer and inner tracks should each be divided into ten segments. Each track segment can contain a train at a time. A train moves to an adjacent segment. If that segment is occupied, the adjacent segment in the other track is tried.

Define a Segment structure. Each segment has a pointer to the next and previous segments in its track. A train can be removed from a track when it is occupied, to make adjacent segment in the other track.

![](bbox=[0.716, 0.624, 0.849, 0.701])

# `ch05/cube.cpp`

```
```cpp
#include <iostream>
using namespace std;

// Computes the volume of a cube.
// @param side_length the side length of the cube
// @return the volume

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
```text
A cube with side length 2 has volume 8
A cube with side length 10 has volume 1000
```
```

> **Program listings** are carefully designed for easy reading, going well beyond simple color coding. Functions are set off by a subtle outline.