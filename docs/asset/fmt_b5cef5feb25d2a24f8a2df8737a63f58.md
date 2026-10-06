
## 示例代码

```cpp
#include <iostream>
#include <Rectangle.h> // `Rectangle` 类需要
using namespace std;

int main() {
    Rectangle box; // 定义 `Rectangle` 类的实例

    // 显示矩形的数据。
    cout << "Here is the rectangle's data:\n";
    cout << "Width: " << box.getWidth() << endl;
    cout << "Length: " << box.getLength() << endl;
    cout << "Area: " << box.getArea() << endl;
    return 0;
}
```

## 程序输出

这是矩形的数据：
宽度: 0
长度: 0
面积: 0

## 使用成员初始化列表

之前显示的 `Rectangle` 类中的构造函数使用赋值语句将初始值存储在 `width` 和 `length` 成员变量中，如下：

```cpp
Rectangle() {
    width = 0.0;
    length = 0.0;
}
```

你可以使用称为成员初始化列表的替代技术来代替赋值语句进行初始化，如下：

```cpp
Rectangle() : width(0.0), length(0.0) {
}
```

## Rectangle 类定义

```cpp
{
  private:
    double width;
    double length;
  public:
    Rectangle(double, double); // 构造函数
    void setWidth(double);
    void setLength(double);
    double getWidth() const { return width; }
    double getLength() const { return length; }
    double getArea() const { return width * length; }
}
#endif
```

## Rectangle.cpp 的内容（版本 4）

```cpp
// Rectangle类的实现文件。
// 此版本包含一个接受参数的构造函数。
#include "Rectangle.h" // Rectangle类需要
#include <iostream> // cout需要
#include <cstdlib> // exit函数需要
using namespace std;

/***************************************************************************************************
// 构造函数接受用于宽度和长度的参数。 *
****************************************************************************************************

Rectangle::Rectangle(double w, double len) {
    width = w;
    length = len;
}

void Rectangle::setWidth(double w) {
    if (w >= 0)
        width = w;
    else {
        cout << "Invalid width\n";
        exit(EXIT_FAILURE);
    }
}
```

## 13.8 向构造函数传递参数

出现在 `Rectangle.cpp` 第12到16行的构造函数接受传递到 `w` 和 `len` 参数的参数。这些参数被赋值给 `width` 和 `length` 成员变量。由于构造函数在 `Rectangle` 对象创建时会被自动调用，因此参数作为对象定义的一部分传递给构造函数。这里有一个示例：

```cpp
Rectangle box(10.0, 12.0);
```

该语句演示了 `box` 作为 `Rectangle` 类的一个实例。构造函数被调用时，将值 `10.0` 传递给 `w` 参数，将 `12` 传递给 `len` 参数。结果是，对象的 `width` 成员变量将被赋值为 `10.0`，`length` 成员变量将被赋值为 `12.0`。这如图 13-16 所示。

### 图 13-16 传递给构造函数的参数

| width  | 10.0 |
| :----- | :--- |
| length | 12.0 |

`Rectangle box(10.0, 12.0);`

程序 13-8 演示了该类。（此文件可以在学生源代码文件夹 `13\Rectangle Version 4` 中找到。）

### 程序 13-8

```cpp
1 // 此程序调用 Rectangle 类的构造函数。
2 #include <iostream>
3 #include <iomanip>
4 #include "Rectangle.h"
5 using namespace std;
```

（程序继续）

### 程序 13-8（续）

```cpp
int main() {
    double houseWidth,  // 用于存储房间宽度
           houseLength; // 用于存储房间长度

    // 获取房子的宽度。
    cout << "In feet, how wide is your house ?";
    cin >> houseWidth;

    // 获取房子的长度。
    cout << "In feet, how long is your house ?";
    cin >> houseLength;

    // 创建一个 Rectangle 对象。
    Rectangle house(houseWidth, houseLength);

    // 显示房子的宽度、长度和面积。
    cout << precision(2) << fixed;
    cout << "The house is " << house.getWidth();
    cout << " feet wide.\n";
    cout << "The house is " << house.getLength();
    cout << " feet long.\n";
    cout << "The house is " << house.getArea();
    cout << " square feet in area.\n";
    return 0;
}
```

### 带有粗体显示的示例输入的程序输出

```text
In feet, how wide is your house? 30 Enter
feet, how long is your house? 60 Enter
The house is 30.00 feet wide.
The house is 60.00 feet long.
The house is 1800.00 square feet in area.
```

第21行的语句创建了一个 `Rectangle` 对象，将 `houseWidth` 和 `houseLength` 的值作为参数。

以下代码显示了另一个示例：`Sale` 类。该类可能用于发生销售交易的零售环境。`Sale` 类的对象代表一件商品的销售。（此文件可以在学生代码文件夹 `Chapter 13\Sale Version 1.0` 中找到。）

### Sale.h 的内容（版本 1）

```cpp
// Sale 类的规范文件。
#ifndef SALE_H
#define SALE_H

class Sale {
private:
    double itemCost; // 商品成本
    double taxRate;  // 销售税率
public:
    Sale(double cost, double rate) {
        itemCost = cost;
        taxRate = rate;
    }

    double getItemCost() const { return itemCost; }
    double getTaxRate() const { return taxRate; }
    double getTax() const { return (itemCost * taxRate); }
    double getTotal() const { return (itemCost + getTax()); }
};
#endif
```

