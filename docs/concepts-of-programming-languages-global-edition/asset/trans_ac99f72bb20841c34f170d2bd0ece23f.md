
```
```cpp
if (empty())
    cerr << "Error in top--stack is empty\n";
else
    return (stackPtr[topSub]);
}
int empty() { return (topSub == -1);}
```
```

我们仅讨论该类定义的几个方面，因为不必理解代码的所有细节。`Stack` 类的对象是栈动态的，但包含一个引用堆动态数据的指针。`Stack` 类有三个数据成员——`stackPtr`、`maxLen` 和 `topSub`——全部为私有。`stackPtr` 用于引用堆动态数据，即实现栈的数组。该类还具有四个公共成员函数——`push`、`pop`、`top` 和 `empty`——以及一个构造函数和一个析构函数。所有成员函数定义都包含在此类中，尽管它们也可以在外部定义。因为成员函数体包含在内，所以它们都隐式地内联。构造函数使用 `new` 操作符从堆上分配 100 个 int 元素的数组。它还初始化 `maxLen` 和 `topSub`。

下面是一个使用 `Stack` 抽象数据类型示例程序：

```
```cpp
void main() {
    int topOne;
    Stack stk;   /** Create an instance of the Stack class
    stk.push(42);
    stk.push(17);
    topOne = stk.top();
    stk.pop();
    . . .
}
```
```

以下是仅包含成员函数原型的 `Stack` 类定义。此代码存储在文件名为 `.h` 的头文件中。成员函数的定义在类定义之后。这些使用作用域解析运算符 `::` 来指示它们所属的类。这些定义存储在文件扩展名为 `.cpp` 的代码文件中。

```
```cpp
// Stack.h - the header file for the Stack class
#include <iostream.h>
class Stack {
private:   /** These members are visible only to other
            /** members and friends (see Section 11.6.3)
    int *stackPtr;
    int maxLen;
    int topSub;
public:    /** These members are visible to clients
    Stack();   /** A constructor
    ~Stack();   /** A destructor
    void push(int);
    void pop();
```
```
```
int top();
int empty();
}

// Stack.cpp - the implementation file for the Stack class
#include <iostream.h>
#include "Stack.h"
using std::cout;
Stack::Stack() { //** A constructor
  stackPtr = new int [100];
  maxLen = 99;
  topSub = -1;
}
Stack::~Stack() {delete [] stackPtr;};  //** A destructor
void Stack::push(int number) {
  if (topSub == maxLen)
    cerr << "Error in push--stack is full\n";
  else  stackPtr[++topSub] = number;
}
void Stack::pop() {
  if (topSub == -1)
    cerr << "Error in pop--stack is empty\n";
  else  topSub--;
}
int Stack::top() {
    if (topSub == -1)
      cerr << "Error in top--stack is empty\n";
    else
      return (stackPtr[topSub]);
}
int Stack::empty() {return (topSub == -1);}
```

## 11.4.2 Objective-C 中的抽象数据类型

如前所述，Objective-C 与 C++ 相似，其初始设计是 C 语言，并扩展以支持面向对象编程。两者之间的一个基本区别是，Objective-C 使用 Smalltalk 的语法进行其方法调用。

### 11.4.2.1 封装

Objective-C 类的接口部分定义在称为接口的容器中，其一般语法如下：

```
@interface class-name: parent-class {
  instance variable declarations
}
method prototypes
@end
```

第一行和最后一行以 at 符号 (@) 开头，是指令。
类的实现被打包在自然命名为 *implementation* 的容器中，其语法如下：

```
@implementation class-name
method definitions
@end
```

与 C++ 一样，在 Objective-C 中类是类型。
方法原型具有以下语法：

```
(+ | -) (return-type) method-name [ : (formal-parameters) ];
```

当存在时，加号表示该方法是类方法；减号表示实例方法。方括号中的形式参数表示它们是可选的。当没有参数时，括号和冒号均不存在。与大多数其他支持面向对象编程的语言一样，Objective-C 类的所有实例共享其实例方法的一个副本，但每个实例都有自己的一份实例数据。

形式参数列表的语法形式与更常见的语言 C、C++、Java 和 C# 不同。如果有一个参数，其类型在参数名称之前用括号指定，如以下方法原型所示：

```
-(void) meth1: (int) x;
```

此方法名为 meth1:（注意冒号）。具有两个参数的方法可如下所示：

```
-(int) meth2: (int) x second: (float) y;
```

在这种情况下，方法名为 meth2:second:，尽管这显然是一个 poorly chosen name。名称的最后一部分（second）可以省略，如下所示：

```
-(int) meth2: (int) x: (float) y;
```

由 myAdder 引用的对象调用一个参数的方法，在本例中为字面量 7，将如下所示：

```
[myAdder add1: 7];
```

如果一个方法接受两个参数并且其名称只有一部分，则在第一个参数后跟一个冒号，第二个参数跟在其后。两个参数之间不使用其他标点符号。如果有更多参数，则重复此模式。例如，如果 add1 接受三个参数并且没有名称的其他部分，则可以如下调用：

```
[myAdder add1: 7: 5: 3];
```

一个方法可以有多个参数和多个名称部分，如前例所示：

```
-(int) meth2: (int) x second: (float) y;
```

对该方法的示例调用如下：

```
[myObject meth2: 7 second: 3.2];
```

Objective-C 中的构造函数称为初始化器；它们只提供初始值。它们可以取任何名称，因此必须显式调用。构造函数返回对新对象的引用，因此其类型始终是指向类名的指针。它们使用返回语句返回 self，即对当前对象的引用。

在 Objective-C 中通过调用 alloc 创建对象。通常，在调用 alloc 之后显式调用类的构造函数。这两个调用可以并且通常是级联的，如以下语句所示，该语句使用 alloc 创建 Adder 类的对象，然后在其上调用其构造函数 init，并在 myAdder 中放置新对象的地址：

```
Adder *myAdder = [[Adder alloc] init];
```

所有类实例都是堆动态的，并通过引用变量引用。

C 程序几乎总是导入用于输入和输出函数的头文件 stdio.h。在 Objective-C 中，通常导入一个头文件，其中包含各种常用所需函数的原型，包括输入和输出，以及一些所需的数据。这是通过以下方式完成的：

```
#import <Foundation/Foundation.h>
```

程序 main 函数中的几乎所有代码通常都放在 @autoreleasepool 之后的复合语句中。在复合语句中创建的任何对象都会在复合语句结束时自动释放。

main 函数中的 @autoreleasepool 复合语句后面跟着 return 0 语句，表示执行成功到达 main 代码的末尾。

### 11.4.2.2 信息隐藏

Objective-C 使用指令 @private 和 @public 来指定类定义中实例变量的访问级别。这些用作 C++ 中使用的保留字 public 和 private。不同之处在于 Objective-C 中的默认值为 protected，而 C++ 中为 private。与大多数支持面向对象编程的编程语言不同，Objective-C 中没有限制对方法访问的方法。

在 Objective-C 中，实例变量的 getter 方法的命名约定是变量的名称。setter 方法的名称是单词 set 加上变量名称的大写形式。因此，对于名为 sum 的变量，getter 方法将命名为 sum，setter 方法将命名为 setSum。假设 sum 是一个 int 变量，这些方法可以定义如下：

```
// The getter for sum
-(int) sum {
    return sum;
}
```

```
// The setter for sum
-(void) setSum: (int) s {
    sum = s;
}
```

如果特定变量的 getter 和 setter 方法不对它们的操作施加任何约束，则它们可以由 Objective-C 编译器自动生成。这是通过在接口部分的属性指令中列出要为其生成 getter 和 setter 的实例变量来完成的，如下所示：

```
@property int sum;
```

在实现部分，变量在 synthesize 指令中列出，如下所示：

```
@synthesize sum;
```

由编译器生成的 getter 和 setter 的变量通常称为属性，并且访问方法被称为合成。

实例变量的 getter 和 setter 可以以两种方式使用，要么在方法调用中，要么在点表示法中，就像它们是公开可访问的一样。例如，如果我们为变量 sum 定义了 getter 和 setter，它们可以如下使用：

