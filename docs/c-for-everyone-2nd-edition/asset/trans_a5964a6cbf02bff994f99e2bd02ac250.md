
**图 1** CashRegister 类的接口

![](img/23fb3582e93ebc95909e1de029c3d388_421_0.png)

修改器成员函数会改变它所操作的对象。

修改器成员函数会改变它所操作的对象。调用其中任一函数后，总金额和商品数量都会改变。

访问器成员函数不会改变它所操作的对象。对访问器使用 const。

访问器只查询对象的某些信息而不改变它。CashRegister 类有两个访问器：get_total 和 get_count。将这两个函数中的任何一个应用于 CashRegister 对象时，只是返回一个值，不会修改该对象。在 C++ 中，应使用保留字 const 来标记访问器函数（见第 402 页的编程提示 9.2），如下所示：

```cpp
double get_total() const;
```

成员函数使用你已经见过的 string 和流函数所用的点表示法来调用：

```cpp
CashRegister register1; // Defines a CashRegister object
register1.clear(); // Invokes a member function
```

现在我们知道 CashRegister 对象能做什么，但不知道它是如何做到的。当然，在程序中使用 CashRegister 对象时，我们不需要知道。我们只需使用公共接口。图 1 展示了 CashRegister 类的接口。修改器函数用指向私有数据内部的箭头表示，以表明它们会修改数据。访问器函数用指向另一方向的箭头表示，以表明它们只读取数据。

![](img/23fb3582e93ebc95909e1de029c3d388_421_1.png)

- 5. 下面的代码段会打印什么？

  ```cpp
  CashRegister reg;
  reg.clear();
  reg.add_item(0.95);
  reg.add_item(0.95);
  cout << reg.get_count() << " " << reg.get_total() << endl;
  ```

- 6. 下面的代码段有什么问题？

  ```cpp
  CashRegister reg;
  reg.clear();
  reg.add_item(0.95);
  cout << reg.get_amount_due() << endl;
  ```

- 7. 声明 CashRegister 类的一个成员函数 get_dollars，用于给出销售总额的美元值。

- 8. 说出 string 类的两个访问器成员函数。

- 9. ifstream 类的 get 成员函数是访问器还是修改器？

### 练习一下

现在你可以尝试本章末尾的这些练习：R9.3、R9.7。

add_item 函数接收一个价格作为参数，并且必须记录该价格。如果 CashRegister 对象存储已输入价格的数组，那么 add_item 函数会追加该价格。另一方面，如果我们决定只存储商品总额和数量，那么 add_item 函数会更新这两个变量。

最后，clear 函数必须为下一次销售准备好收银机，可以通过清空价格数组或将总额和数量设置为零来实现。

我们现在已经发现了表示对象所需数据的两种不同方式。两种方式都可以工作，我们必须做出选择。我们将选择更简单的一种：用变量表示总价格和商品数量。（其他选项在练习 P9.3 和 P9.4 中探讨。）

> 每个对象都有自己的一组数据成员。

数据成员定义在类定义的私有部分：

```cpp
class CashRegister
{
public:
   // See Section 9.2
private:
   int item_count;
   double total_price;
};
```

每个 CashRegister 对象都有这些数据成员的独立副本（见图 2）。

由于数据成员被定义为私有，只有类的成员函数才能访问它们。使用 CashRegister 类的程序员不能直接访问数据成员：

```cpp
int main()
{
   ...
   cout << register1.item_count; // Error—use get_count() instead
   ...
}
```

> 私有数据成员只能由同一类的成员函数访问。

所有数据访问都必须通过公共接口进行。因此，对象的数据成员对使用该类的程序员实际上是隐藏的。虽然在 C++ 中理论上可以通过将数据成员放入公共部分来不封装它们，但在实践中这非常少见。在本书中，我们将始终把所有数据成员设为私有。

![](img/23fb3582e93ebc95909e1de029c3d388_423_0.png)

**图 2** CashRegister 对象的数据成员

