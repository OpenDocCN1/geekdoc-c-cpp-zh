
A basic property of complex numbers is that

$e^{i\theta} = \cos \theta + i \sin \theta$

and thus an alternative form of the polar representation of a complex number is

$r e^{i\theta}$

Now consider two complex numbers

$z = r_1 e^{i\theta_1}$

$w = r_2 e^{i\theta_2}$

The familiar properties of exponents then give

$z \cdot w = (r_1 e^{i\theta_1})(r_2 e^{i\theta_2}) = r_1 r_2 e^{i(\theta_1 + \theta_2)}$

which agrees with the geometric representation of the product of two complex numbers shown earlier. In the same manner, we can use polar representation and properties of exponents to show that the quotient of two complex numbers corresponds to a vector whose magnitude is the quotient of the magnitudes of the vectors representing the numbers and whose angle of inclination is the difference of the vectors’ angles of inclination:

$z / w = (r_1 e^{i\theta_1}) / (r_2 e^{i\theta_2}) = (r_1 / r_2) e^{i(\theta_1 - \theta_2)}$

These basic arithmetic operations for complex numbers are defined in C++’s complex number classes and are denoted by the usual arithmetic operators +, -, *, and /; + and - may also be used as unary operators. Also defined are the assignment operator = along with assignment shortcuts +=, -=, *=, and /= and the logical operations == and !=.

The input and output operators << and >> have also been overloaded for the three complex types. Complex values are output in the form (a, b), where a is the real part and b is the imaginary part. They can be input in the form a or (a) if the imaginary part is 0 and (a, b) otherwise.

In addition to these operations, C++ defines several functions for its complex classes. The following table describes some of the more useful ones. In the descriptions, z is a complex number a + bi.

## COMPLEX FUNCTIONS

|  |  |
|---|---|
| Real part of z | real(z) returns the real part of z |
|  | z.real(a) assigns a to the real part of z |
| Imaginary part of z | imag(z) returns the imaginary part of z |
|  | z.imag(b) assigns b to the imaginary part of z |

6 <, >, ≤, and ≥ are not defined for complex numbers.

|  |  |
|---|---|
| Phase angle of z: θ | arg(z) |
| Norm of z: a² + b² | norm(z) |
| Absolute value (or magnitude) of z: | abs(z) |
| |z| = √a² + b² |  |
| Conjugate of z: z̄ = a − bi | conj(z) |
| Power: zʳ, where r is a real value | pow(z, r) |
| Square root | sqrt(z) |
| Trig Functions | cos(z), sin(z), tan(z), |
| Hyperbolic Functions | cosh(z), sinh(z), tanh(z), |
| Exponential Function: eᶻ | exp(z) |
| Logarithms—natural, base-10 | log(z), log10(z) |

## 7.5.3 Example: Solving Quadratic Equations

In Section 5.4 we considered the problem of solving quadratic equations, using the if statement to check if there were real roots and if not, display a message. The program in Example 7.2 is a variation of the program in Example 5.4 that finds the roots—possibly complex—of any quadratic equation.

### Example 7.2 Quadratic Equation Solver—Complex Roots

```
/* This program solves quadratic equations using the quadratic formula.

    Input: the three coefficients of a quadratic equation
    Output: the complex roots of the equation
-------------------------------------------------------------------*/

#include <iostream>      // cout, cin, <<, >>
#include <complex>       // complex types
using namespace std;

int main()
{
    complex<double> a, b, c;
    cout << "Enter the coefficients of a quadratic equation: ";
    cin >> a >> b >> c;

    complex<double> discriminant = b*b - 4.0*a*c,
                    root1, root2;
    root1 = (-b + sqrt(discriminant)) / (2.0*a);
    root2 = (-b - sqrt(discriminant)) / (2.0*a);
    cout << "Roots are " << root1 << " and " << root2 << endl;
}
```

### SAMPLE RUNS:

Enter the coefficients of a quadratic equation: 1 4 3
Roots are (-1,0) and (-3,0)

Enter the coefficients of a quadratic equation: 2 0 -8
Roots are (2,0) and (-2,0)

Enter the coefficients of a quadratic equation: 2 0 8
Roots are (0,2) and (-0,-2)

Enter the coefficients of a quadratic equation: 1 2 3
Roots are (-1,1.41421) and (-1,-1.41421)

