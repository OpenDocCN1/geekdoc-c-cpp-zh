

private void showFloatValue()
{
    float floatVar;
    floatVar = 0.42F;
    value.Text = floatVar.ToString();
}

private void showIntValue()
{
    int intVar;
    intVar = 42;
    value.Text = intVar.ToString();
}

private void showDoubleValue()
{
    double doubleVar;
    doubleVar = 0.42;
    value.Text = doubleVar.ToString();
}

private void showBoolValue()
{
    bool boolVar;
    boolVar = false;
    value.Text = boolVar.ToString();
}

long moneyPaidToConsultant;
moneyPaidToConsultant = 750 * 20;

// 编译时错误
Console.WriteLine("Gillingham" - "Forest Green Rovers");

Console.WriteLine("43" + "1");

private void addValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: 将 rhs 加到 lhs 并将结果存储在 outcome 中
    expression.Text = $"{lhsOperand.Text} + {rhsOperand.Text}";
    result.Text = outcome.ToString();
}

private void addValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: 将 rhs 加到 lhs 并将结果存储在 outcome 中
    outcome = lhs + rhs;
    expression.Text = $"{lhsOperand.Text} + {rhsOperand.Text}";
    result.Text = outcome.ToString();
}

private void subtractValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: 从 lhs 中减去 rhs 并将结果存储在 outcome 中
    outcome = lhs - rhs;
    expression.Text = $"{lhsOperand.Text} - {rhsOperand.Text}";
    result.Text = outcome.ToString();
}

private void multiplyValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: 将 lhs 乘以 rhs 并将结果存储在 outcome 中
    outcome = lhs * rhs;
    expression.Text = $"{lhsOperand.Text} * {rhsOperand.Text}";
    result.Text = outcome.ToString();
}

private void divideValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: 将 lhs 除以 rhs 并将结果存储在 outcome 中
    outcome = lhs / rhs;
    expression.Text = $"{lhsOperand.Text} / {rhsOperand.Text}";
    result.Text = outcome.ToString();
}

private void remainderValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: 计算 lhs 除以 rhs 后的余数并将结果存储在 outcome 中
    outcome = lhs % rhs;
    expression.Text = $"{lhsOperand.Text} % {rhsOperand.Text}";
    result.Text = outcome.ToString();
}

int myInt;
myInt = 10; // 赋值表达式的值为 10

myInt5 = myInt4 = myInt3 = myInt2 = myInt = 10;

int myInt, myInt2, myInt3 = 10;

未分配局部变量 'myInt' 的使用
未分配局部变量 'myInt2' 的使用

int x;
x = 42;
Console.WriteLine(x++); // x 现在为 43，输出 42
x = 42;
Console.WriteLine(++x); // x 现在为 43，输出 43

var myVariable = 99;
var myOtherVariable = "Hello";

var yetAnotherVariable; // 错误 - 编译器无法推断类型

returnType methodName ( parameterList )
{
    // 方法体语句放在这里
}

int addValues(int leftHandSide, int rightHandSide)
{
    // ...
    // 方法体语句放在这里
    // ...
}

int addValues(int leftHandSide, int rightHandSide)
{
    // ...
    return leftHandSide + rightHandSide;
}

void showResult(int answer)
{
    // 显示答案
    Console.WriteLine($"The answer is {answer}");
    return;
}

int addValues(int leftHandSide, int rightHandSide) => leftHandSide + rightHandSide;
void showResult(int answer) => Console.WriteLine($"The answer is {answer}");

private int addValues(int leftHandSide, int rightHandSide)
{
    expression.Text = $"{leftHandSide} + {rightHandSide}";
    return leftHandSide + rightHandSide;
}

private void showResult(int answer) => result.Text = answer.ToString();

result = methodName ( argumentList )

int addValues(int leftHandSide, int rightHandSide)
{
    // ...
}

addValues;          // 编译时错误，无括号
addValues();        // 编译时错误，参数不足
addValues(39);      // 编译时错误，参数不足
addValues("39", "3"); // 编译时错误，参数类型错误

int result = addValues(39, 3);    // 赋值语句的右侧
showResult(addValues(39, 3));    // 作为另一个方法调用的参数

int leftHandSide = System.Int32.Parse(lhsOperand.Text);
int rightHandSide = System.Int32.Parse(rhsOperand.Text);

calculatedValue = addValues(leftHandSide, rightHandSide);

result.Text = answer.ToString();

private void calculateClick(object sender, RoutedEventArgs e)
{
    int calculatedValue = 0;
    ...
}

class Example
{
    void firstMethod()
    {
        int myVar;
        ...
    }
    void anotherMethod()
    {
        myVar = 42; // 错误 - 变量不在作用域中
        ...
    }
}

static void Main()
{
    Console.WriteLine("The answer is ");
    Console.WriteLine(42);
}

void run()
{
    double dailyRate = readDouble("Enter your daily rate: ");
    int noOfDays = readInt("Enter the number of days: ");
    writeFee(calculateFee(dailyRate, noOfDays));
}

private double readDouble(string v)
{
    throw new NotImplementedException();
}

private double readDouble(string v)
{
    Console.Write(v);
    string line = Console.ReadLine();
    return double.Parse(line);
}

private int readInt(string v)
{
    throw new NotImplementedException();
}

private int readInt(string v)
{
    Console.Write(v);
    string line = Console.ReadLine();
    return int.Parse(line);
}

private object calculateFee(double dailyRate, int noOfDays)
{
    throw new NotImplementedException();
}

private double calculateFee(double dailyRate, int noOfDays)
{
    throw new NotImplementedException();
}

private double calculateFee(double dailyRate, int noOfDays) => dailyRate * noOfDays;

private void writeFee(double v)
{
    ...
}

private void writeFee(double v) => Console.WriteLine($"The consultant's fee is: {v * 1.1}");

顾问费为：9817.5

double dailyRate = readDouble("Enter your daily rate: ");

int noOfDays = readInt("Enter the number of days: ");

writeFee(calculateFee(dailyRate, noOfDays));

public void DoWorkWithData(int intData, float floatData, int moreIntData)
{
    ...
}

public void DoWorkWithData(int intData, float floatData)
{
    ...
}

int arg1 = 99;
float arg2 = 100.0F;
int arg3 = 101;

DoWorkWithData(arg1, arg2, arg3); // 调用具有三个参数的重载
DoWorkWithData(arg1, arg2);      // 调用具有两个参数的重载

public void DoWorkWithData(int intData)
{
    ...
}

public void DoWorkWithData(int moreIntData)
{
    ...
}

void optMethod(int first, double second = 0.0, string third = "Hello")
{
    ...
}

optMethod(99, 123.45, "World"); // 为全部三个参数提供参数
optMethod(100, 54.321);          // 仅为前两个参数提供参数

optMethod(first : 99, second : 123.45, third : "World");
optMethod(first : 100, second : 54.321);