第9行定义的 `itemCost` 成员变量持有销售税。第11和13行定义的 `taxRate` 变量。注意构造函数是内联的。它接受两个参数：`itemCost` 和 `taxRate`。这些参数用于初始化 `itemCost` 和 `taxRate` 成员变量。第15和16行的 `getItemCost` 函数返回 `itemCost` 的值。第18和19行的 `getTaxRate` 函数返回 `taxRate` 的值。第21和22行的 `getTax` 函数计算销售税金额。第24和25行的 `getTotal` 函数通过相加 `itemCost` 和 `tax` 返回总额。

### 程序示例

```cpp
1 // 此程序调用 Sale 类构造函数。
2 #include <iostream>
3 #include <iomanip>
4 #include "Sale.h"
5 using namespace std;

6 int main() {
7    double cost; // 用于存储商品成本
8    const double TAX_RATE = 0.06; // 税率

9    // 获取商品的成本。
10   cout << "Enter the cost of the item: ";
11   cin >> cost;

12   // 创建一个 Sale 对象。
13   Sale item(cost, TAX_RATE);

14   // 设置数值格式。
15   cout << fixed << precision(2);

16   // 显示销售税和总额。
17   cout << "The amount of sales tax is $" << item.getTax() << endl;
18   cout << "The total is $" << item.getTotal() << endl;

19   return 0;
20 }
```

### 带有粗体显示的示例输入的程序输出

```text
Enter the cost of the item: 10.00
The amount of sales tax is $0.60
The total is $10.60
```

第18行的语句创建一个 `Sale` 对象，将 `cost` 和 `TAX_RATE` 作为参数传递。

## 使用默认参数

与其他函数一样，构造函数可以有默认参数。回想第6章，如果在函数调用时没有提供参数，会自动传递默认参数。默认值列在函数的列表中。

以下代码显示了 `Sale` 类的修改版本。该版本的构造函数为税率使用了默认参数。（此文件可以在学生源代码文件夹 `13\Version 2` 中找到。）

### Sale.h 内容（版本 2）

```cpp
// 此版本的 Sale 类在构造函数未使用默认参数。
#ifndef SALE_H
#define SALE_H

class Sale {
private:
    double itemCost; // 商品成本
    double taxRate;  // 销售税率
public:
    Sale(double cost, double rate = 0.05) {
        itemCost = cost;
        taxRate = rate;
    }

    double getItemCost() const { return itemCost; }
    double getTaxRate() const { return taxRate; }
    double getTax() const { return (itemCost * taxRate); }
    double getTotal() const { return (itemCost + getTax()); }
};
#endif
```

如果定义 `Sale` 类对象时只向构造函数传递了一个参数（`cost` 参数），则 `rate` 参数将提供默认参数 `0.05`。这在程序 13-10 中演示。

```cpp
1 // 此程序使用构造函数的默认参数。
2 #include <iostream>
3 #include <iomanip>
4 #include "Sale.h"
5 using namespace std;

6 int main() {
7    double cost; // 用于存储商品成本
8    const double TAX_RATE = 0.06; // 税率

9    // 获取商品的成本。
10   cout << "Enter the cost of the item: ";
11   cin >> cost;

12   // 创建一个 Sale 对象。
13   Sale item(cost, TAX_RATE);

14   // 设置数值格式。
15   cout << fixed << precision(2);

16   // 显示销售税和总额。
17   cout << "The amount of sales tax is $" << item.getTax() << endl;
18   cout << "The total is $" << item.getTotal() << endl;

19   return 0;
20 }
```

### 带有粗体显示的示例输入的程序输出

```text
Enter the cost of the item: 10.00
The amount of sales tax is $0.60
The total is $10.60
```

### 程序 13-10 (继续)

```cpp
11 // 获取物品的成本。
12 cout << "Enter the cost of the item: ";
13 cin >> cost;

14 // 为此交易创建一个 Sale 对象。
15 // 指定物品成本，但使用默认的
16 // 5% 的税率。
17 Sale itemSale(cost);

18 // 设置数值输出格式。
19 cout << fixed << showpoint << setprecision(2);

20 // 显示销售税额和总额。
21 cout << "The amount of sales tax is $" << itemSale.getTax() << endl;
22 cout << "The total of the sale is $";
23 cout << itemSale.getTotal() << endl;
24 }
```

### 带有加粗示例输入的程序输出

```text
Enter the cost of the item: 10.00
The amount of sales tax is $0.50
The total of the sale is $10.50
```

## 关于默认构造函数的更多信息

前面提到过，当构造函数不接受参数时，它被称为默认构造函数。如果构造函数的所有参数都有默认参数，则可以在不传递任何参数的情况下调用，并成为默认构造函数。例如，假设 `Sale` 类的构造函数编写如下：

```cpp
Sale(double cost = 0.0, double rate = 0.05) {
    itemCost = cost;
    taxRate = rate;
}
```
