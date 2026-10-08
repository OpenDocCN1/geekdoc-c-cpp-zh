```
```
int main()
{
    double c = 0;        // declare input variable
    cin >> d;           // retrieve temperature to input variable
    double k = ctok("c");  // convert temperature
    Cout << k << '/n';  // print out temperature
}
```
```

+   3. Absolute zero is the lowest temperature that can be reached; it is −273.15°C, or 0K. The above program, even when corrected, will produce erroneous results when given a temperature below this. Place a check in the main program that will produce an error if a temperature is given below −273.15°C.

+   4. Do exercise 3 again, but this time handle the error inside `ctok()`.

+   5. Add to the program so that it can also convert from Kelvin to Celsius.

+   6. Write a program that converts from Celsius to Fahrenheit and from Fahrenheit to Celsius (formula in §4.3.3). Use estimation (§5.8) to see if your results are plausible.

+   7. Quadratic equations are of the form $ a \cdot x^{2} + b \cdot x + c = 0 $

To solve these, one uses the quadratic formula:
$ x = \frac{-b \pm \sqrt{b^{2} - 4ac}}{2a} $

There is a problem, though: if b²-4ac is less than zero, then it will fail. Write a program that can calculate x for a quadratic equation. Create a function that prints out the roots of a quadratic equation, given a, b, c. When the program detects an equation with no real roots, have it print out a message. How do you know that your results are plausible? Can you check that they are correct?

+   8. Write a program that reads and stores a series of integers and then computes the sum of the first N integers. First ask for N, then read the values into a vector, then calculate the sum of the first N values. For example:

"Please enter the number of values you want to sum:"

**3**

"Please enter some integers (press 'q' to stop):"

**12 23 13 24 15** |

"The sum of the first **3** numbers (**12 23 13**) is **48**."