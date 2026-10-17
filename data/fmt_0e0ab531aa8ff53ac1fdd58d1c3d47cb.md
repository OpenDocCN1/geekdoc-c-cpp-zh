
    // ...

    return leftHandSide + rightHandSide;

}

void showResult(int answer) {

    // 显示答案

    Console.WriteLine($"The answer is {answer}");

    return;

}

```csharp

int addValues(int leftHandSide, int rightHandSide) => leftHandSide + rightHandSide;

void showResult(int answer) => Console.WriteLine($"The answer is {answer}");

private int addValues(int leftHandSide, int rightHandSide)

expression.Text = `$(leftHandSide) + ${rightHandSide}`;

return leftHandSide + rightHandSide;

```

```csharp

private void showResult(int answer) => result.Text = answer.ToString();

    result = methodName ( argumentList )

    int addValues(int leftHandSide, int rightHandSide)

    // ...

```

```csharp

addValues(); // 编译错误，缺少括号

addValues(); // 编译错误，参数不足

addValues(39); // 编译错误，参数不足

addValues("39") // 编译错误，参数类型错误

int result = addValues(39, 3); // 在赋值的右侧

showResult(addValues(39, 3)); // 作为另一个方法调用的参数

int leftHandSide = System.Int32.Parse(lhsOperand.Text);

int rightHandSide = System.Int32.Parse(rhsOperand.Text);

calculatedValue = addValues(leftHandSide, rightHandSide);

```
*(注：后续重复的相似代码块逻辑一致，已根据要求保留格式并仅翻译其中注释/结构)*

```csharp

public void DoWorkWithData(int intData, float floatData)

{

    ...

}

int arg1 = 99;

float arg2 = 100.0F;

int arg3 = 101;

DoWorkWithData(arg1, arg2, arg3); // 调用三个参数的重载

DoWorkWithData(arg1, arg2); // 调用两个参数的重载

public void DoWorkWithData(int intData)

{

    ...

}

public void DoWorkWithData(int moreIntData)

{

    ...

}

void optMethod(int first, double second = 0.0, string string_ = "Hello") {

    optMethod(99, 123.45, "World"); // 为三个参数都提供了参数

    optMethod(100, 54.321); //仅为前两个参数提供了参数

    optMethod(first : 99, second : 123.45, third : "World");

    optMethod(first : 100, second : 54.321);

    optMethod(third : "World", second : 123.45, first : 99);

    optMethod(second : 54.321, first : 100);

    optMethod(third : "54.321", second : 123.45, first : 99);

    optMethod(second : 54.321, first : 99, third : "World");

    optMethod(99, third : "World"); // 第一个参数是位置参数

}

void optMethod(int first, double second = 0.0, string string_ = "Hello") {

}

void optMethod(int first, double second = 1.0, string string_ = "Goodbye", int fourth = 100)

{

    optMethod(1, third : "World");

    optMethod(1);

    optMethod(second : 2.5, first : 1);

}

private double calculateFee(double dailyRate = 500.0, int noOfDays = 1) {{

    Console.WriteLine("calculateFee 使用两个可选参数");

    return dailyRate * noOfDays;

}

private double calculateFee(double dailyRate = 500.0)

{

    Console.WriteLine("calculateFee 使用一个可选参数");

    int defaultNoOfDays = 1;

    return dailyRate * defaultNoOfDays;

}

private double calculateFee()

{

    Console.WriteLine("calculateFee 使用硬编码值");

    double defaultDailyRate = 400.0;

    int defaultNoOfDays = 1;

    return defaultDailyRate * defaultNoOfDays;

}

public void run()

{

    double fee = calculateFee();

    Console.WriteLine($"Fee is {fee}");

}

// 使用硬编码值 calculateFee

// Fee is 400

public void run()

{

    double fee = calculateFee(650.0);

    Console.WriteLine($"Fee is {fee}");

}

// 使用一个可选参数 calculateFee

// Fee is 650

public void run()

{

    double fee = calculateFee(500.0, 3);

    Console.WriteLine($"Fee is {fee}");

}

// 使用两个可选参数 calculateFee

// Fee is 1500

public void run()

{

    double fee = calculateFee(dailyRate : 375.0);

    Console.WriteLine($"Fee is {fee}");

}

// 使用一个可选参数 calculateFee

// Fee is 375

public void run()

{

    double fee = calculateFee(noOfDays : 4);

}

// 使用两个可选参数 calculateFee

// Fee is 2000

private double calculateFee(double dailyRate = 500.0, int noOfDays = 1)

{

    Console.WriteLine("calculateFee 使用两个可选参数");

    return dailyRate * noOfDays;

}

public void run()

{

    double fee = calculateFee(dailyRate : 375.0);

    Console.WriteLine($"Fee is {fee}");

}

// 使用一个可选参数 calculateFee

// Fee is 375

public void run()

{

    double fee = calculateFee(noOfDays : 4);

}

// 使用两个可选参数 calculateFee

// Fee is 2000

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

int i = 0;

while (i < 10)

{

    Console.WriteLine(i);

}

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

for (int i = 0; i < 10; i++)

{

    ...

    Console.WriteLine(j); // compile-time error

}

for (int i = 0; i < 10; i++)

{

    ...

}

for (int i = 0; i < 20; i += 2) // okay

{

    ...

}

for (int i = 0; i < 10; i++)

{

    ...

}

for (int i = 0; i < 20; i += 2) // okay

{

    ...

}

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

store the decimal number in the variable

do the following

div by 8 and store the remainder

set dec to the quotient from the previous step

while dec is not equal to zero

combine the values for each calculation in reverse order

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

    char digit = Convert.ToChar(digitCode);

    int amount = int.Parse(number);

    int i = 0; while (i < 10)

    {

        Console.WriteLine(i);

        i++;

    }

    for (int i = 0; i < 10; i++)

    {

        Console.WriteLine(i);

    }

    int i = 0;

    do

    {

        Console.WriteLine(i);

        i++;

    } while (i < 10);

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
