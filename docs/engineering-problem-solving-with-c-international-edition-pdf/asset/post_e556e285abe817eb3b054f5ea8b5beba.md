
\frac{f(a) - f(b)}{b - a} = \frac{f(a) - f(c)}{c - a}

![](img/f2bfa570e453b020c16e048c79a3ea0e_128_0.png)

Figure 3.7 Similar triangles.

that have been connected with straight-line segments and that have been connected with cubic degree polynomial segments. It should be clear that the values determined for the function between sample points depend on the type of interpolation that we select. In this section, we discuss linear interpolation.

A graph with two arbitrary data points f(a) and f(c) is shown in Figure 3.7. If we assume that the function between the two points can be estimated by a straight line, we can then compute the function value at any point f(b) using an equation derived from similar triangles:

f(b) = f(a) + \frac{b - a}{c - a} [f(c) - f(a)] .

Recall that we are also assuming that a < b < c.

To illustrate using this interpolation equation, assume that we have a set of temperature measurements taken from the cylinder head in a new engine that is being tested for possible use in a race car. These data are plotted with straight lines connecting the points in Figure 3.8, and they are also listed here:

![](img/f2bfa570e453b020c16e048c79a3ea0e_128_1.png)

Figure 3.8 Cylinder head temperatures.

| Time, s | Temperature, degrees F |
|---|---|
| 0.0 | 0.0 |
| 1.0 | 20.0 |
| 2.0 | 60.0 |
| 3.0 | 68.0 |
| 4.0 | 77.0 |
| 5.0 | 110.0 |

Assume that we want to interpolate a temperature to correspond to the value 2.6 seconds. We then have the following situation:

| a | 2.0 | f(a) | 60.0 |
|---|---|---|---|
| b | 2.6 | f(b) | ? |
| c | 3.0 | f(c) | 68.0 |

Using the interpolation formula, we have

```
f(b) = f(a) + \frac{b-a}{c-a} [f(c) - f(a)]
= 60.0 + \frac{2.6 - 2.0}{3.0 - 2.0} [68.0 - 60.0]
= 64.8.
```

In this example, we used linear interpolation to find the temperature that corresponds to a specified time. We could also interchange the roles of temperature and time so that we plot temperature on the x-axis and time on the y-axis. In this case, we can use the same process to compute the time that a specified temperature occurred, assuming that we have a pair of data points with temperatures below and above the specified temperature.

### Practice!

- 1. Use your calculator to compute temperatures at the following times, using linear interpolation:
- 0.3, 1.25, 2.36, 4.48

- 2. Use your calculator to compute time values that correspond to the following temperatures, using linear interpolation:
- 81, 96, 100, 106

- 3. Suppose Problem 2 asked you to compute the time value that corresponds to the temperature 110 degrees Fahrenheit. What complicates this problem? How many time values correspond to the temperature 110 degrees Fahrenheit? Find each of the corresponding time values, using linear interpolation. (You may want to refer to Figure 3.10, which contains a plot of these data with the temperature data on the x-axis and the time values on the y-axis.)

![](img/f2bfa570e453b020c16e048c79a3ea0e_130_0.png)

Figure 3.9 Temperature values.

![](img/f2bfa570e453b020c16e048c79a3ea0e_130_1.png)

Figure 3.10 Time values.

## 3.6 Problem Solving Applied: Freezing Temperature of Seawater

In this section, we use linear interpolation to solve a problem related to the salinity of seawater. Recall from the chapter opening discussion that the salinity of seawater is a measure of the amount of dissolved material in the seawater. Salinity varies from one location to another in the ocean, but typically falls in the range of 33 to 38 parts per thousand (ppt), or a percentage of 3.3 to 3.8.

Salinity is often measured using an instrument that measures the electrical conductivity of the water; the more dissolved materials in the water, the better it conducts electricity. Measurements of salinity are especially important in colder regions because the temperature at which seawater freezes is dependent upon its salinity. The following table contains a set of salinity measurements and corresponding freezing temperatures; the values are also plotted in Figure 3.11

| Salinity (ppt) | Freezing Temperature (degrees F) |
|---|---|
| 0 (fresh water) | 32 |
| 10 | 31.1 |
| 20 | 30.1 |
| 24.7 | 29.6 |
| 30 | 29.1 |
| 35 | 28.6 |

