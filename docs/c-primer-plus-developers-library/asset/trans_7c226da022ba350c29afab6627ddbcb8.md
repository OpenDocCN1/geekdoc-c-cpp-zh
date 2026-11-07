

- 2.

  ```cpp
  Gloam::Gloam(int g, const char * s) : glip(g), fb(s) { }
  Gloam::Gloam(int g, const Pabjous & fr) : glip(g), fb(fr) { }
  // note: the above uses the default Pabjous copy constructor
  void Gloam::tell()
  {
      fb.tell();
      cout << glip << endl;
  }
  ```

- 3.

  ```cpp
  Gloam::Gloam(int g, const char * s)
      : glip(g), Pabjous(s) { }
  Gloam::Gloam(int g, const Pabjous & fr)
      : glip(g), Pabjous(fr) { }
  // note: the above uses the default Pabjous copy constructor
  void Gloam::tell()
  {
      Pabjous::tell();
      cout << glip << endl;
  }
  ```

- 4.

  ```cpp
  class Stack<Worker *>
  {
  private:
      enum {MAX = 10};       // constant specific to class
      Worker * items[MAX];   // holds stack items
      int top;               // index for top stack item
  public:
      Stack();
      Boolean isempty();
      Boolean isfull();
      Boolean push(const Worker * & item); // add item to stack
      Boolean pop(Worker * & item);        // pop top into item
  };
  ```

- 5.

  ```cpp
  ArrayTP<string> sa;
  StackTP< ArrayTP<double> > stck_arr_db;
  ArrayTP< StackTP<Worker *> > arr_stk_wpr;
  ```

  清单 14.18 生成了四个模板：`ArrayTP<int, 10>`、`ArrayTP<double, 10>`、`ArrayTP<int, 5>` 和 `ArrayTP<ArrayTP<int, 5>, 10>`。

- 6. 如果一个类的两条继承线共享一个共同祖先，那么这个类最终会拥有该祖先成员的两份副本。将祖先类设为其直接后代的虚基类可以解决这个问题。

## 第15章复习题答案

- 1.
  - a. 友元声明应如下所示：

    ```cpp
    friend class clasp;
    ```

  - b. 这需要前向声明，以便编译器能够解释 `void snip(muff &)`：

    ```cpp
    class muff;    // forward declaration
    class cuff {
    public:
        void snip(muff &) { ... }
        ...
    };
    class muff {
        friend void cuff::snip(muff &);
        ...
    };
    ```

  - c. 首先，cuff 类的声明应位于 muff 类之前，以便编译器能够理解 `cuff::snip()` 这一项。其次，编译器需要 muff 的前向声明，以便它能够理解 `snip(muff &)`：

    ```cpp
    class muff;    // forward declaration
    class cuff {
    public:
        void snip(muff &) { ... }
        ...
    };
    class muff {
        friend void cuff::snip(muff &);
        ...
    };
    ```

- 2. 不行。要让类 A 拥有一个作为类 B 成员函数的友元，B 的声明必须位于 A 的声明之前。仅靠前向声明是不够的，因为它会告诉 A：B 是一个类，但不会揭示该类成员的名称。同样，如果 B 有一个作为 A 成员函数的友元，那么完整的 A 声明必须位于 B 的声明之前。这两个要求是互斥的。

- 3. 对类的唯一访问途径是通过其公共接口，这意味着对于 Sauce 对象，你唯一能做的事情就是调用构造函数来创建一个对象。其他成员（soy 和 sugar）默认是私有的。

- 4. 假设函数 `f1()` 调用函数 `f2()`。`f2()` 中的 return 语句会使程序执行恢复到函数 `f1()` 中 `f2()` 函数调用之后的下一条语句。throw 语句会使程序沿着当前函数调用序列回溯，直到找到一个直接或间接包含对 `f2()` 调用的 try 块。这个 try 块可能在 `f1()` 中，也可能在调用 `f1()` 的函数中，依此类推。一旦到达那里，执行会转到下一个匹配的 catch 块，而不是函数调用后的第一条语句。

- 5. 应按从最派生类到最不派生类的顺序排列 catch 块。

- 6. 对于示例 #1，如果 `pg` 指向一个 Superb 对象或任何派生自 Superb 的类的对象，则 if 条件为真。特别是，如果 `pg` 指向一个 Magnificent 对象，该条件也为真。在示例 #2 中，if 条件仅对 Superb 对象为真，对派生自 Superb 的对象不为真。

