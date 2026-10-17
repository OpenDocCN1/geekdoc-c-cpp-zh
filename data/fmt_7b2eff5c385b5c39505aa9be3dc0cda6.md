
派生类概念的一种流行且高效的实现方式是：将派生类的对象表示为基类的一个对象，并在末尾追加属于派生类的特定信息。例如：

Employee: Manager:

```
first_name first_name
family_name family_name
...
...
group
level ...
```

派生一个类并不隐含内存开销。所需空间仅仅是成员所需的空间。

以这种方式从 `Employee` 派生 `Manager`，使 `Manager` 成为 `Employee` 的一个子类型，因此任何可以接受 `Employee` 的地方都可以使用 `Manager`。例如，我们现在可以创建一个 `Employee` 列表，其中有些是 `Manager`：

```
void f(Manager m1, Employee e1)
{
list<Employee*> elist {&m1,&e1};
// ...
}
```

`Manager`（也）是一种 `Employee`，所以 `Manager*` 可以用作 `Employee*`。类似地，`Manager&` 可以用作 `Employee&`。然而，`Employee` 不一定是 `Manager`，所以 `Employee*` 不能用作 `Manager*`。一般来说，如果类 `Derived` 有一个公有基类 `Base`（§20.5），那么 `Derived*` 可以无需显式类型转换而赋给 `Base*` 类型的变量。相反的转换，从 `Base*` 到 `Derived*`，则必须显式进行。例如：

```
void g(Manager mm, Employee ee) {
Employee* pe = &mm; Manager* pm = &ee;
// OK: every Manager is an Employee // error : not every Employee is a Manager
pm->level = 2; // disaster : ee doesn’t have a level
pm = static_cast<Manager*>(pe); // bruteforce: works because pe points // to the Manager mm
pm->level = 2; // fine: pm points to the Manager mm that has a level }
```

换句话说，通过指针和引用操作时，派生类对象可以被当作其基类对象来对待。反之则不然。`static_cast` 和 `dynamic_cast` 的用法将在 §22.2 中讨论。

将一个类用作基类，相当于定义该类的一个（未命名的）对象。因此，一个类必须被定义后才能用作基类（§8.2.2）：

```
class Employee; // declaration only, no definition
class Manager : public Employee { // error : Employee not defined // ...
};
```

# 20.2.1 成员函数

诸如 `Employee` 和 `Manager` 这样的简单数据结构，其实并不那么有趣，也往往没什么用处。我们需要提供带有合适操作集合的恰当类型，而且不能受制于特定表示的细节。例如：

```
class Employee {
public:
void print() const;
string full_name() const { return first_name + ' ' + middle_initial + ' ' + family_name; }
// ...
private:
string first_name , family_name;
char middle_initial;
// ...
};
```

```
class Manager : public Employee {
public:
void print() const;
// ...
};
```

派生类的成员可以使用基类的公有——以及受保护（见 §20.5）——成员，就像它们在派生类自身中声明一样。例如：

```
void Manager::print() const
```

```
{
cout << "name is " << full_name() << '\n';
// ...
}
```

然而，派生类不能访问基类的私有成员：

```
void Manager::print() const
{
cout << " name is " << family_name << '\n'; // error!
// ...
}
```

第二个版本的 `Manager::print()` 将无法编译，因为 `family_name` 对 `Manager::print()` 不可访问。

这会让一些人感到惊讶，但请考虑另一种选择：如果派生类的成员函数可以访问基类的私有成员，那么私有成员的概念将变得毫无意义，因为程序员只需从类派生一个新类，就能访问类的私有部分。此外，人们再也无法通过查看声明为该类成员和友元的函数来找到私有名的所有用途。人们必须检查整个程序中所有源文件以寻找派生类，然后检查这些类的每个函数，再查找从这些类派生的每个类，等等。这充其量是乏味的，而且往往是不切实际的。在可接受的情况下，可以使用受保护成员而不是私有成员（§20.5）。

通常，最干净的解决方案是让派生类只使用其基类的公有成员。例如：

```
void Manager::print() const
{
Employee::print(); // print Employee information
cout << level; // print Manager-specific information
// ...
}
```

注意必须使用 `::`，因为 `print()` 在 `Manager` 中被重新定义了。这种名称重用很典型。粗心的人可能会这样写：

```
void Manager::print() const
{
print(); // oops!
// print Manager-specific information
}
```

结果是产生一系列递归调用，最终以某种形式的程序崩溃告终。

# 20.2.2 构造函数与析构函数

与通常一样，构造函数和析构函数是不可或缺的：