Assume that we would like to use linear interpolation to determine the freezing temperature of water for which we have measured the salinity. Write a program that allows the user to enter the data for two points and a salinity measure between those points. The program should verify that the value entered for the salinity lies between the values entered for the salinity of the two data points. If the input data is valid, the program should compute the corresponding freezing temperature. If the data is invalid, the program should print an error message and the invalid data.

![](img/f2bfa570e453b020c16e048c79a3ea0e_131_0.png)

Figure 3.11 Freezing temperature of seawater.

### 1. PROBLEM STATEMENT

Use linear interpolation to compute a new freezing temperature for water with a specified salinity.

### 2. INPUT/OUTPUT DESCRIPTION

The following diagram shows that the input to the program includes two consecutive points (a, f(a)) and (c, f(c)) and the new salinity measurement b. The output is the new freezing temperature.

![](img/f2bfa570e453b020c16e048c79a3ea0e_132_0.png)

### 3. HAND EXAMPLE

Suppose that we want to determine the freezing temperature for water with a salinity measurement of 33 ppt. From the data, we see that this point falls between 30 and 35 ppt:

| a | 30 | 29.1 | f(a) |
|---|---|---|---|
| b | 33 | ? | f(b) |
| c | 35 | 28.6 | f(c) |

Using the linear equation formula, we can compute f(b):

```
f(b) = f(a) + (b - a) / (c - a) . (f(c) - f(a))
= 29.1 + 3/5 . (28.6 - 29.1)
= 28.8
```

As expected, this value falls between f(a) and f(c).

### 4. ALGORITHM DEVELOPMENT

The first step in the development of an algorithm is the decomposition of the problem solution into a set of sequentially executed steps:

*Decomposition Outline*

- 1. Read the coordinates of the adjacent points and the new salinity value.
- 2. Validate input.
- 3. Compute the new freezing temperature.
- 4. Print the new freezing temperature.

The second step in the decomposition outline requires a selection structure. If the value entered for the salinity does not lie between the salinity values of the two data points, an error message will be printed, along with the erroneous data, and the program will terminate. The following refinement, described in a flowchart, outlines these steps.

The steps in the flowchart are now detailed enough to convert into C++. We will use an if statement to implement the selection structure.

![](img/f2bfa570e453b020c16e048c79a3ea0e_133_0.png)

```
/*........................................................................*/
/* Program chapter3_2                                                */
/*                                                                   */
/* This program uses linear interpolation to                         */
/* compute the freezing temperature of seawater.                     */
/*                                                                   */
#include<iostream>    //Required for cin, cout, endl.
#include<iomanip>     //Required for fixed, setprecision()
using namespace std;
int main()
{
   // Declare objects.
   double a, f_a, b, f_b, c, f_c;

   // Prompt and get user input from the keyboard.
   cout << "Use ppt for salinity values." << endl
        << "Use degrees F for temperatures." << endl
        << "Enter first salinity and freezing temperature: \\n";
   cin >> a >> f_a;
   cout << "Enter second salinity and freezing temperature: \\n";
   cin >> c >> f_c;
   cout << "Enter new salinity: \\n";
   cin >> b;
   if ( !(a < b && b < c) )
   {
      cout << "Invalid data: " << a << ",\\n"
           << b << "\",\\"" << c << endl;
   }
   else
   {
      // Use linear interpolation to compute
      // new freezing temperature.
      f_b = f_a + (b-a)/(c-a)*(f_c - f_a);

      // Print new freezing temperature to the screen.
      cout << "New freezing temperature in degrees F: "
           << fixed << setprecision(1) << f_b << endl;
   } // end else

   // Exit program.
   return 0;
}
```

### 5. TESTING

We first test the program using the data from the hand example. This generates the following interaction:

Use ppt for salinity values.
Use degrees F for temperatures.
Enter first salinity and freezing temperature:
30 29.1
Enter second salinity and freezing temperature:
35 28.6
Enter new salinity:
33
New freezing temperature in degrees F: 28.8

The value computed matches the hand example, so we can then test the program with other time values. If the new coefficient value had not matched the result from the hand example, we would then need to determine if the error is in the hand example or in the C++ program.
