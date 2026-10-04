
## Chapter 1 11

## Preliminary Two: Exponential and Scientific Notations

In exponential notation, the letter e stands for exponent. The number following e represents powers of 10 and indicates the number of places the decimal point should be moved to obtain the standard decimal value. The decimal point is moved to the right if the number is positive, or to the left if the number after e is negative. the e3 in 1.62e3 moves the decimal point three places to the right, so the number becomes 1625.

The e-3 in 7.3e-3 means the decimal point three places to the left, so 7.3e-3 becomes .00731. Using these representations, Avogadro's number is 6.0221407e23 and 6.02214e-19 in exponential and scientific notation, and the universal gravitational constant is written as 6.6742e-11 in exponential notation and 6.6742× 10⁻¹¹ in scientific notation.

As noted, exponential notation is used to enter very large or small numbers in a C++ program and will be used in Section 2.6, where very large numbers are required for the option.

## Using Scientific Notation

An essential part of engineering and scientific programming is understanding what formulas are to be used and verifying calculations, typically by hand. For evaluating formulas that use very large or small numbers, which isn't uncommon in the applications you'll be programming, scientific notation is convenient. The reason is that scientific notation permits using the following two basic rules, as they apply to

- Rule 1: 10ⁿ × 10ᵐ for any values, positive or negative, of n and m
  Examples: 10² × 10⁵ = 10⁷ (that is, 100 × 100,000 = 10,000,000)
  10² × 10⁻⁵ = 10⁻³ (that is, 100 × .00001 = .01)
  10² × 10⁻⁶ = 10⁻⁴ (that is, 100 × .000001 = .001)
  10² × 10⁻⁷ = 10⁻⁵ (that is, 100 × .0000001 = .00001)
  10² × 10⁻⁸ = 1

- Rule 2: 10ⁿ / 10ᵐ for any positive or negative value of n

- Examples: 10⁷ / 10² = 10⁵ (that is, .01)
  10⁷ / 10¹⁰ = 10⁻³ (that is, .001)
  10⁴ / 10¹ = 10³ (that is, 1000)
  10⁴ / 10⁸ = 10⁻⁴ (that is, .00000)

Note that in scientific notation (as in exponential notation), it represents the actual number of zeros that follow the 1, but if the exponent is negative, it represents one less than the number of zeros after the decimal point and before the 1.

After you understand the basic rules of using scientific notation, you can combine them easily, as shown in this computation:

```
10² × 10⁸ = 10¹⁰
10⁴ / 10⁷ = 10⁻³
```

## Preliminaries

If scientific notation was concerned only with powers of 10, as in the preceding example, its usefulness would be extremely limited. Fortunately, however, this notation can be used with any decimal number. For example, take a look at this computation:

236,000 × .345 × 1,345,000
67.8 × .000007

This computation is calculated more easily by first converting each number to its scientific notation, and then combining exponents (using Rules 1 and 2) as follows:

```
$2.36 × 10^5 × 3.45 × 10^1 × 1.345 × 10^6 =
6.78 × 10^1 × 7.0 × 10^6
2.36 × 3.45 × 10^{10} =
6.78 × 10^7 × 10^{-5}
2.36 × 1.345 × 10^{15}
6.78 × 7.0$
```

Finally, the remaining numbers in the numerator can be multiplied and divided by the numbers in the denominator to yield a final result of .2307 × 10^{15} = 2.307 × 10^{14}.

