The method is declared private so only code within this class can use it. For simple programs, that's all of the code anyway so this isn't an issue.

The method's data type is long so it must return a value of type long.

The method's name is Factorial. You should try to give each method a name that is simple and that conveys the method's purpose so it's easy to remember what it does.

The method takes a single parameter of type long named value. Parameters have method scope so value is only defined inside the method. In that sense parameters are similar to variables declared inside the method.

The method creates a variable result and multiplies it by the values 2, 3, ..., value.

The method finishes by executing the return statement, passing it the final value of result.

The following code shows how a program might call the Factorial method:

```
```
long number = long.Parse(numberTextBox.Text);
long answer = Factorial(number);
resultTextBox.Text = answer.ToString();
```
```

This code starts by creating a long variable named number and initializing it to whatever value is in numberTextBox.

The code then calls the Factorial method, passing it the value number and saving the returned result in the new long variable named answer.

Notice that the names of the variables in the calling code (number and answer) have no relation to the names of the parameters and variables used inside the method (value and result). The method's parameter declaration determines the names the parameters have while inside the method.

The code finishes by displaying the result.

A method's parameter list can include zero, one, or more parameters separated by commas. For example, the following code defines the method Gcd, which returns the greatest common divisor (GCD) of two integers. (The GCD of two integers is the largest integer that evenly divides them both.)

```
```
// Calculate GCD(a, b).
private long Gcd(long a, long b)
{
    long remainder;
    do
    {
        remainder = a % b;
        if (remainder != 0)
        {
            a = b;
            b = remainder;
        }
    } while (remainder > 0);

    return b;
}
```
```