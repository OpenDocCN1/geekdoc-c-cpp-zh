
```csharp
try
{
    int leftHandSide = int.Parse(lhsOperand.Text);
    int rightHandSide = int.Parse(rhsOperand.Text);
    int answer = doCalculation(leftHandSide, rightHandSide);
    result.Text = answer.ToString();
}
catch (Exception ex) // this is a general catch
{
    ...
}
catch
{
    ...
}
```

```csharp
bool catchErrors = ...;
try {
    catch (Exception ex) when (catchErrors == true) {
        // Only handle exceptions if the catchErrors variable is true
        try {
            int lhs = int.Parse(lhsOperand.Text);
            int rhs = int.Parse(rhsOperand.Text);
            int outcome = 0;
            outcome = lhs + rhs;
            expression.Text = `${lhs} + ${rhs}`;
            result.Text = outcome.ToString();
        }
        catch (FormatException fex) {
            result.Text = fex.Message;
        }
    }
}
```

```csharp
private void addValues() {
    int leftHandSide = int.Parse(lhsOperand.Text);
    int rightHandSide = int.Parse(rhsOperand.Text);
    int outcome = 0;
    outcome = lhs + rhs;
    expression.Text = lhsOperand.Text + " + " + rhsOperand.Text;
    result.Text = outcome.ToString();
}
```

```csharp
private void calculateClick(object sender, RoutedEventArgs e)
{
    try
    {
        if ((bool)addition.IsChecked)
        {
            addValues();
        } else if ((bool)subtraction.IsChecked)
        {
            subtractValues();
        } else if ((bool)multiplication.IsChecked)
        {
            multiplyValues();
        } else if ((bool)division.IsChecked)
        {
            divideValues();
        } else if ((bool)remainder.IsChecked)
        {
            remainderValues();
        }
    } catch (FormatException fEx)
    {
        result.Text = fEx.Message;
    }
    int number = int.MaxValue;
    int willThrow = number++;
    Console.WriteLine("this");
    int number = int.MaxValue;
    int willThrow = number++;
    Console.WriteLine("this be reached");
    int willThrow = unchecked(int.MaxValue + 1);
}
```

```csharp
public static string monthName(int month)
{
    switch (month) {
        case 1:
            return "January";
        case 2:
            return "February";
        ...
        case 12:
            return "December";
        default:
            throw new ArgumentOutOfRangeException("Bad month");
    }
}
```

```csharp
switch (current)
{
    case '<' :
        target.Text += "<";
        break;
    default:
        target.Text += current;
        break;
    case '>' :
        target.Text += ">";
        break;
    case '&' :
        target.Text += "&";
        break;
    case '"':
        target.Text += "\"";
        break;
    case '\'' :
        target.Text += "'";
        break;
}
inRange = (lo <= number) && (hi >= number);
inRange = (lo < number) && (hi <= hi);
outOfRange = (number < lo) || (hi > number);
if (inRange)
    process();
if (seconds == 59)
{
    seconds = 0;
    minutes++;
}
```

```csharp
switch (current)
{
    case 0:
        ...
        break;
    case 1:
        ...
        break;
    default:
        ...
        break;
}
string name = "John";
string greeting = "Hello ";
greeting += name;
Console.WriteLine(greeting);
count += 1;
while (booleanExpression)
int i = 0;
while (i < 10)
{
    Console.WriteLine(i);
    i++;
}
```

```csharp
TextReader reader = new StreamReader(inputStream);
displayData(reader);
private void displayData(TextReader reader)
{
    // TODO: add while loop
    while (line != null)
    {
        source.Text += line + '\n';
        line = reader.ReadLine();
    }
}
```

```csharp
initialization (Boolean expression)
{
    update variable
    for (int i = 0; i < 10; i++)
    {
        Console.WriteLine(i);
    }
}
for (int i = 0; i++)
{
    Console.WriteLine("somebody me!");
}
int i = 0; i < 10; i++
{
    Console.WriteLine(i);
    i++;
}
for (int i = 0, j = 10; i <= j; i++)
{
    ...
}
string line = reader.ReadLine(); line != null
{
    source.Text += line + '\n';
}
```

```csharp
do (booleanExpression)
int i = 0;
do
{
    Console.WriteLine(i);
    i++;
} while (i < 10);
int i = 0;
while (true)
{
    Console.WriteLine(i);
    i++;
    if (i < 10)
    continue;
    else
    break;
}
```

```csharp
private void showClick(object sender, RoutedEventArgs e)
{
    int amount = int.Parse(number);
    steps.Text = "";
    string current = "";
}
private void showClick(object sender, RoutedEventArgs e)
{
    int amount = int.Parse(number);
    steps.Text = "";
    string current = "";
    do
    {
        int nextDigit = amount % 8;
        amount /= 8;
        int digitCode = '0' + nextDigit;
        char digit = Convert.ToChar(digitCode);
        current = digit + current;
        steps.Text += current + "\n";
    } while (amount != 0);
}
```

```csharp
try
{
    int leftHandSide = int.Parse(lhsOperand.Text);
    int rightHandSide = int.Parse(rhsOperand.Text);
    int answer = doCalculation(leftHandSide, rightHandSide);
    result.Text = answer.ToString();
}
catch (FormatException fEx)
{
    // Handle the exception
    ...
}
try
{
    int leftHandSide = int.Parse(lhsOperand.Text);
    int rightHandSide = int.Parse(rhsOperand.Text);
    int answer = doCalculation(leftHandSide, rightHandSide);
    result.Text = answer.ToString();
}
catch (FormatException fEx)
{
    ...
}
catch (OverflowException oEx)
{
    ...
}
```
