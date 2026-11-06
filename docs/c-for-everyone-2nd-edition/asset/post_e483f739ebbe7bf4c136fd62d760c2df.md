
## P2.19 Printing a grid

Write a program that prints the following grid to play tic-tac-toe.

```
+---+---+---+
|   |   |   |
+---+---+---+
|   |   |   |
+---+---+---+
|   |   |   |
+---+---+---+
```

Of course, you could simply write seven statements of the form

```cpp
cout << "+---+---+---+";
```

You should do it the smart way, though. Define string variables to hold two kinds of patterns: a comb-shaped pattern

```
+---+---+---+
|   |   |   |
```

and the bottom line. Print the comb three times and the bottom line once.

## P2.20

Write a program that reads an integer and breaks it into a sequence of individual digits. For example, the input 16384 is displayed as

```
1 6 3 8 4
```

You may assume that the input has no more than five digits and is not negative.

## P2.21

Write a program that reads two times in military format (0900, 1730) and prints the number of hours and minutes between the two times. Here is a sample run. User input is in color.

```
Please enter the first time: 0900
Please enter the second time: 1730
8 hours 30 minutes
```

Extra credit if you can deal with the case where the first time is later than the second:

```
Please enter the first time: 1730
Please enter the second time: 0900
15 hours 30 minutes
```

## P2.22 Writing large letters

A large letter H can be produced like this:

```
*   *
*   *
*****
*   *
*   *
```

It can be defined as a string constant like this:

```cpp
const string LETTER_H =
   "*   *\n*   *\n*****\n*   *\n*   *\n";
```

(The \n character is explained in Special Topic 1.1.) Do the same for the letters E, L, and O. Then write the message

```
H
E
L
L
O
```

in large letters.

## P2.23

Write a program that transforms numbers 1, 2, 3, …, 12 into the corresponding month names January, February, March, …, December. *Hint:* Make a very long string "January February March …", in which you add spaces such that each month name has the same length. Then use `substr` to extract the month you want.

![](img/23fb3582e93ebc95909e1de029c3d388_97_0.png)

## Engineering P2.24

Consider the following circuit.

![](img/23fb3582e93ebc95909e1de029c3d388_97_1.png)

Write a program that reads the resistances of the three resistors and computes the total resistance, using Ohm’s law.

## Engineering P2.25

The dew point temperature \(T_d\) can be calculated (approximately) from the relative humidity \(RH\) and the actual temperature \(T\) by

\[
T_d = \frac{b \cdot f(T, RH)}{a - f(T, RH)}
\]

\[
f(T, RH) = \frac{a \cdot T}{b + T} + \ln(RH)
\]

where \(a = 17.27\) and \(b = 237.7^\circ\text{C}\). Write a program that reads the relative humidity (between 0 and 1) and the temperature (in degrees C) and prints the dew point value. Use the C++ function `log` to compute the natural logarithm.

## Engineering P2.26

The pipe clip temperature sensors shown here are robust sensors that can be clipped directly onto copper pipes to measure the temperature of the liquids in the pipes.

![](img/23fb3582e93ebc95909e1de029c3d388_97_2.png)

Each sensor contains a device called a *thermistor*. Thermistors are semiconductor devices that exhibit a temperature-dependent resistance described by:

\[
R = R_0 e^{\beta\left(\frac{1}{T} - \frac{1}{T_0}\right)}
\]

where \(R\) is the resistance (in \(\Omega\)) at the temperature \(T\) (in °K), and \(R_0\) is the resistance (in \(\Omega\)) at the temperature \(T_0\) (in °K). \(\beta\) is a constant that depends on the material used to make the thermistor. Thermistors are specified by providing values for \(R_0\), \(T_0\), and \(\beta\).

