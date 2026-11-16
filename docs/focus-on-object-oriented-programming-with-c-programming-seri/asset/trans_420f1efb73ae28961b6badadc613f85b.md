

默认参数看起来很像函数重载，因为你可以使用相同的名称和不同的参数来调用函数。但是，使用默认参数时没有重载。编译器正在执行参数替换并调用同一个函数。

只要不会产生歧义，就可以将函数重载和默认参数一起使用：

```
void foo(); // ambiguous
void foo(int a = 10); // ambiguous
```

## 函数重载与默认参数作业

我们已经了解到 C++ 允许我们创建可以以不同方式调用的函数。我们可以为一个概念创建一个函数名称，并以多种便捷的方式实现该名称。这意味着我们需要教给最终用户的内容更少，代码也更易读。C++ 以两种方式支持这一特性：

函数重载允许我们创建多个同名函数，只要所有函数都有不同的参数列表即可。函数重载还可以在使用多个库时防止名称冲突。以下是一些重载函数的示例：

```
void foo(int);
void foo(int, char);
void foo(double);
```

当你希望某些参数由编译器自动插入，而不是每次调用函数时都自己全部写出时，默认参数用于单个函数。以下是一个带有默认参数的函数：

```
int foo(float f, float f2 = 1.1, char x = 'i');
```

你可以多次声明函数，但只能给默认参数一次。只有尾随参数可以赋予默认值，一旦开始赋予默认值，列表中其余所有参数都必须有默认值。

- 1. 名称编码方案因编译器而异，由编译器的实现者决定。此外，编码后的名称不打算由程序员直接使用（例如，编码方案可能会被编译器供应商合法更改，这将需要重新编译所有代码，但不需要其他更改。）看看你能否找出编译器为文件 array5.cpp 生成哪些编码后的名称。

```
// array5.cpp - friend function
// This program will compile, but it won't link without the set() definition
#include <iostream>
using namespace std;
#define SIZE 10
class intArray {
private:
    int a[SIZE];
public:
    void setVal(int index, int value);
    friend void print(intArray);
};
void print(intArray x) {
    int i;
    for(i = 0; i < SIZE; i++)
        cout << "a[" << i << "] = " << x.a[i] << endl;
}
int main() {
    intArray num;
    int i;
    for(i = 0; i < SIZE; i++)
        num.setVal(i,i);
    print(num);
    return 0;
}
```

汇编清单显示了 C++ 在被翻译成机器语言的 0 和 1 之前被翻译成的低级汇编语言。

有关为 Visual Studio 和 Xcode 生成汇编代码的说明，可以在此 Canvas 位置找到：

文件 | C++ 编译器

- 2. 创建一个具有整数 x、y、z 坐标的 Point 类。向类中添加一个 initialize() 成员函数，该函数包含三个坐标的默认参数。成员函数应在类外定义。

- 3. 向自己证明默认参数使用的是同一个函数。看看你能否为文件 send.cpp 生成汇编清单，并找到三个函数调用，以查看它们实际上是在调用同一个函数。

```
// send.cpp

void send(char * msg = "test", int times = 1);
void send(char *, int);

int main() {
  send();
  send("hello");
  send("hello", 3);
  return 0;
}
```

## 第 8 章。静态数据成员和静态成员函数

- 静态数据成员
- 静态成员函数
- 静态数据成员和静态成员函数作业

### 静态数据成员

有时，特定类的所有对象都需要访问同一个变量。这可能是与类相关的某个条件标志或计数器，在程序运行过程中会动态变化。

例如，可能需要统计在程序的某一时刻一个类有多少个对象存在。有时，为一个类的所有对象提供一个变量，比让每个对象维护自己的副本更高效。这个变量可能是指向该类错误处理例程的指针，或是指向该类堆的指针。

对于这些情况，静态数据成员可以提供解决方案。静态数据成员允许你在类的对象之间共享信息，而不向外部透露，例如全局类变量。

例如，假设我有一篮苹果，并且有一个定义成熟度的变量。现在当一个苹果达到某种状态时，我们说它已经坏了。一旦发生这种情况，所有其他苹果都应该知道，以便它们也能坏掉。在这种情况下，一个坏苹果确实会毁掉整篮苹果。

假设你想要一个存储单个单词的对象。然后你可以将文本文件转换为一组这样的对象。还假设你希望任何单词都能知道总共有多少个单词对象。例如：

```
// word1.h

#ifndef _WORD1_H
#define _WORD1_H

class Word {
private:
    char *buf;
public:
    Word(char *s);
};

#endif
```

```
// word1.cpp

#include <string.h>
#include "word1.h"

int wordCount = 0;              // global variable

Word::Word(char *s) {
    buf = strdup(s);
    wordCount++;                // increment global variable
}
```

现在，任何单词对象都可以访问 `wordCount` 来了解有多少个单词。但是这种方法有两个问题：

- 由于 `wordCount` 是全局的，任何人都可以修改它。没有安全性。
- `wordCount` 在全局命名空间中，这意味着如果你引入另一个使用相同名称的库，就会发生名称冲突。

你可能会想通过将 `wordCount` 放入类 Word 内部来解决这个问题，如下所示：

```
// word2.h

#ifndef WORD2_H
#define WORD2_H

class Word {
private:
    char *buf;
    int wordCount;
public:
    Word(char *s);
};

#endif
```

```
// word2.cpp

#include <string.h>
#include "word2.h"

Word::Word(char *s) {
    buf = strdup(s);
    wordCount++;
}
```

名称 wordCount 不再是全局的，数据受到保护，只有类 Word 的成员可以读取或修改它。但是，它没有产生预期的效果，因为 wordCount 的存储对于每个对象都不同。C++ 通过给关键字 static 添加另一个含义来解决这些问题。

在 C 语言中，static 有两种含义：

- 当用于定义所有函数外部的变量时，它意味着该变量具有内部链接，即该变量只能在声明它的文件中访问。如果同一个变量在另一个文件中定义为 static 或全局，则不会发生冲突，并且会为两个变量保留不同的存储。

- C 语言中 static 的第二种含义发生在它用于定义函数中的局部变量时。静态变量不是自动变量或局部变量。它不是在栈上创建，而是在特殊的静态数据区中创建。这意味着它的值在函数调用之间被保留，即保持静态。

在 C++ 中，类内部的静态数据成员类似于第二种定义。静态数据成员保存在静态数据区中，并且为类中的所有对象只分配一个变量。类中的每个对象共享同一个变量。这正是类 Word 所需要的：

```
// word3.h
#ifndef WORD3_H
#define WORD3_H
class Word {
private:
    char *buf;
    static int wordCount;
public:
    Word(char *s);
};
#endif

// word3.cpp
#include <string.h>
#include "word3.h"
Word::Word(char *s) {
    buf = strdup(s);
    wordCount++;
}
```

所以说每个对象包含其自身独立的数据并不完全正确。如果类中的数据项定义为 static，那么无论有多少个相同类的对象需要共享一个信息项，类中只会创建这样一个项。类的静态数据成员只有一个实例，并且只要类在作用域内，它就在作用域内，即只要类定义可访问。因此，静态数据成员是类的所有对象都可访问的单个共享变量。它充当其类的全局变量。

与使用全局变量相比，静态数据成员有两个优点：

- 可以强制执行信息隐藏。静态成员可以设为非公共；全局变量不能。
- 静态成员不会进入程序的全局命名空间，从而消除了意外名称冲突的可能性。

