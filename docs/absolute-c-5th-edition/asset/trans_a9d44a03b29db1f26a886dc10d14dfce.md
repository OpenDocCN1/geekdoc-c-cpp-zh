

## 函数重载与默认参数

## 示例：修改后的披萨购买程序

披萨消费者联盟在显示 4.5 中我们为他们编写的程序非常成功。事实上，每个人总是会购买最划算的披萨。曾有一家争议性的披萨店通过欺骗消费者购买更贵的披萨来盈利，但我们的程序已经终结了这种恶劣行为。然而，老板们将继续他们卑鄙的行为，并想出了欺骗消费者的新方法。他们现在同时提供圆形披萨和矩形披萨，希望这样可以迷惑消费者。显示 4.7 是程序的另一个版本，用于比较圆形披萨和矩形披萨。注意，函数名 `unitPrice` 已经被重载，使其同时适用于圆形和矩形披萨。

### 4.7 修改后的披萨程序（3 部分中的 1 部分）

```cpp
// // 确定圆形披萨或矩形披萨哪个划算。
#include <iostream>
using namespace std;
```

```cpp
double unitPrice(int diameter, double price);
// 返回圆形披萨每平方英寸的价格。
// 形形参数 diameter 是直径（英寸）。
// 形形参数 price 是披萨的价格。
```

```cpp
double unitPrice(int length, int width, double price);
// 返回长为 length、宽为 width 英寸的矩形披萨每平方英寸的价格。
// 形形参数 price 是披萨的价格。
int main()
{
    int diameter, length, width;
    double priceRound, unitPriceRound,
    priceRectangular, unitPriceRectangular;
    cout << "Welcome to the Pizza Consumers Union.\n";
    cout << "Enter the diameter in inches\n";
    cout << "of a round pizza: ";
    cin >> diameter;
    cout << "Enter the price of a round pizza: $";
    cin >> priceRound;
    cout << "Enter length and width in inches\n";
    cout << "of a rectangular pizza: ";
    cin >> length >> width;
    cout << "Enter the price of a rectangular pizza: $";
```

（继续）

### 4.7 修改后的披萨程序（3 部分中的 2 部分）

```cpp
    cin >> priceRectangular;
    unitPriceRectangular =
        unitPrice(length, width, priceRectangular);
    unitPriceRound = unitPrice(diameter, priceRound);
```

```cpp
    cout.set(ios::fixed);
    cout.set(ios::precision(2));
    cout << endl;
    cout << "Round pizza: Diameter = "
        << diameter << " inches\n";
    cout << "$" << priceRound;
```

```cpp
    cout << " Per square inch = $" << unitPriceRound;
    cout << endl;
    cout << "Rectangular pizza: Length = "
        << length << " inches\n";
    cout << "Rectangular pizza: Width = "
        << width << " inches\n";
    cout << "$" << priceRectangular;
    cout << " Per square inch = $" << unitPriceRectangular;
    cout << " The round one is the better buy.\n";
    cout << endl;
```

```cpp
    if (unitPriceRound < unitPriceRectangular)
        cout << "The round one is the better buy.\n";
    else
        cout << "The rectangular one is the better buy.\n";
    cout << "Buon Appetito!\n";

    return 0;
}

double unitPrice(int diameter, double price)
{
    const double PI = 3.14159;
    double radius, area;
    radius = diameter/double(2);
    area = PI * radius * radius;
    return (price/area);
}

double unitPrice(int length, int width, double price)
{
    double area = length * width;
    return (price/area);
}
```

### 4.7 修改后的披萨程序（3 部分中的 3 部分）

示例对话

```
Welcome to the Pizza Consumers Union.
Enter the diameter in inches of a round pizza: 10
Enter the price of a round pizza: $8.50
Enter length and width in inches
of a rectangular pizza: 6 4
Enter the price of a rectangular pizza: $7.55
```

```
Round pizza: Diameter = 10 inches
Price = $8.50 Per square inch = $0.11
Rectangular pizza: Length = 6 inches
Rectangular pizza: Width = 4 inches
Price = $7.55 Per square inch = $0.31
The round one is the better buy.
Buon Appetito!
```

## 默认参数

你可以为函数中的一个或多个按值传递参数指定默认参数。如果省略了相应的参数，它将被默认参数替换。例如，显示 4.8 中的函数 `volume` 根据长度、宽度和高度计算箱箱的体积。如果没有给出高度，则假设高度为 1。如果既没有给出宽度也没有高度，则它们都被假设为 1。

注意，在 4.8 中，默认参数是在函数声明中提供的，而不是在函数中。默认参数在函数第一次声明（或定义，如果发生的话）时给出。随后的声明或后续定义即使即使也不会导致此错误

