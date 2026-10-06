
`realCube` 未定义。C++ 要求每个函数、常量、变量或类在调用之前必须先定义。

在包含少量函数的简单程序中，很容易按照所需顺序的反序来定义函数，这样编译器在需要每个函数之前就能看到它的定义。在更复杂的程序中，这种方法更加困难，甚至无法实现。

编译器需要的函数定义部分是函数的头，而 C++ 了一种了一种机制，允许程序员向编译器提供函数头，将其与函数的实际定义分开。这种机制就是**原型**（prototype），它由函数头后跟一个分号组成。例如，函数 `realCube` 的原型是：

```
double realCube(double x);
```

为了消除在 C++ 文件中在函数定义之前就需要它的概率，常见的做法是在文件开头列出函数原型。在较大的程序中，函数原型被放置在头文件中，如 K.1 节所述。然后你可以在程序中包含（include）这些头文件。在创建类时，原型也同样重要，正如你将在下一节看到的那样。

请注意，你可以将函数作为参数传递给另一个函数或方法。这将在第 15 章的第 15.2.1 节中讨论。

## K.4 类

在 Java 类中实现的许多面向对象的概念也适用于 C++ 类。本附录仅涵盖你在单个类中可能遇到的语法差异。关于 C++ 类的更多信息请见附录 A 的 A.8 节以及 C++ 间插 1 和 2。

考虑以下 Java 类：

```
public class PlainBox {
    private String item;

    public PlainBox() {
    } // 默认构造函数结束

    public PlainBox(String theItem) {
        item = theItem;
    } // 构造函数结束

    public void setItem(String theItem) {
        item = theItem;
    } // setItem结束

    public String getItem() {
        return item;
    } // getItem 结束
} // PlainBox 类结束
```

虽然在 C++ 中可以在单个文件中定义类，但我们将使用两个文件，因为这是一种更常见且灵活的方法。第一个文件是类头文件；它包含了类的数据字段以及类中定义的所有方法的原型。它是类的描述，通常不包含可执行代码。例如，这里是 C++ 类 `PlainBox` 的头文件：

```
/** @file PlainBox.h */
#include <string> // 因为我们使用了 string 对象。
using namespace std; // 字符串是系统 std 库的一部分。
class PlainBox // 这是 PlainBox 的类声明。
  private:
    string item; // 定义在私有访问权限的项目。
  public: // 定义在公共访问权限的项目。
    PlainBox(); // 构造函数和方法的原型。
    PlainBox(string item);
    void setItem(string item);
    void getItem();
}; // 声明结束 PlainBox。
```

请注意，每个数据成员和方法并不需要有访问修饰符。私有数据成员分在一起，公共方法分在一起。每个访问修饰符后都跟一个冒号。可以有多个私有区域或受保护区域，但并不常见。类声明必须在右括号后以一个分号结束，如上所示。

类的实现文件（或源文件）名称通常与头文件相同，但以 `.cpp` 结尾以表示它是一个 C++ 文件。实现文件包含了随附头文件中声明的方法定义。这里是 C++ 类 `PlainBox` 的实现文件：

```
/** @file PlainBox.cpp */
#include "PlainBox.h" // 我们需要告诉编译器我们的数据字段和方法。
PlainBox::PlainBox()
{
} // 默认构造函数结束
PlainBox::PlainBox(string item)
{
  item = item;
} // 构造函数结束
void PlainBox::setItem(string item)
{
  item = item;
} // setItem 结束
string PlainBox::getItem()
{
  return item;
}
```

该实现文件首先包含头文件，头文件包含了类声明并知道该类的数据字段和方法。然后我们定义每个方法。在实现文件中没有封装所有方法的“主”大括号。每个方法都是单独定义的。为了让编译器知道某个方法属于 `PlainBox` 类，我们在方法名前添加了前缀 `PlainBox::`。注意前缀位于方法类型之前。前缀仅是方法名的扩展。

在 Java 中创建 `PlainBox` 对象，你可以可以使用以下语句：

```
PlainBox myBox = new PlainBox("Jewelry");
```

C++ 提供了几种创建对象的形式：

```
PlainBox myBox = PlainBox("Jewelry");
PlainBox myBox("Jewelry");
```

这些语句在 C++ 中是等价的，并且创建一个局部于创建它的函数或方法的 `PlainBox` 对象。在这些示例中，没有使用 C++ 关键字 `new`。

下面的示例使用 `new` 关键字创建一个 `PlainBox` 对象，该对象在程序特定删除它之前一直存在：

```
PlainBox* myBoxPtr = new PlainBox("Jewelry");
```

语法与 Java 类似，但 `PlainBox` 后面跟着 `*` 字符。`*` 表示 `myBoxPtr` 是一个指向 `PlainBox` 的指针，而不是对象本身。指针将在 C++ 2 中进行详细讨论。

如果在 C++ 中通过使用 `new` 运算符实例化对象（如上所示），则由程序员在不再需要时从内存中删除对象，因为 C++ 不提供垃圾回收。要通过 `someBoxPtr` 删除对象，可以使用以下语句：

```
delete someBoxPtr; // 释放对象使用的内存。
someBoxPtr = nullptr; // 安全预防措施。
```

每当你使用 `new` 运算符创建对象时，都必须编写相应的 `delete` 运算符来释放对象的内存。否则，你的应用程序将出现内存泄漏。

## K.5 基本输入与输出

尽管在系统层面，Java 和 C++ 处理键盘输入和控制台输出类似，但用于完成这些任务的高级结构差异很大。

为了让 Java 应用从键盘输入，你需要在 `System` 中创建一个 `Scanner` 对象，并使用它从用户获取输入。输出显示是通过调用 `System.out` 上的 `print` 或 `println` 方法实现的。以下代码创建一个 `Scanner` 对象，显示用户提示，接受响应并将响应回给用户：

```
Scanner scanner = new Scanner(System.in);
System.out.print("How many apples are in a box? ");
int applesPerBox = keyboard.nextInt();
System.out.print("You entered " + applesPerBox + " apples per box. ");
```

C++ 没有 `System` 或 `System.out`；相反分别使用 `cin` 和 `cout` 进行键盘输入和控制台输出。要使用 `cin` 和 `cout`，你需要在程序开头包含以下语句：

```
#include <iostream>
using namespace std;
```

以下 C++ 语句与之前的 Java 语句等效：

```
cout << "How many apples are in a box ? ";
int applesPerBox = 0;
cin >> applesPerBox;
cout << "You entered " << applesPerBox << " per box. " << endl;
```

注意使用输出流运算符 `<<` 将字符串字面量和变量发送到输出对象 `cout`。同样，输入流运算符 `>>` 将输入从输入对象 `cin` 发送到变量中。如果你将它们想象成指向数据流方向的箭头，就很容易记住使用哪种运算符。

常量 `endl` 定义在 `iostream` 中，代表换行符。关于 `iostream` 库的更多信息以及关于 C++ 基本输入和输出的信息，请见附录 A 的 A.2 节。

