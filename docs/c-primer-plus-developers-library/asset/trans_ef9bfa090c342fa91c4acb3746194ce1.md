
- 6. 类构造函数何时被调用？类析构函数何时被调用？
- 7. 为本章复习题第5题中的银行账户类提供构造函数的代码。
- 8. 什么是默认构造函数？拥有默认构造函数有什么优点？
- 9. 修改 `Stock` 类定义（`stock20.h` 中的版本），使其具有返回各个数据成员值的成员函数。注意：返回公司名称的成员不应提供修改数组的方法。也就是说，它不能简单地返回字符串引用。它可以返回 `const` 引用。
- 10. `this` 和 *this* 是什么？

## 编程练习

- 1. 为本章复习题第5题中描述的类提供方法定义，并编写一个演示所有特性的简短程序。

- 2. 下面是一个相当简单的类定义：

  ```cpp
  class Person {
  private:
      static const LIMIT = 25;
      string lname;       // Person's last name
      char fname[LIMIT];  // Person's first name
  public:
      Person() {lname = ""; fname[0] = '\0'; }  // #1
      Person(const string & ln, const char * fn = "Heyyou");  // #2
      // the following methods display name and fname
      void Show() const;          // firstname lastname format
      void FormalShow() const;    // lastname, firstname format
  };
  ```

  （它同时使用 `string` 对象和字符数组，以便你比较这两种形式的用法。）编写一个程序，通过为未定义的方法提供代码来完成实现。使用该类的程序还应使用三种可能的构造函数调用（无参数、一个参数和两个参数）以及两个显示方法。下面是一个使用构造函数和方法的示例：

  ```cpp
  Person one;                       // use default constructor
  Person two("Smythecraft");       // use #2 with one default argument
  Person three("Dimwiddy", "Sam"); // use #2, no defaults
  one.Show();
  cout << endl;
  one.FormalShow();
  // etc. for two and three
  ```

- 3. 完成第9章编程练习1，但将那里显示的代码替换为合适的 `golf` 类声明。将 `setgolf(golf &, const char*, int)` 替换为带有用于提供初始值的合适参数的构造函数。保留 `setgolf()` 的交互版本，但通过使用构造函数来实现它。（例如，对于 `setgolf()` 的代码，获取数据，将数据传递给构造函数以创建临时对象，并将临时对象赋值给调用对象，即 `*this`。）

- 4. 完成第9章编程练习4，但将 `Sales` 结构及其关联函数转换为类及其方法。将 `setSales(Sales &, double [], int)` 函数替换为构造函数。通过使用构造函数来实现交互式 `setSales(Sales &)` 方法。将类保留在命名空间 `SALES` 中。

- 5. 考虑以下结构声明：

  ```cpp
  struct customer {
      char fullname[35];
      double payment;
  };
  ```

  编写一个程序，从由 `Stack` 类声明表示的栈中添加和移除 customer 结构。每次移除一个 customer 时，应将其付款加到累计总额中，并且应报告该累计总额。注意：你应该能够不加修改地使用 `Stack` 类；只需更改 `typedef` 声明，使 `Item` 为 `customer` 类型而不是 `unsigned long`。

- 6. 下面是一个类声明：

  ```cpp
  class Move
  {
  private:
      double x;
      double y;
  public:
      Move(double a = 0, double b = 0);  // sets x, y to a, b
      void showmove() const;             // shows current x, y values
      Move add(const Move & m) const;
      // this function adds x of m to x of invoking object to get new x,
      // adds y of m to y of invoking object to get new y, creates a new
      // Move object initialized to new x, y values and returns it
      void reset(double a = 0, double b = 0);  // resets x,y to a, b
  };
  ```

  创建成员函数定义和一个练习该类的程序。

- 7. 一个 Betelgeusean plorg 具有以下属性：

  ### 数据

  一个 plorg 的名字不超过 19 个字母。

  一个 plorg 有一个满意度指数（CI），它是一个整数。

  ### 操作

  一个新的 plorg 初始时具有一个名字和值为 50 的 CI。

  plorg 的 CI 可以改变。

  plorg 可以报告其名称和 CI。

  默认 plorg 的名字为“Plorga”。

  编写一个表示 `plorg` 的 `Plorg` 类声明（包括数据成员和成员函数原型）。编写成员函数的函数定义。编写一个演示 `Plorg` 类所有特性的简短程序。

- 8. 你可以这样描述一个简单列表：

  - 简单列表可以保存某种特定类型的零个或多个项。
  - 你可以创建一个空列表。
  - 你可以向列表添加项。
  - 你可以判断列表是否为空。
  - 你可以判断列表是否已满。
  - 你可以访问列表中的每一项并对其执行某种操作。

  如你所见，这个列表确实很简单；例如，它不允许插入或删除。

  设计一个 `List` 类来表示这种抽象类型。你应该提供一个包含类声明的 `list.h` 头文件，以及一个包含类方法实现的 `list.cpp` 文件。你还应创建一个利用你的设计的简短程序。

  保持列表规范简单的主要原因是简化这个编程练习。你可以将列表实现为数组，或者，如果你熟悉该数据类型，也可以实现为链表。但公共接口不应依赖于你的选择。也就是说，公共接口不应包含数组索引、指向节点的指针等。它应该用创建列表、向列表添加项等一般概念来表达。处理访问每一项并执行操作的常用方法是使用一个接受函数指针作为参数的函数：

  ```cpp
  void visit(void (*pf) (Item &));
  ```

  这里 `pf` 指向一个函数（不是成员函数），该函数接受一个 `Item` 引用参数，其中 `Item` 是列表中项的类型。`visit()` 函数将此函数应用于列表中的每一项。你可以将 `Stack` 类作为大致参考。

## 使用类

在本章中，你将学习以下内容：

- 运算符重载
- 友元函数
- 为输出重载 `<<` 运算符
- 状态成员
- 使用 `rand()` 生成随机值
- 类的自动转换和类型转换
- 类转换函数

C++ 类功能丰富、复杂且强大。在第10章“对象与类”中，你通过学习定义和使用一个简单的类，开始了面向对象编程之旅。你看到了类如何通过定义用于表示对象的数据类型，并通过成员函数定义可对这些数据执行的操作，从而定义一种数据类型。你还了解了两个特殊的成员函数——构造函数和析构函数，它们负责管理按类规范创建的对象的创建和销毁。本章将进一步探索类属性，重点放在类设计技术而不是一般原则上。你可能会发现这里涵盖的某些特性很直接，而有些则更微妙。要最好地理解这些新特性，你应该尝试这些示例并进行实验：如果对此函数使用普通参数而不是引用参数，会发生什么？如果从析构函数中遗漏某些内容，会发生什么？不要害怕犯错；通常，从解开错误中你能学到的东西比按部就班做对更多。（但是，不要以为一连串错误必然会带来惊人的洞见。）最终，你将获得回报：更全面地理解 C++ 如何工作以及 C++ 能为你做什么。

本章从运算符重载开始，它允许你对类对象使用标准 C++ 运算符，例如 = 和 +。然后它考察友元，这是 C++ 中允许非成员函数访问私有数据的机制。最后，它探讨如何指示
