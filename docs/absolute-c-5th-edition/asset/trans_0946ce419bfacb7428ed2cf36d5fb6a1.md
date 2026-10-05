

# 第 15 章 多态与虚函数

销售额，直觉上，应该是所有单独销售账单的总和。你可能还想计算当天最大和最小的销售额或当天的平均销售额。这些都可以从单个账单计算出来，但许多计算账单的函数将等到你决定要处理什么种类型的销售时才会添加。为了适应这一点，我们将计算账单的函数设为虚函数（为了第一个示例的简单起见，我们假设每笔销售只有一个物品。尽管通过派生类和虚函数我们可以处理多个物品的销售，但此处不再这样做）。

显示 15.1 和 15.2 包含了 `Sale` 类的接口和实现。所有类型的销售都将是 `Sale` 类的派生类。`Sale` 类对应于没有折扣或费用的单品简单销售。注意成员函数 `bill` 声明中的 `virtual` 关键字（显示 15.1）。注意（显示 15.2），成员函数 `savings` 和重载运算符 `<` 均都使用了 `bill` 函数。由于 `bill` 被声明为虚函数，我们可以

显示 15.1 基类 Sale 的接口

```cpp
2 //这是头文件 sale.h。
3 //这是 Sale 类的接口。
4 //Sale 是一个用于简单销售的类。

5 #ifndef SALE_H
6 #define SALE_H

7 namespace SavitchSale
8 {
9 class Sale
10 {
11 public:
12 Sale();
13 Sale(double price);
14 double getPrice() const;
15 void setPrice(double price);
16 virtual double bill() const;
17 double savings(const Sale& other) const;
18 //如果你购买其他而不是调用对象，则返回节省金额。
19 private:
20 double price;
21 };

22 bool operator < (const Sale& first, const Sale& second);
23 //比较两个销售以查看哪个更大。
24 //SavitchSale

25 #endif // SALE_H
```

# 显示 15.2 基类的实现（部分 1/2）

```cpp
1 //这是文件 sale.cpp。
2 //这是 Sale 类的实现。
3 //Sale 类的接口在 sale.h 文件中。

5 #include <iostream>
6 #include "sale.h"
7 using std::cout;

8 namespace SavitchSale
9 {

10 Sale::Sale() : price(0)
11 {
12 // 意留为空
13 }

14 Sale::Sale(double thePrice)
15 {
16 if (thePrice >= 0)
17 price = thePrice;
18 else
19 {
20 cout << "Error: Cannot have a negative price!\n";
21 exit(1);
22 }
23 }

24 double Sale::bill() const
25 {
26 return price;
27 }

28 double Sale::getPrice() const
29 {
30 return price;
31 }

32 void Sale::setPrice(double newPrice)
33 {
34 if (newPrice >= 0)
35 price = newPrice;
36 else
37 {
38 cout << "Error: Cannot have a negative price!\n";
39 exit(1);
40 }

41 double Sale::savings(const Sale& other) const
42 {
43 return (bill() - other.bill());
44 }
```

（续）

# 显示 15.2 基类的实现（部分 2/2）

```cpp
47 bool operator < (const Sale& first, const Sale& second)
48 {
49 return (first.bill() < second.bill());
50 }
51 //SavitchSale
```

后定义的 `Sale` 类派生类会定义它们自己的 `bill` 成员函数；`Sale` 类提供的 `savings` 函数定义和重载运算符 `<` 在处理派生类对象时，将使用对应派生类的 `bill` 函数版本。例如，显示 15.3 和 15.4 展示了派生类 `DiscountSale`。注意 `DiscountSale` 类对其 `bill` 版本有不同的定义。然而，当 `savings` 函数和重载运算符 `<` 用于 `DiscountSale` 对象时，它们将使用为 `DiscountSale` 类提供的 `bill` 函数版本。这是 C++ 实现的一种非常巧妙的技巧。尽管，在函数 `d1.(d2)` 中，调用该函数的代码知道要使用为 `DiscountSale` 类提供的 `bill` 定义。

这是如何运作的？在 C++ 程序中，你可以认为这是通过魔法实现的，但真正的解释在本节的介绍中。当你将一个函数标记为 `virtual` 时，你是在告诉 C++ 环境：“等待在该中使用此函数，然后获取对应调用对象的实现。”显示 15.5 提供了一个示例程序，说明了虚函数 `bill` 和使用 `bill` 的函数在完整程序中的工作。

显示 15.3 派生类 DiscountSale 的接口（部分 1/2）

```cpp
2 //这是文件 discountsale.h。
3 //这是 DiscountSale 类的接口。

4 #ifndef DISCOUNTSALE_H
5 #define DISCOUNTSALE_H
6 #include "sale.h"
```

```cpp
7 namespace SavitchSale
```

# 显示 15.3 派生类 DiscountSale 的接口（部分 2/2）

```cpp
8 {
9   class DiscountSale : public Sale
10  {
11    public:
12      DiscountSale(double thePrice, double theDiscount);
13      //Discount 以价格的百分比表示。
14      //负的 discount 表示价格增加。
15      double getDiscount() const;
16      void setDiscount(double newDiscount);
17      double bill() const; // 由于 bill 在基类中被声明为虚函数，
18                             它在派生类 DiscountSale 中自动是虚的。
19                             可以在 bill 的声明中添加 virtual 饰符，也可以像这里这样省略；无论
20                             bill 在 DiscountSale 类中都是虚的。
21                             double discount;（我们倾向于在所有虚函数声明中包含 virtual 单词，
22                             即使不需要。我们在这里省略它是为了说明不需要。）
23 //
24 //SavitchSale
25 #endif //DISCOUNTSALE_H
```

# 显示 15.4 派生类 DiscountSale 的实现（部分 1/2）

```cpp
1
2   //这是 DiscountSale 类的实现。
3   //这是文件 discountsale.cpp。
4   //DiscountSale 类的接口在头文件
5   //discountsale.h 中。
6   #include "discountsale.h"
7
8   namespace SavitchSale
9   {
10    DiscountSale::DiscountSale() : Sale( ), discount(0)
11    {
12      // 意留为空
13    }
14
15    DiscountSale::DiscountSale(double thePrice, double theDiscount)
16    : Sale(thePrice), discount(theDiscount)
17    {
18      // 意留为空
19    }
20
21    double DiscountSale::getDiscount() const
22    {
23      return discount;
24    }
25
26    void DiscountSale::setDiscount(double newDiscount)
27    {
28      discount = newDiscount;
29    }
30
31    double DiscountSale::bill() const
32    {
33      double fraction = discount / 100;
34      return (1 - fraction) * getPrice();
35    }
```

（续）

# 显示 15.5 虚函数的使用

```cpp
//演示虚函数 bill 的性能。
#include <iostream>
#include "sale.h" // 不需要，由于 ifndef 是安全的
#include "discountsale.h"
using std::cout;
using std::endl;
using std::;
namespace SavitchSale
int main() {
    Sale sale(10.00);//一个价格 10.00 的物品；
    DiscountSale discount(11.00, 10); //一个价格 11.00 并有 10% 折扣的物品
    cout.set(ios::fixed);
    cout.set(ios::showpoint);
    cout.precision(2);
    if (discount < sale) {
        cout << "Discounted item is cheaper.\\n";
        cout << "Savings is $" << sale.savings(discount) << endl;
    } else {
        cout << "Discounted item is not cheaper.\\n";
    }
}
```