Enter the coefficients of a quadratic equation: (1,2) (3,4), (5,6)
Roots are (-0.22822,0.63589) and (-1.97178,-0.23589)

## 7.5.4 Application: A-C Circuits

The following a-c circuit contains a capacitor, an inductor, and a resistor in series:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_253_0.png)

The impedance Z_R for a resistor is simply the resistance R (in ohms), but for inductors and capacitors, it is a function of the frequency. The impedance Z_L of an inductor is the complex value given by

```
Z_L = ω L i
```

where ω is the frequency (in radians per second) of the a-c source, and L is the self-inductance (in henrys). For a capacitor, the impedance is

```
Z_C = -i / (ω C)
```

where C is the capacitance (in farads). The total impedance Z is then given by

```
Z = Z_R + Z_L + Z_C
```

and the current I (in amperes) by

```
I = V / Z
```

The program in Example 7.3 inputs the resistance, inductance, capacitance, the frequency of the a-c source, and the voltage, and then uses the preceding equations to calculate the current and output it.

### Example 7.3 Current in an A-C Circuit

```
/* This program computes the current in an a-c circuit containing a capacitor, an inductor, and a resistor in series.

Input: resistance, inductance, capacitance, frequency, voltage
Output: current
*/

#include <iostream>  // cin, cout, <<, >>
#include <complex>  // complex<double> type
#include <iomanip>  // format output
using namespace std;

int main()
{
  const complex<double> i = complex<double>(0, 1);
  double R,  // resistance (ohms)
  L,  // inductance (henrys)
  C,  // capacitance (farads)
  omega;  // frequency (radians per second)
  complex<double> V,  // voltage (volts)
  Z,  // total impedance
  I;  // current (amperes)
  cout << "\nEnter resistance (ohms), inductance (henrys),\n and capacitance (farads): ";
  cin >> R >> L >> C;
  cout << "\nEnter frequency (radians/second): ";
  cin >> omega;
  cout << "\nEnter voltage as a complex number in the form (x, y): ";
  cin >> V;
  // Calculate resistance using complex arithmetic
  Z = R + omega * L * i - i / (omega * C);
  // Calculate and display current using complex arithmetic
  I = V / Z;
  cout << fixed << setprecision(2)
       << "\nCurrent = " << real(I) << " + " << imag(I) << "I"
       << "\nwith magnitude = " << abs(I) << endl;
}
```

### SAMPLE RUN:

Enter resistance (ohms), inductance (henrys),
and capacitance (farads): 5000 .03 .02

Enter frequency (radians/second): 377

Enter voltage as a complex number in the form (x, y): (60000, 134)

Current = 12.00 + -0.00I
with magnitude = 12.00

## 7.6 SIMULATION WITH RANDOM NUMBERS: SHIELDING A NUCLEAR REACTOR

The term **simulation** refers to modeling a dynamic process and using this model to study the behavior of the process. The behavior of some *deterministic* processes can be modeled with an equation or a set of equations. For example, processes that involve exponential growth or decay are commonly modeled with an equation of the form $A(t) = A_0 e^{kt}$, where $A(t)$ is the amount of some substance $A$ present at time $t$, $A_0$ is the initial amount of the substance, and $k$ is a rate constant. In many problems, however, the process being studied can be modeled using *randomness*; for example, Brownian motion, the arrival of airplanes at an airport, the number of defective parts manufactured by a machine, and so on. Computer programs that simulate such processes use random number generators to introduce randomness into the values produced during execution.

## 7.6.1 Random Number Generators—The RandomInt Class

A **random number generator** is a function that produces a number selected at *random* from some fixed range in such a way that a sequence of these numbers tends to be uniformly distributed over the given range. Although it is not possible to develop an algorithm that produces truly random numbers, there are some methods that produce sequences of *pseudorandom numbers* that are adequate for most purposes. Most of these algorithms have two properties:

- 1. Some initial value called a *seed* is required to begin the process of generating random numbers. Different seeds will produce different sequences of random numbers.
- 2. Each random number produced is used in the computation of the next random number.

Although C++ does not provide a random number generator, its parent language C does. This can be used to construct a class RandomInt for data objects whose values are pseudorandom integers. (See the text’s website for more information about this class.)⁷

> ⁷ This RandomInt class was developed by Professor Joel Adams of Calvin College who was a coauthor of the text C++: An Introduction to Computing, 3/e, Pearson Education Inc., 2003.