![](img/23fb3582e93ebc95909e1de029c3d388_424_0.png)

这些时钟有共同的行为，但每一个都有不同的状态。类似地，一个类的对象可以将其数据成员设置为不同的值。

![](img/23fb3582e93ebc95909e1de029c3d388_424_1.png)

- 10. 执行这些语句后，`register1.item_count`、`register1.total_price`、`register2.item_count` 和 `register2.total_price` 的值是什么？

  ```cpp
  CashRegister register1;
  register1.clear();
  register1.add_item(0.90);
  register1.add_item(0.95);
  CashRegister register2;
  register2.clear();
  register2.add_item(1.90);
  ```

- 11. 下面的代码段有什么问题？

  ```cpp
  CashRegister register2;
  register2.clear();
  register2.add_item(0.95);
  cout << register2.total_price << endl;
  ```

- 12. 考虑一个表示时间点的 Time 类，例如上午 9 点或下午 3:30。给出两组可用于实现 Time 类的不同数据成员。

- 13. 假设 Time 类的实现者从一种实现策略改为另一种实现策略，同时保持公共接口不变。使用 Time 类的程序员需要做什么？

- 14. 考虑一个表示字母等级（例如 A+ 或 B）的 Grade 类。给出两组可用于实现 Grade 类的不同数据成员。

**练习一下** 现在你可以尝试本章末尾的这些练习：R9.16、R9.17、R9.18。

## 9.4 成员函数

类的定义声明其成员函数。每个成员函数都在类定义之后单独定义。以下各节展示如何定义成员函数。

### 9.4.1 实现成员函数

下面是 CashRegister 类的 add_item 函数的实现。

```cpp
void CashRegister::add_item(double price)
{
    item_count++;
    total_price = total_price + price;
}
```

CashRegister:: 前缀清楚地表明我们正在定义 CashRegister 类的 add_item 函数。在 C++ 中，其他类中也可以有 add_item 函数，这完全合法，因此准确指明我们正在定义哪个 add_item 函数很重要。（见第 400 页的语法 9.2。）只在定义函数时使用 ClassName::add_item 语法，调用它时不要使用。调用 add_item 成员函数时，调用的形式为 object.add_item(...)。

定义成员函数时使用 ClassName:: 前缀。

定义访问器成员函数时，在参数列表的右括号后提供保留字 const。下面是 get_count 成员函数：

```cpp
int CashRegister::get_count() const
{
    return item_count;
}
```

你将在本节末尾的示例程序中找到其他成员函数。

### 9.4.2 隐式参数和显式参数

每当在成员函数中引用数据成员（例如 item_count 或 total_price）时，它表示调用该成员函数的对象的数据成员。例如，考虑以下调用：

```cpp
register1.add_item(1.95);
```

CashRegister::add_item 函数中的第一条语句是

```cpp
item_count++;
```

哪个 item_count 被递增？在这个调用中，是 register1 对象的 item_count。（见图 3。）

![](img/23fb3582e93ebc95909e1de029c3d388_425_0.png)

添加商品时，它会影响调用该函数的收银机对象的数据成员。

```cpp
for (int i = 1; i <= quantity; i++)
{
    add_item(price);
}
```

这里，`add_item` 成员函数是在隐式参数上被调用的。

```cpp
for (int i = 1; i <= quantity; i++)
{
    implicit_parameter.add_item(price);
}
```

也就是调用 `add_items` 函数的对象。例如，在调用 `register1.add_items(6, 0.95);` 时，`add_item` 函数会在 `register1` 上被调用六次。

### 语法 9.2 成员函数定义

![](img/23fb3582e93ebc95909e1de029c3d388_427_0.png)

**ch09/registertest1.cpp**

```cpp
1 #include <iostream>
2 #include <iomanip>
3
4 using namespace std;
5
6 /**
7    A simulated cash register that tracks the item count and
8    the total amount due.
9 */
10 class CashRegister
11 {
12 public:
13    /**
14       Clears the item count and the total.
15    */
16    void clear();
```

