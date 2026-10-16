

object pointed to really belong? There are four fundamental solutions:

+   [1] 确保仅指向单一类型的对象（§3.4，第23章）。  
+   [2] 在基类中放置类型字段供函数检查。  
+   [3] 使用 **dynamic_cast**（§22.2，§22.6）。  
+   [4] 使用虚函数（§3.2.3，§20.3.2）。

除非你使用了 **final**（§20.3.4.2），方案1依赖于比编译器所能获得的更多关于所涉及类型的知识。一般来说，试图比类型系统更聪明并不是一个好主意，但（尤其结合模板的使用）它可以用来实现同质容器（如标准库的 **vector** 和 **map**）并具有无与伦比的性能。方案[2]、[3]和[4]可用于构建异构列表，即（指向）多种不同类型对象的列表。方案[3]是方案[2]的语言支持变体。方案[4]是方案[2]的一种特殊类型安全变体。方案[1]和[4]的组合尤其有趣且强大；在几乎所有情况下，它们产生的代码比方案[2]和[3]更清晰。

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

在此基础上，我们现在可以编写一个打印每个 **Employee** 信息的函数：

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

并用它来打印 Employee 列表，如下所示：

## Section 20.3.1 Type Fields 585

```
void print_list(const list<Employee*>& elist) {
for (auto x : elist)
print_employee(x);
}
```

这工作得很好，尤其是在由单个人维护的小程序中。然而，它有一个根本性的弱点，即它依赖于程序员以编译器无法检查的方式操作类型。这个问题通常会变得更糟，因为 print_employee() 等函数通常被组织成利用所涉及类的共同性：

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

在处理许多派生类的庞大函数中，找到所有埋藏在其中的对类型字段的测试可能很困难。即使找到了，理解正在发生的事情也可能很困难。此外，任何新增 Employee 类型的添加都涉及对系统中所有关键函数的更改——那些包含对类型字段测试的函数。程序员必须考虑更改后可能需要对类型字段进行测试的每个函数。这意味着需要访问关键源代码以及由此产生的受影响代码测试的必要开销。使用显式类型转换是一个强有力的提示，表明改进是可能的。

换句话说，使用类型字段是一种容易出错的技术，会导致维护问题。随着程序规模的增大，问题会变得更严重，因为使用类型字段违反了模块化和数据隐藏的理想。每个使用类型字段的函数都必须知道包含类型字段的类的每个派生类的表示和其他实现细节。

似乎任何可从每个派生类访问的公共数据，例如类型字段，都会诱使人们添加更多此类数据。公共基类因此成为各种“有用信息”的存储库。这反过来又使基类和派生类的实现以最不希望的方式交织在一起。在一个大型类层次结构中，

公共基类中可访问（非私有）的数据成为层次结构的“全局变量”。为了实现干净的设计和更简单的维护，我们希望保持问题分离并避免相互依赖。

## 20.3.2 Virtual Functions

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

关键字 virtual 表示 print() 可以作为在此类中定义的 print() 函数以及从它派生的类中定义的 print() 函数的接口。在派生类中定义此类 print() 函数时，编译器确保在每种情况下为给定的 Employee 对象调用正确的 print()。

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

## Section 20.3.2 Virtual Functions 587

派生类中具有与基类中虚函数相同名称和相同参数类型集的函数被称为覆盖基类版本的虚函数。此外，可以用更派生的返回类型覆盖来自基类的虚函数（§20.3.6）。

除非我们明确说明调用虚函数的哪个版本（如 Employee::print() 中的调用），否则覆盖函数会根据调用它的对象选择最合适的。无论使用哪个基类（接口）来访问对象，我们在使用虚函数调用机制时始终获得相同的函数。

全局函数 print_employee()（§20.3.1）现在变得不必要了，因为 print() 成员函数已取代了它的位置。Employee 列表可以这样打印：

```
void print_list(const list<Employee*>& s)
{
for (auto x : s)
x->print();
}
```

每个 Employee 将根据其类型写出。例如：

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

请注意，即使 print_list() 在特定的派生类 Manager 甚至被构思之前就已编写并编译，这也有效！这是类的一个关键方面。当正确使用时，它成为面向对象设计的基石，并为不断发展的程序提供了一定的稳定性。

从 Employee 的函数中获得“正确”的行为，而与具体是什么

