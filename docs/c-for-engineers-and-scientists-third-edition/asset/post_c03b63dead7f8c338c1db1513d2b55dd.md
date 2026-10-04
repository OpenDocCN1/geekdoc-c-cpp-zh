
## 322 Modularity Using Functions

b. Include the function written in Exercise 5a in a working program. Make sure your function is called from main() and returns a value to main() correctly. Have main() use a cout statement to display the returned value. Test the function by passing various data to it.

6. (General Math) a. The volume, $V$, of a cylinder is given by the formula
$V = \pi r^2 L$

where $r$ is the cylinder's radius and $L$ is its length. Using this formula, write a C++ function cylvol() that accepts a cylinder's radius and length and returns its volume.

b. Include the function written in Exercise 6a in a working program. Make sure your function is called from main() and returns a value to main() correctly. Have main() use a cout statement to display the returned value. Test the function by passing various data to it.

7. (General Math) a. The surface area, $S$, of a cylinder is given by the formula
$S = 2\pi rl$

where $r$ is the cylinder's radius, and $l$ is the length of the cylinder. Using this formula, write a C++ function named area() that accepts a cylinder's radius and length and returns its surface area.

b. Include the function written in Exercise 7a in a working program. Make sure your function is called from main() and returns a value to main() correctly. Have main() use a cout statement to display the returned value. Test the function by passing various data to it.

8. (Numerical) A second-degree polynomial in $x$ is given by the expression $ax^2 + bx + c$, where $a$, $b$, and $c$ are known numbers and $a$ is not equal to 0. Write a C++ function named poly2(a, b, c, x) that computes and returns the value of a second-degree polynomial for any values of $a$, $b$, and $c$.

9. (Structural Eng.) a. The maximum allowable deflection of a beam depends on its function. For a floor, the typical maximum deflection, in, $Dmax = L / 240$, and for a roof beam, $Dmax = L / 180$, where $L$ is the length of the beam. Using these formulas, write and test a function named maxDefect() that accepts the length of a beam, in feet, the type of beam (floor or roof) as a character code and returns the maximum allowable deflection.

b. Include the function written in Exercise 9a in a working program. Make sure your function is called from main() and returns a value to main() correctly. Have main() use a cout statement to display the returned value. Test the function by passing various data to it.

10. (Structural Eng.) a. The load, $P$, in units of kips, applied to a column that causes the column to buckle is referred as the critical buckling load. This load can be determined by using this formula:

$Pcr = \pi^2 E A / (L / r^2)$

$E$ is the modulus of elasticity of the column's material.

$A$ is the cross-sectional area.

$L$ is the length of the column.

$r$ is the column's radius of gyration.

Using this formula, write a C++ function named `cLoad()` that accepts values of $E, A, L$, and $r$ and returns the critical buckling load.

b. Include the function written in Exercise 10a in a working program. Make sure your function is called from `main()` and returns a value to `main()` correctly. Have `main()` use a `cout` statement to display the returned value. Test the function by passing various data to it.

11. (Numerical) a. The following is an excellent programming algorithm for rounding a real number to $n$ decimal places:

- Step 1: Multiply the number by $10^n$
- Step 2: Add 0.5
- Step 3: Delete the fractional part of the result
- Step 4: Divide by $10^n$

For example, using this algorithm to round the number 78.374625 to three decimal places yields:

- Step 1: $78.374625 \times 10^3 = 78374.625$
- Step 2: $78374.625 + 0.5 = 78371.125$
- Step 3: Delete the fractional part: $78375$
- Step 4: $78375 / 10^3 = 78.375$

*(Note: The example steps in the OCR were corrupted/convoluted; I have restored the logic based on the standard algorithm described).*

12. (Numerical) a. Write a C++ function named isLeapYear(int year) that returns 1 if the given year is a leap year, and 0 otherwise.

b. Include the function written in Exercise 12a in a working program. Make sure your function is called from main() and returns a value to main() correctly. Have main() use a cout statement to display the returned value. Test the function by passing various data to it.

13. (Numerical) a. Write a C++ function named roundTo(double value, int n) that returns the value rounded to $n$ decimal places.

b. Include the function written in Exercise 13a in a working program. Make sure your function is called from main() and returns a value to main() correctly. Have main() use a cout statement to display the returned value. Test the function by passing various data to it.