- 对象自底向上构造（先基类后成员，先成员后派生类），自顶向下析构（先派生类后成员，先成员后基类）；§17.2.3。

- 每个类都可以初始化自己的成员和基类（但不能直接初始化其基类的成员或基类）；§17.4.1。

- 通常，层次结构中的析构函数需要是虚函数；§17.2.5。

- 层次结构中类的拷贝构造函数应谨慎使用（如果确实要使用），以避免切片；§17.5.1.4。

- 构造函数或析构函数中虚函数调用、`dynamic_cast` 或 `typeid()` 的解析反映的是构造和析构的阶段（而不是尚未完成对象的类型）；§22.4。

在计算机科学中，“上”和“下”可能会让人非常困惑。在源代码中，基类的定义必须出现在其派生类定义之前。这意味着对于小例子，基类在屏幕上显示在派生类上方。此外，我们倾向于绘制根在顶部的树。然而，当我谈论自底向上构造对象时，我指的是从最基础的（例如基类）开始，然后再构建依赖于它的部分（例如派生类）。我们从根（基类）向叶子（派生类）构建。

# 20.3 类层次结构

派生类本身也可以是基类。例如：

```
class Employee { /* ... */ };
class Manager : public Employee { /* ... */ };
class Director : public Manager { /* ... */ };
```

这样一组相关的类传统上称为类层次结构。这种层次结构通常是一棵树，但也可以是更一般的图结构。例如：

```
class Temporary{/* ... */};
class Assistant : public Employee { /* ... */ };
class Temp : public Temporary, public Assistant { /* ... */ };
class Consultant : public Temporary, public Manager { /* ... */ };
```

或以图形表示：

Temporary        Employee

Assistant        Manager

Temp

Consultant       Director

因此，如 §21.3 中详细解释的那样，C++ 可以表达类的一个有向无环图。

## 20.3.1 类型字段

要把派生类用作不仅仅是声明中的便捷简写，我们必须解决以下问题：给定一个类型为 `Base*` 的指针，它指向哪个派生类型

object pointed to really belong? There are four fundamental solutions:

+ [1] 确保仅指向单一类型的对象（§3.4，第23章）。

+ [2] 在基类中放置类型字段供函数检查。

+ [3] 使用 `dynamic_cast`（§22.2，§22.6）。

+ [4] 使用虚函数（§3.2.3，§20.3.2）。

除非你使用了 `final`（§20.3.4.2），方案1依赖于比编译器所能获得的更多关于所涉及类型的知识。一般来说，试图比类型系统更聪明并不是一个好主意，但（尤其结合模板的使用）它可以用来实现同质容器（如标准库的 `vector` 和 `map`）并具有无与伦比的性能。方案[2]、[3]和[4]可用于构建异构列表，即（指向）多种不同类型对象的列表。方案[3]是方案[2]的语言支持变体。方案[4]是方案[2]的一种特殊类型安全变体。方案[1]和[4]的组合尤其有趣且强大；在几乎所有情况下，它们产生的代码比方案[2]和[3]更清晰。

让我们首先检查简单的类型字段方案，看看为什么通常最好避免它。manager/employee 示例可以这样重新定义：

```
struct Employee {
  enum Empl_type { man, empl };
  Empl_type type;

  Employee() : type(empl) { }
  string first_name, family_name; char middle_initial;

  Date hiring_date; short department; // …
};
struct Manager : public Employee { Manager() { type = man; }
  list<Employee **> group; // people managed
  short level;
  // …
};
```

在此基础上，我们现在可以编写一个打印每个 `Employee` 信息的函数：

```
void print_employee(const Employee * e)
{
  switch (e->type) {
  case Employee::empl:
    cout << e->family_name << '\t' << e->department << '\n'; // …
    break;
  case Employee::man:
    { cout << e->family_name << '\t' << e->department << '\n'; // …
      const Manager* p = static_cast<const Manager*>(e); cout << " level " << p->level
      << '\n';
```

```
// ...
break;
}
}
}
```

并用它来打印 `Employee` 列表，如下所示：

### Section 20.3.1 Type Fields 585

```
void print_list(const list<Employee*>& elist) {
for (auto x : elist)
print_employee(x);
}
```

这工作得很好，尤其是在由单个人维护的小程序中。然而，它有一个根本性的弱点，即它依赖于程序员以编译器无法检查的方式操作类型。这个问题通常会变得更糟，因为 `print_employee()` 等函数通常被组织成利用所涉及类的共同性：