Whenever a formula contains one or more small or large numbers, the technique of first, converting the number to scientific notation, and second, dealing with the exponents and remaining numbers individually. This technique can be of great help in the final computation. (Note that converting all the numbers isn't necessary.) You'll make use of this technique when performing hand calculations to validate results during the testing of a program.

Scientific Notational Symbols Certain scientific notations often occur enough in science and engineering applications that they have their own symbols. The The most commonly used are listed in Table 1.2.

### Table 1.2 Notational Symbols

| Scientific Notation | Symbol | Name |
| :--- | :--- | :--- |
| $10^{-12}$ | p | pico |
| $10^{-9}$ | n | nano |
| $10^{-6}$ | $\mu$ | micro |
| $10^{-3}$ | m | milli |
| $10^3$ | k | kilo |
| $10^6$ | M | mega |
| $10^9$ | G | giga |
| $10^{12}$ | T | tera |

For example, the storage capacities of disks and thumb drives are currently specified in megabytes (MB) and gigabytes (GB), which means they contain millions ($10^6$) and billions ($10^9$) of bytes. See Section 1.5 for the definition of a byte. Similarly, processing speeds are specified in nanoseconds (nsec), which means a billionth ($10^{-9}$) of a second.

## Chapter 1 Preliminary Two: Exponential and Scientific Notations

### EXERCISES 1.2

1. (Practice) Convert the following numbers from exponential form into standard decimal form:
   a. 6.34e5
   b. 1.9562e2
   c. 8.395e1
   d. 2.95e-3
   e. 4.623e-4

2. (Practice) Convert the following numbers from scientific notation into standard decimal form:
   a. $2.67 \times 10^3$
   b. $2.67 \times 10^{-3}$
   c. $1.872 \times 10^9$
   d. $1.872 \times 10^{-9}$
   e. $2.627 \times 10^3$
   f. $6.6256 \times 10^{-34}$ (known as Planck's constant)

3. (Practice) Write the following decimal numbers using scientific notation:
   a. 16
   b. 656.23
   c. 3426.95
   d. 4893.2
   e. .321
   f. .0123
   g. .006789

4. (Practice) Compute the following:
   a. $10^{-6} \times 10^3$
   b. $10^4 \times 10^{-6} \times 10^3 \times 10^{12}$
   c. $10^2 \times 10^7 \times 10^4$
   d. $10^4 \times 10^{-6} \times 10^5 \times 10^{12}$
   d. $10^3 \times 10^7 \times 10^{-4}$
   f. $10^{-6} \times 10^{-5}$

5. (Practice) Compute the following:
   a. $2.8 \times 10^5 \times 1.6 \times 10^{-6} \times 3.2 \times 10^{-3}$
   b. $1.4 \times 10^{-2} \times 2.5 \times 10^5 \times 5.3104$
   c. $3.2 \times 10^4 \times 1.8 \times 10^{-6} \times 2.7 \times 10^3$
   d. $4.5 \times 10^4 \times 1.8 \times 10^{-6} \times 6.7 \times 10^{-3}$
   e. $7.1 \times 10^3 \times 8.45 \times 10^{-7} \times 3.67104$
   f. $9.89 \times 10^{-6} \times 6.28 \times 10^{-5}$

6. (Aeronautics) The initial acceleration, $a$, of a rocket fired from earth, with an initial thrust, $T$, is given by this formula:

```
a = \frac{T-mg}{m}
```

$a$ is the initial acceleration.
$T$ is the thrust in Newtons.
$m$ is the mass in kg.
$g$ is the acceleration caused by gravity in $m/s^2$.

   a. Determine the units of the initial acceleration by calculating the units resulting from the right side of the equation. (Hint. As listed in Table 1.1, a Newton is $N = kg \cdot m/s^2$).

   b. Determine the initial acceleration of a rocket having a mass of $5 \times 10^4$ kg and an initial thrust of $6 \times 10^5$ Newtons. The value of $g$ is $9.81$ $m/s^2$.

7. (Heat Transfer) The energy radiated from the surface of the sun or a planet in the solar system can be calculated using Stefan-Boltzmann's Law:
$E = \sigma T^4$

$E$ is the radiated energy.
$\sigma$ is Stefan-Boltzmann's constant ($5.6697 \times 10^{-8}$ $W/m^2K^4$).
$T$ is the surface temperature in Kelvin ($^\circ C + 273$).

   a. Determine the units of $E$ by calculating the units resulting from the right side of the formula.

   b. Determine the energy radiated from the sun's surface, given that the sun's average temperature is approximately $6,000$K.

## Preliminary Three: Software Development

A computer is a machine, and like other machines, such as an automobile or a lawnmower, it must be turned on and then driven, or controlled, to perform the task it was meant to. In an automobile, control is provided by the driver, who sits inside the car and directs it. In a computer, drive is a set of instructions called a program. More, a computer program is a self-contained set of instructions used to operate a computer to produce a specific result. Another term for a set of programs is software, and both are used interchangeably throughout this.

At most basic level, a program is a solution developed to solve a particular problem, written in a format that can be executed on a computer. Therefore, writing a program is almost the last step in a process that determines the problem to be solved and the method to be used in the solution. Each field of study has its own name for the systematic method of designing solutions to solve problems. In science and engineering, the approach is referred to as the scientific method, and in quantitative analysis, the approach is called the systems approach. Professional software developers use the software development procedure for
