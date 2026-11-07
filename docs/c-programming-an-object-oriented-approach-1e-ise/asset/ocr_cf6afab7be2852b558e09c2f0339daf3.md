# Program 6.27  Finding the future value of periodic investments (Continued)

```
```cpp
void input (double& invest, double& rate, double& term)
{
    invest = getInput ("Enter the value of periodic investment: ");
    rate = getInput ("Enter the interest rate per year: ");
    term = getInput ("Enter the term (number of years): ");
}

/*
 * The process function calls findMultiplier to calculate the
 * the multiplier. It then multiplies the return value by the value
 * invested to find the future value.
 */
void process (double invest, double rate, double term,
              double& multiplier, double& futureValue)
{
    multiplier = findMultiplier (rate, term);
    futureValue = multiplier * invest;
}

/*
 * The output function calls printData to print three given values.
 * It then calls printResult to print the calculated values.
 */
void output (double invest, double rate, double term,
             double multiplier, double futureValue)
{
    printData (invest, rate, term);
    printResult (multiplier, futureValue);
}

/*
 * The getInput function gets the input from the user. Its
 * only parameter is an object of type string that contains
 * a different message in each call to force the user to input
 * the appropriate data. It then validates the data and sends it back
 * to the calling expression in the input function.
 */
double getInput(string message )
{
    double input;
    do
    {
        cout << message;
        cin >> input;
    } while (input < 0.0);
    return input;
```
```