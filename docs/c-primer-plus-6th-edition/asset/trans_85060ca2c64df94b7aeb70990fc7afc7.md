
# 第14 章 在 C++ 中重用代码

```cpp
cin.getline(lab, 50);
cout << "Enter number of years: ";
int yrs;
cin >> yrs;
```

```cpp
Wine holding(lab, yrs); // 存储标签，赋予数组 yrs 个元素
holding.GetBottles(); // 请求年份、瓶数量的输入
holding.Show(); // 显示对象内容
```

```cpp
const int YRS = 3;
y[YRS] = {1993, 1995, 1998};
int b[YRS] = {48, 60, 72};
// 创建新对象，使用数组 y 和 b 初始化数据
Wine more("Gushing Grape", yrs, y, b);
more.Show();
```

```cpp
cout << "Total bottles for " << more.Label() // 使用 Label() 方法
cout << ": " << more.sum() << endl; // 使用 sum() 方法
cout << "Bye\n";
return 0;
```

以下是一些示例输出：

Enter name of wine: Gully Wash
Enter number of years: 4
Enter Gully Wash data for 4 year(s):
Enter year: 1988
Enter bottles for that year: 42
Enter year: 1994
Enter bottles for that year: 58
Enter year: 1998
Enter bottles for that year: 122
Enter year: 2001
Enter bottles for that year: 144
Wine: Gully Wash

| Year | Bottles |
||||
| 1988 | 42 |
| 1994 | 58 |
| 1998 | 122 |
| 2001 | 144 |

Wine: Gushing Grape Red
Year Bottles
1993 48
1995 60
1998 72

Total bottles for Gushing Grape Red: 180
Bye

# 编程练习

2. 此练习与编程练习 1 相同，不同之处你应该使用包含的私有继承（private inheritance of containment）。同样，几个类型定义（typedefs）可能会证明很有用。此外，你可能需要思考如下语句的含义：
`PairArray::operator((PairArray(ArrayInt),ArrayInt()));`
`cout << (const string&)*this);`

该类应该能够与练习 1 所示的测试程序配合。

3. 定义一个 QueueTp 模板。通过创建一个指向 Worker 指针的队列（如列表 14.10 中定义）来对其进行测试，并在一个类似于列表 14.12 的程序中使用该队列。

4. Person 类持有一个人的名和姓。除了构造函数外，它还有一个 `Show()` 方法来显示这两个名字。Gunslinger 类虚析继承自 Person 类。它有一个 `Draw()` 成员，返回一个 `double` 类型的值，代表快枪手手的拔枪速度。该类还有一个 `int`，表示快枪手手枪上缺口的数量。最后，它有一个 `Show()` 函数来显示所有这些信息。

PokerPlayer 类虚析继承自 Person 类。它有一个 `Draw()` 成员，返回一个 1 到 52 之间的随机数，代表牌牌值。（可选地，你可以定义一个带有花色和点值成员的 Card 类，并使用牌的返回值用于 Draw()。）PokerPlayer 使用 Person 的 `show()`。BadDude 类公有析自 Gunslinger 和 PokerPlayer 类。它有一个 `GDraw()` 成员返回坏蛋的拔枪时间，以及一个 `GDraw()` 成员返回下一张抽牌。它有一个相应的 `Show()` 函数。定义所有这些类和方法，以及任何其他必要的方法（作为设置对象值的方法），并在类似于列表 14.12 的简单程序中对它们进行测试。

5. 这里是一些类声明：
`// emp.h -- abstr_emp 类及其子类的头文件`

```cpp
#include <iostream>
#include <string>

class abstr_emp {
private:
    std::string fname; // abstr_emp 的名
    std::string lname; // abstr_emp 的姓
    std::string job;
```

# 第14 章 在 C++ 中重用代码

public:

```cpp
abstr_emp();
abstr_emp(const std::string & fn, const std::string & ln,
    const std::string & j);
virtual void ShowAll() const; // 并显示所有数据
virtual void SetAll(); // 提示用户输入值
friend std::ostream &n
    operator<<=(std::ostream& os, const abstr_emp & e);
    // 只显示名和姓
virtual ~abstr_emp() = 0; // 虚基类
};

class employee : public abstr_emp {

public:

```cpp
employee();
employee(const std::string & fn, const std::string & ln,
    const std::string & j);
virtual void ShowAll() const;
virtual void SetAll();
};

class manager : virtual public abstr_emp {

private:

```cpp
int inchargeof; // 管理的 abstr_emps 数量
```

protected:

```cpp
int InchargeOf() const { return inchargeof; } // 输出
int& InchargeOf() { return inchargeof; } // 输入
```

public:

```cpp
manager();
manager(const std::string & fn, const std::string & ln,
    const std::string & j, int ico = 0);
manager(const abstr_emp & e, int ico);
manager(const manager & m);
virtual void ShowAll() const;
virtual void SetAll();
};

class fink : virtual public abstr_emp {

private:

```cpp
std::string reportsto; // fink 向谁汇报
```

protected:

```cpp
const std::string reportToSto() const { return reportsto; }
std::string & reportToSto() { return reportsto; }
```

```cpp
public:

fink();
fink(const std::string & fn, const std::string & ln,
const std::string & j, const std::string & rpo);
fink(const abstr_emp & e, const std::string & rpo);
fink(const fink & e);
virtual void ShowAll() const;
virtual void SetAll();
};
```

```cpp
class highf: public manager, public fink // 管理 mink
public:
highink();
highink(const std::string & fn, const std::string & ln,
const std::string & j, const std::string & rpo,
ico);
highink(const abstr_emp & e, const std::string & rpo,
ico);
highink(const manager & m, ico);
highink(const fink & f, ico);
virtual void ShowAll() const;
virtual void SetAll();
};
```

注意：由于虚基类，highf::ShowAll() 会调用 fink::ShowAll() 和 manager::ShowAll()，以及 abstr_emp::ShowAll()。这简化了代码。请注意某些保护访问方法。这里有一个最小的测试程序：

```cpp
// pele4-5.cpp
// emp.h -- 使用 abstr_emp 类的头文件

```cpp
#include <iostream>
using namespace std;
#include "emp.h"

int main(void)
{
  employee em("Trip", "Thumper", "Sales");
  em.ShowAll();

  manager ma("Amorphia", "Nuancer", "Management", 5);
  ma.ShowAll();

  fink fi("Matt", "Oggs", "Oiler");
  fi.ShowAll();

  highf h("Curly", "Kew", "Executive", 2);
  h.ShowAll();

  abstr_emp *tri[4] = {&em, &ma, &fi, &h};
  for (int i = 0; i < 4; i++)
    tri[i]->ShowAll();

  return 0;
}
```

为什么没有定义赋值运算符？
为什么 ShowAll() 和 SetAll() 是虚函数？
为什么 abstr_emp 是虚基类？
为什么 highf 类没有数据部分？
为什么只需要一个版本的 <<？

如果将程序的结尾替换为以下代码会发生什么？
```cpp
abstr_emp tri[4] = {em, hf, hf2};
for (int i = 0; i < 4; i++)
  tri[i].ShowAll();
```

# 朋友、异常以及更多

在本章中，你将学习：

- 朋友类
- 朋友方法类
- 嵌套类
- 抛出异常、try 块和 catch 块
- 异常类
- 运行时类型识别 (RTTI)
- dynamic_cast 和 typeid
- static_cast、const_cast 和 reinterpret_cast

本章结束了一些遗留问题，并探索了 C++ 语言的一些后续功能。嵌套类是定义在其他类内部。这里讨论的后续功能是异常、运行时类型识别以及改进类型控制。C++ 异常处理为处理否则会导致程序停止的异常情况提供了机制。RTTI 是识别对象类型的机制。新的类型转换提高了类型转换的安全性。最后这三个功能对于 C++ 来说相当新，旧的编译器不支持它们。