- 7. `dynamic_cast` 运算符只允许在类层次中进行向上转换，而 `static_cast` 运算符既允许向上转换，也允许向下转换。`static_cast` 运算符还允许从枚举类型转换为整数类型，以及反向转换，并允许在各种数值类型之间转换。

## 第16章复习题答案

- 1.

  ```cpp
  #include <string>
  using namespace std;
  class RQ1
  {
  private:
      string st;       // a string object
  public:
      RQ1() : st("") {}
      RQ1(const char * s) : st(s) {}
      ~RQ1() {};
  // more stuff
  };
  ```

  不再需要显式的复制构造函数、析构函数和赋值运算符，因为 string 对象提供了自己的内存管理。

- 2. 可以将一个 string 对象赋给另一个 string 对象。string 对象提供自己的内存管理，因此通常不必担心字符串超出其容纳对象的容量。

- 3.

  ```cpp
  #include <string>
  #include <cctype>
  using namespace std;
  void ToUpper(string & str)
  {
      for (int i = 0; i < str.size(); i++)
          str[i] = toupper(str[i]);
  }
  ```

- 4.

  ```cpp
  auto_ptr<int> pia = new int[20];   // wrong, use with new, not new[]
  auto_ptr<string>(new string);      // wrong, no name for pointer
  int rigue = 7;
  auto_ptr<int>(rigue);              // wrong, memory not allocated by new
  auto_ptr dbl (new double);         // wrong, omits <double>
  ```

- 5. 栈的后进先出（LIFO）特性意味着，在拿到所需的那根球杆之前，你可能得先取出许多球杆。

- 6. set 只会存储每个值的一份副本，因此，比方说，五个值为 5 的分数会被存储为单个 5。

- 7. 使用迭代器可以让你使用具有类似指针接口的对象，来遍历以数组以外某种方式组织的数据（例如，双向链表中的数据）。

- 8. STL 方法允许 STL 函数既可用于指向普通数组的普通指针，也可用于 STL 容器类的迭代器，从而提高了通用性。

- 9. 可以将一个 vector 对象赋给另一个 vector 对象。vector 管理自己的内存，因此可以向 vector 中插入项，并让它自动调整大小。通过使用 `at()` 方法，可以获得自动边界检查。

- 10. 两个 `sort()` 函数和 `random_shuffle()` 函数要求随机访问迭代器，而 list 对象只有双向迭代器。你可以使用 list 模板类的 `sort()` 成员函数（参见附录 G“STL 方法和函数”）代替通用函数来进行排序，但没有与 `random_shuffle()` 等价的成员函数。不过，你可以将 list 复制到 vector，打乱 vector，然后将结果复制回 list。

## 第17章复习题答案

- 1. iostream 文件定义了用于管理输入和输出的类、常量和操纵符。这些对象管理用于处理 I/O 的流和缓冲区。该文件还创建标准对象（`cin`、`cout`、`cerr` 和 `clog` 及其宽字符版本），用于处理连接到每个程序的标准输入和输出流。

- 2. 键盘输入会生成一系列字符。键入 **121** 会生成三个字符，每个字符由一个 1 字节的二进制代码表示。如果要将该值存储为 `int` 类型，则必须将这三个字符转换为值 121 的单个二进制表示。

- 3. 默认情况下，标准输出和标准错误都将输出发送到标准输出设备，通常是一台显示器。然而，如果让操作系统将输出重定向到文件，标准输出会连接到该文件而不是屏幕，但标准错误仍继续连接到屏幕。

- 4. `ostream` 类为每种基本 C++ 类型定义了 `operator<<()` 函数的一个版本。编译器会将类似

  ```cpp
  cout << spot
  ```

  的表达式解释为以下内容：

  ```cpp
  cout.operator<<(spot)
  ```

  然后，它可以将此方法调用与具有相同参数类型的函数原型匹配。

- 5. 可以串联返回类型为 `ostream &` 的输出方法。这会使以对象调用方法后返回该对象。然后，返回的对象可以调用序列中的下一个方法。

- 6.

  ```cpp
  //rq17-6.cpp
  #include <iostream>
  #include <iomanip>

  int main()
  {
      using namespace std;
      cout << "Enter an integer: ";
      int n;
      cin >> n;
      cout << setw(15) << "base ten" << setw(15)
           << "base sixteen" << setw(15) << "base eight" << "\n";
      cout.setf(ios::showbase);    // or cout << showbase;
      cout << setw(15) << n << hex << setw(15) << n
           << oct << setw(15) << n << "\n";

      return 0;
  }
  ```

