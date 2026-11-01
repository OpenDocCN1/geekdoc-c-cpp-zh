```
result = firstNumber + secondNumber    ' Results in 123.5
result = firstNumber - secondNumber    ' Results in 76.5
result = firstNumber * secondNumber    ' Results in 2350
result = firstNumber / secondNumber    ' Results in 4.25531914893617
```

# C#

```
int firstNumber = 100;
float secondNumber = 23.5F;
double result = 0;

result = firstNumber + secondNumber;    // Results in 123.5
result = firstNumber - secondNumber;    // Results in 76.5
result = firstNumber * secondNumber;    // Results in 2350
result = firstNumber / secondNumber;    // Results in 4.25531914893617
```

Note that in the C# example you need to add the letter F to the value of 23.5. This tells the compiler you really want it to be a float rather than a double

VB.NET also supports the \ operator, which basically performs the division and then drops the remainder from the value, effectively rounding the return value down to the nearest integer.

# VB.NET

```
result = firstNumber \ secondNumber    ' Results in 4
```

C# doesn't have a special operator for this. However, when you try to divide two integers, the result is always an integer as well. This means that 7 (stored as an int) divided by 2 (stored as an int) will be 3. It's important to realize that this rounding occurs, or you may end up with unexpected results.

The final two operators need a bit more explanation. First, the ^ operator — for raising one number to the power of another — is available only in the VB.NET language:

# VB.NET

```
Dim result As Double

result = 2 ^ 3        ' Results in 8 (2 * 2 * 2)
result = 3 ^ 2        ' Results in 9 (3 * 3)
```

C# doesn't support this operator, but you can easily replicate its behavior using Math.Pow, which is made available by the .NET Framework. The following code snippet is functionally equivalent to the preceding one:

# C#

```
result = Math.Pow(2, 3);    // Results in 8 (2 * 2 * 2)
result = Math.Pow(3, 2);    // Results in 9 (3 * 3)
```

Of course Math.Pow is available to VB.NET as well, so if you're using that language, you have two options to choose from.

The final operator is called the modulus operator. It returns the remainder of the division of two numbers, like this:

# VB.NET

```
Dim firstNumber As Integer = 17
Dim secondNumber As Integer = 3
```