The thermistors used to make the pipe clip temperature sensors have \(R_0 = 1075\ \Omega\) at \(T_0 = 85\ ^\circ\mathrm{C}\), and \(\beta = 3969\ ^\circ\mathrm{K}\). (Notice that \(\beta\) has units of °K. Recall that the temperature in °K is obtained by adding 273 to the temperature in °C.) The liquid temperature, in °C, is determined from the resistance \(R\), in \(\Omega\), using

\[
T = \frac{\beta T_0}{T_0\ln\left(\frac{R}{R_0}\right)+\beta}-273
\]

Write a C++ program that prompts the user for the thermistor resistance \(R\) and prints a message giving the liquid temperature in °C.

## Engineering P2.27

The circuit shown below illustrates some important aspects of the connection between a power company and one of its customers. The customer is represented by three parameters, \(V_t\), \(P\), and \(pf\). \(V_t\) is the voltage accessed by plugging into a wall outlet. Customers depend on having a dependable value of \(V_t\) in order for their appliances to work properly. Accordingly, the power company regulates the value of \(V_t\) carefully. \(P\) describes the amount of power used by the customer and is the primary factor in determining the customer’s electric bill. The power factor, \(pf\), is less familiar. (The power factor is calculated as the cosine of an angle, so its value will always be between zero and one.) In this problem you will be asked to write a C++ program to investigate the significance of the power factor.

![](img/23fb3582e93ebc95909e1de029c3d388_98_0.png)

![](img/23fb3582e93ebc95909e1de029c3d388_98_1.png)

In the figure, the power lines are represented, somewhat simplistically, as resistances in Ohms. The power company is represented as an AC voltage source. The source voltage, \(V_s\), required to provide the customer with power \(P\) at voltage \(V_t\) can be determined using the formula

\[
V_s = \sqrt{\left(V_t + \frac{2RP}{V_t}\right)^2 + \left(\frac{2RP}{pf\,V_t}\right)^2(1-pf^2)}
\]

(\(V_s\) has units of Vrms.) This formula indicates that the value of \(V_s\) depends on the value of \(pf\). Write a C++ program that prompts the user for a power factor value and

## Answers to Self-Check Questions

1. One possible answer is

   ```cpp
   int bottles_per_case = 8;
   ```

   You may choose a different variable name or a different initialization value, but your variable should have type `int`.

2. There are three errors:
   - You cannot have spaces in variable names.
   - The variable type should be `double` because it holds a fractional value.
   - There is a semicolon missing at the end of the statement.

3.

   ```cpp
   double unit_price = 1.95;
   int quantity = 2;
   ```

4. `cout << "Total price: " << unit_price * quantity << endl;`

5. Change the definition of `cans_per_pack` to

   ```cpp
   int cans_per_pack = 4;
   ```

6. You need to use a `*/` delimiter to close a comment that begins with a `/*`:

   ```cpp
   double can_volume = 0.355; /* Liters in a 12-ounce can */
   ```

7. The program would compile, and it would display the same result. However, a person reading the program might find it confusing that fractional cans are being considered.

8. Its value is modified by the assignment statement.

9. Assignment would occur when one car is replaced by another in the parking space.

10. `double interest = balance * p / 100;`

11. `double side_length = sqrt(area);`

12.

   ```cpp
   4 * PI * pow(radius, 3) / 3
   or (4.0 / 3) * PI * pow(radius, 3),
   but not (4 / 3) * PI * pow(radius, 3)
   ```

13. 172 and 9

14. `int leftover = 12 - amount % 12;`

15. There is no prompt that alerts the program user to enter the quantity.

16. The `unit_price` variable is defined as an `int`. If the user were to enter a price such as 1.95, only the 1 would be placed into the variable.

17. The output is

   ```text
   The total volume is20
   ```

   Note that there is no space between the `is` and `20`.

18. `cout << "$" << fixed << setprecision(2) << total_price;`

19.

   ```cpp
   cout << "Bottles: " << setw(8) << bottles << endl
        << "Cans: " << setw(8) << cans << endl;
   ```

   Note that the `setw` manipulator appears twice. Also note the added spaces in the string "Cans: ".
