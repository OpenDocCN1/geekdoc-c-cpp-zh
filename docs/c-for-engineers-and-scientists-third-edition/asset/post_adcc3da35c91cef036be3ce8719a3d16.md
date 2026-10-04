
## Problem Solving Using C++

3. Following the function name, the body of a function has the following general form:
```
{
  All C++ statements in here;
}
```

4. All C++ statements must be terminated by a semicolon.

5. Four types of data were introduced in this chapter: integer, floating-point, character, and Boolean. C++ recognizes each of these data types, in addition to other types you learn about later chapters.

6. The cout object can be used to display all C++ data types.

7. When the cout object is used in a program, the preprocessor command `#include <iostream> using namespace std;` must be placed at the top of the program. `#include <iostream>` preprocessor command does not end with a semicolon.

8. Every variable in a C++ program must be declared and the type of value it can store must be specified. Declaration statements must be placed anywhere in the function, although a variable can be used only after it is declared. Variables can also be initialized when they are declared. Variables of the same type can be declared with a single declaration statement. Variable declaration statements have this general form:
`data variableName(s);`

9. A simple C++ program containing declaration statements has this typical form:
```cpp
#include <iostream>
using namespace std;

int main()
{
  // declaration statements;
  // other statements;

  return 0;
}
```

10. Declaration statements always play the software role of informing the compiler of a function's valid variable names. When a variable declaration also causes the computer to set aside memory locations for the variable, the declaration statement is called a definition statement. (All declarations used in this chapter have also been definition statements.)

11. The sizeof() operator can be used to determine the amount of storage reserved for variables.

## Programming Projects for Chapter 2

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_116_0.png)

- 1. (General Math) a. Design, write, compile, and execute a C++ program that calculates the perimeter of a two-dimensional triangle with sides $a = 1$ in, $b = 1.5$ in, and $c = 2$ in, as shown in Figure 2.17. The perimeter is given by this formula:
`perimeter = a + b + c`

- b. Manually check the values computed by your program. After verifying that your program is working correctly, modify it to determine the perimeter of a two-dimensional triangle with sides $a = 1.62$ in, $b = 2.13$ in, and $c = 3.2$ in.

- 2. (General Math) a. Design, write, compile, and execute a C++ program that calculates and displays the area of a two-dimensional triangle, like the one in Figure 2.17, with a base of 1 in and a height of 1.5 in. The area is given by this formula:
$Area = 1/2(base) \times (height)$

- b. Manually check the values computed by your program. After verifying that your program is working correctly, modify it to determine the area of a two-dimensional triangle with a base of 2 in and a height of 1.67 in.

- 3. (General Math) a. Design, write, compile, and execute a C++ program to calculate the volume of a sphere with a radius, $r$ of 3 in. The volume is given by this formula:
$Volume = 4/3\pi r^3$

- b. Manually check the values computed by your program. After verifying that your program is working correctly, modify it to determine the volume of a cube with a base of 1.67 in.

- 4. (Physics) a. Design, write, compile, and execute a C++ program to calculate the elapsed time it takes to make a 183.67 mile trip. This is the formula for computing elapsed time:
$elapsed time = total distance / average speed$
The average speed during the trip is 58 mph.

- b. Manually check the values computed by your program. After verifying that your program is working correctly, modify it to determine the elapsed time it takes to make a 372-mile trip at an average speed of 67 mph.

- 5. (Numerical) a. Design, write, compile, and execute a C++ program to calculate the sum of integers from 1 to 100. This is the formula for this sum:
$sum = (n/2)(2 \times a + (n-1))$
$n$ is the number of integers to be added. $a$ is the first number.

- b. Manually check the values computed by your program. After verifying that your program is working correctly, modify it to determine the sum of integers from 1000.

- 6. (Physics and Electrical) The energy, $E$, of a photon, in Joules, $J$, is provided by this formula:
$E = P \times f$
$P$ is $6.626 \times 10^{-34}$ Joules/sec (Planck's constant).
$f$ is frequency in Hertz (Hz).

- a. Given the frequency of light in $3.84 \times 10^{14}$ Hz, design, write, compile, and execute a C++ program to calculate the energy of light with a frequency of $5.7 \times 10^{14}$. Verify the result produced by your program with a hand calculation.

- b. After verifying that your program is working correctly, use it to determine the photon output of 60 Hz.

- 7. (Physics) a. The weight of an object on Earth is a measurement of the downward force caused by Earth's gravity. The formula for this force is determined using Newton's Second Law:
$F = M \times A_g$
$F$ is the object's weight. $M$ is the object's mass. $A_g$ is the acceleration caused by Earth ($32.2$ ft/sec² = $9.82$ m/s²). Given this information, design, write, compile, and execute a C++ program to calculate the weight in lbs of a person having a mass of 4 lb. Verify the result produced by your program with a hand calculation.

- b. After verifying that your program is working correctly, use it to determine the weight, of Earth, of a person having a mass of 3.2 lb.

- 8. (Physics) Rewrite the program you wrote for Exercise 7 to provide the mass of a person as an output, or her weight as an input to the program. Use your program to determine the mass of a person who weighs 140 lb on Mars.

- b. Modify the program written for Exercise 7a to also output the person's weight on Mars and the moon. The pull of gravity on Mars is $12.54$ ft/sec² = $3.728$ m/s², and on the moon is $5.33$ ft/sec² = $1.625$ m/s².

- 9. (Civil Eng.) The maximum load that can be placed at the end of a symmetrical wooden beam, as the rectangular beam shown in Figure 2.18, can be calculated as the following:
$L = \frac{S \times I}{d \times c}$
$L$ is the maximum weight in lbs of the load placed on the beam. $S$ is the stress in lbs/in². $I$ is the beam's rectangular moment of inertia in units of in⁴. $d$ is the distance in inches that the load is placed from the fixed end of the beam (moment arm). $c$ is one-half the height in inches of the symmetrical beam.

img/e2a849fc7bc04aa2e6669ad865e0c22b_118_0.png

**Figure 2.18** Calculating a symmetrical beam’s maximum load

For a 2” x 4” wooden beam, the rectangular moment of inertia is given by this formula:
$I = \frac{base \times height^3}{12} = \frac{2 \times 4^3}{12} = 10.67$
$c = \frac{1}{2}(4\text{ in}) = 2\text{ in}$

- a. Using this information, design, write, compile, and execute a C++ program that computes the maximum load in lbs that can be placed at the end of an 8-foot 2” x 4” wooden beam so that the stress on the fixed end is 3000 lbs/in².

- b. Use the program developed in Exercise 9 to determine the maximum load in lbs that can be placed at the end of a 3” x 6” wooden beam so that the stress on the fixed end is 3000 lbs/in².

- 10. (Civil Eng.) Modify the program for Exercise 9 to determine the maximum load that can be placed at the end of an 8-foot I-beam, shown in Figure 2.19, so that the stress on the fixed end is 20,000 lbs/in². Use the fact that this beam’s rectangular moment of inertia is 21.4 in⁴ and the value of c is 3 in.

- 11. (Mechanical Eng.) The minimum radius required for a cylindrical rod, such as one supporting a bicycle pedal (see Figure 2.20), to provide enough support for the pressure
