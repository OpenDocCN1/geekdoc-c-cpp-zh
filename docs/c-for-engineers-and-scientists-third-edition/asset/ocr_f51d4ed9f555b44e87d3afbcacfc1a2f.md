# Chapter 5

# 243

while Loops

# Technical Note

# Fluid Mechanics (continued)

Essentially, the Reynolds number is equal to the ratio of

fluid speed

viscous forces

A higher Reynolds number correlates with a higher fluid speed. However, when viscous forces predominate (they are retracting forces), and the Reynolds number is lower, and the fluid flow is slower. In a highly viscous fluid, such as heavy oil, all the fluid's particles tend to be kept in line, which is referred to as laminar flow. Critical Reynolds numbers for determining flow type as follows:

+   - Re < 2000: Fluid flow is laminar (least common type of water flow).
- 2000 ≤ Re ≤ 3000: Fluid flow is in transition.
- Re > 3000: Fluid flow is turbulent (most common type of fluid flow).

![](bbox=[0.117, 0.423, 0.163, 0.477])

# EXERCISES 5.2

1. (Practice) Rewrite Program 5.1 to print the numbers 2 to 10 in increments of two. The output of your program should be the following:

2 4 6 8 10

2. (Practice) Rewrite Program 5.4 to produce a table starting at a Celsius value of -10 and ending with a Celsius value of 60, in increments of 10 degrees.

3. (Desk Checking) a. For the following program, determine the total number of items displayed as the first and the last numbers printed:

```
#include <iostream>
using namespace std;

int main() {
    int num = 0;
    while (num <= 20)
    {
        num++;
        cout << num << " ";
    }
    return 0;
}
```

b. Enter and run the program from Exercise 3a on a computer to verify your answers to the exercise.