```
void print_employee(const Employee * e)
{
cout << e->family_name << '\t' << e->department << '\n';
// ...
if (e->type == Employee::man) {
const Manager* p = static_cast<const Manager*>(e);
cout << " level " << p->level << '\n';
// ...
}
}
```

在处理许多派生类的庞大函数中，找到所有埋藏在其中的对类型字段的测试可能很困难。即使找到了，理解正在发生的事情也可能很困难。此外，任何新增 `Employee` 类型的添加都涉及对系统中所有关键函数的更改——那些包含对类型字段测试的函数。程序员必须考虑更改后可能需要对类型字段进行测试的每个函数。这意味着需要访问关键源代码以及由此产生的受影响代码测试的必要开销。使用显式类型转换是一个强有力的提示，表明改进是可能的。

换句话说，使用类型字段是一种容易出错的技术，会导致维护问题。随着程序规模的增大，问题会变得更严重，因为使用类型字段违反了模块化和数据隐藏的理想。每个使用类型字段的函数都必须知道包含类型字段的类的每个派生类的表示和其他实现细节。

似乎任何可从每个派生类访问的公共数据，例如类型字段，都会诱使人们添加更多此类数据。公共基类因此成为各种“有用信息”的存储库。这反过来又使基类和派生类的实现以最不希望的方式交织在一起。在一个大型类层次结构中，

公共基类中可访问（非私有）的数据成为层次结构的“全局变量”。为了实现干净的设计和更简单的维护，我们希望保持问题分离并避免相互依赖。

# 20.3.2 Virtual Functions

虚函数通过允许程序员在基类中声明函数，并在每个派生类中重新定义这些函数，从而克服了类型字段方案的问题。编译器和链接器将保证对象与其应用的函数之间的正确对应。例如：

```
class Employee {
public:
Employee(const string& name, int dept);
virtual void print() const;
// ...
private:
string first_name , family_name;
short department;
// ...
};
```

关键字 `virtual` 表示 `print()` 可以作为在此类中定义的 `print()` 函数以及从它派生的类中定义的 `print()` 函数的接口。在派生类中定义此类 `print()` 函数时，编译器确保在每种情况下为给定的 `Employee` 对象调用正确的 `print()`。

为了允许虚函数声明作为在派生类中定义的函数的接口，为派生类中的函数指定的参数类型不能与基类中声明的参数类型不同，并且仅允许返回类型有非常轻微的更改（§20.3.6）。虚成员函数有时称为方法。

虚函数必须为首次声明它的类定义（除非它被声明为纯虚函数；参见§20.4）。例如：

```
void Employee::print() const
{
cout << family_name << '\t' << department << '\n';
// ...
}
```

即使没有类从其类派生，也可以使用虚函数，并且不需要派生类提供自己的虚函数版本，除非需要。派生类时，如果需要，只需提供适当的函数即可。例如：

```
class Manager : public Employee {
public:
Manager(const string& name, int dept, int lvl);
void print() const;
// ...
```

```
private:
list<Employee*> group;
short level;
// ...
};
void Manager::print() const {
Employee::print();
cout << "\tlevel " << level << '\n'; // ...
```

### Section 20.3.2 Virtual Functions 587

派生类中具有与基类中虚函数相同名称和相同参数类型集的函数被称为覆盖基类版本的虚函数。此外，可以用更派生的返回类型覆盖来自基类的虚函数（§20.3.6）。

除非我们明确说明调用虚函数的哪个版本（如 `Employee::print()` 中的调用），否则覆盖函数会根据调用它的对象选择最合适的。无论使用哪个基类（接口）来访问对象，我们在使用虚函数调用机制时始终获得相同的函数。

全局函数 `print_employee()`（§20.3.1）现在变得不必要了，因为 `print()` 成员函数已取代了它的位置。`Employee` 列表可以这样打印：

```
void print_list(const list<Employee*>& s)
{
for (auto x : s)
x->print();
}
```

每个 `Employee` 将根据其类型写出。例如：

```
int main()
{
Employee e {"Brown",1234}; Manager m {"Smith",1234,2};
print_list({&e,&m});
}
```

生成：

```
Smith 1234
level 2
Brown 1234
```

请注意，即使 `print_list()` 在特定的派生类 `Manager` 甚至被构思之前就已编写并编译，这也有效！这是类的一个关键方面。当正确使用时，它成为面向对象设计的基石，并为不断发展的程序提供了一定的稳定性。

从 `Employee` 的函数中获得“正确”的行为，而与具体是什么

使用作用域解析运算符 `::` 调用函数，如 `Manager::print()` 所做，可以确保不使用虚机制：
