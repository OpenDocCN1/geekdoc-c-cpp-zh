

// word10.cpp

#include <iostream>
#include <string.h>
#include "word10.h"

using namespace std;

int Word::wordCount = 0;

Word::Word(char *s) {
	buf = strdup(s);
	wordCount++;
}

int Word::getCount(Word *w) {
	cout << w->buf << endl;
	return wordCount;
}
}

// word10dr.cpp

#include <iostream>
#include "word10.h"

using namespace std;

int main() {
	Word w1("Red");
	Word w2("White");
	Word w3("Blue");

	cout << w1.getCount(&w1) << endl;
	cout << w2.getCount(&w2) << endl;
	cout << w3.getCount(&w3) << endl;
	return 0;
}
```

// word10 output:

Red
3
White
3
Blue
3

在这个示例中，我们在函数调用中传递了一个显式对象指针。下一个示例表明，使用引用来实现这一点也是合适的。

// word11.h

#ifndef WORD11_H
#define WORD11_H

class Word {
private:
    char *buf;
    static int wordCount;
public:
    Word(char *s);
    static int getCount(Word &w);
};

#endif

// word11.cpp

#include <iostream>
#include <string.h>
#include "word11.h"

using namespace std;

int Word::wordCount = 0;

Word::Word(char *s) {
    buf = strdup(s);
    wordCount++;
}

int Word::getCount(Word &w) {
    cout << w.buf << endl;
    return wordCount;
}
```

// word11dr.cpp
#include <iostream>
#include "word11.h"
using namespace std;
int main() {
    Word w1("Red");
    Word w2("White");
    Word w3("Blue");
    cout << w1.getCount(w1) << endl;
    cout << w2.getCount(w2) << endl;
    cout << w3.getCount(w3) << endl;
    return 0;
}
// word11 output
Red
3
White
3
Blue
3

请注意，不能将构造函数声明为 `static`。如果允许构造函数为 `static`，则可以在没有 `this` 指针的情况下调用它，因此将无法正确构建对象。

请记住，当你在类中看到一个 `static` 成员函数时，设计者的意图是该函数在概念上与整个类相关联。该函数将具有普通全局函数更快的调用时间，但其名称仅在类内可见，因此不会与全局函数名称冲突。

## 静态作业

- 1. 为下面的 Word5 类添加一个析构函数，使其递减 wordCount。为你的代码创建一个驱动程序，并展示你的析构函数有效。

// word5.h

#ifndef WORD5_H
#define WORD5_H

class Word {
private:
    char *buf;
    static int wordCount;
public:
    Word(char *s);
    int getCount();
};

#endif

// word5.cpp

#include <string.h>
#include "word5.h"

int Word::wordCount = 0;

Word::Word(char *s) {
    buf = strdup(s);
    wordCount++;
}

int Word::getCount() {
    return wordCount;
}

- 2. 编写一些代码，展示 this 指针成功传递到普通成员函数中，但无法在静态成员函数内访问。

- 3a. 创建一个包含普通成员函数和静态成员函数的类。

- 3b. 创建该类的一个对象，并在 for 循环内多次调用这两个函数。

- 3c. 编译程序，看看是否可以检查汇编列表以查看参数传递的位置，并验证 this 仅在一种情况下被传递。

## this 指针友元

## this 指针

到此你可能会好奇 C++ 中成员函数是如何实现的。考虑以下类：

class Alpha {
    private:
        int a, b, c;
    public:
        void foo(int x, int y, int z);
};

int main() {
    Alpha a1, a2;
    :
    :
}

普通成员函数的调用方式如下：

a1.foo(i, j, k);
a2.foo(i, j, k);

成员函数的代码保留在类 Alpha 中。当对象 a1 调用 foo() 时，成员函数 foo() 操作对象 a1 的私有数据。同样，当对象 a2 调用 foo() 时，成员函数 foo() 操作对象 a2 的私有数据。成员函数如何知道它正在处理哪个对象，以及操作哪些私有数据？

让我们探索成员函数 foo() 的调用：

a1.foo(i, j, k);

有多少个参数传递给了函数？答案可能会让你惊讶。是 7 个！

- 显式参数列表包含 3 个参数：i、j、k。

- 隐式参数列表包含 3 个参数，由对象的成员数据组成：a、b、c。

- 还有一个额外的隐式参数，称为 `this` 指针，它是指向调用成员函数的对象的指针。

C++ 自动在类的每个（非静态）成员函数中声明一个名为 `this` 的局部变量，并将其初始化为指向应用该成员函数的类的实例（或对象）。

因此，`this` 指针作为隐藏参数隐式传递给类中的每个非静态成员函数，并且具有与指向该类的声明指针相同的类型。实际上，我们将看到隐式参数可以被视为可通过 `this` 指针访问的参数列表。

因此，每个对象的成员函数都可以访问 `this` 指针，该指针指向（或包含）对象本身的地址。因此，任何成员函数都可以找出它所属对象的地址。

class Alpha {
    private:
        int a, b, c;
    public:
        void foo(int x, int y, int z);
        void display() { cout << this; }
};
int main() {
    Alpha a1, a2;
    a1.display();
    a2.display();
    :
}

所以，当你调用成员函数时，它进入作用域，`this` 的值设置为被调用对象的地址。`this` 指针可以像任何其他对象指针一样处理，因此可以用来访问它所指向对象中的数据。

class Alpha {
    private:
        int a, b, c;
    public:
        void foo(int x, int y, int z) {
            this->a = x;
            this->b = y;
            this->c = z;
            cout << this->a << this->b << this->c;
        }
        void display() {
            cout << this;
        }
};
int main() {
    Alpha a1, a2;
    a1.foo(2, 4, 6);
    a2.foo(1, 3, 5);
    :
    :
}

请注意，语法有效，但除了展示 `this` 确实指向对象之外，没有其他理由。`this` 指针实际上是我们可以在对象中将成员数据称为 `a`、`b`、`c` 而不是 `a1.a`、`a1.b`、`a1.c` 的原因。编译器会将 `this` 前缀添加到所有成员数据和函数中。

请注意以下区别：

- this 指向被指向对象的地址

- this->memberData 指向调用成员函数的对象的成员数据

- *this 指向实际对象，并且根据上下文，可以是左值或右值

## 另一个示例：

// this.cpp
#include <iostream>
#include <iomanip>
using namespace std;
class Alpha {
private:
   char ch;
public:
   void init(char c) {
       ch = c;
   }
   Alpha increment() {
       ch++;
       return *this;
   }
   Alpha* whereAmI() {
       return this;
   }
   void print() {
       cout << ch;
   }
};

int main() {
   Alpha a, b, c;

   a.init('a');
   b.init('b');
   c.init('c');
   a.print();
   cout << " is at " << a.whereAmI() << endl;
   b.print();
   cout << " is at " << b.whereAmI() << endl;
   c.print();
   cout << " is at " << c.whereAmI() << endl;
   c.increment().print();
   cout << " is at " << c.whereAmI() << endl;

   return 0;
}

程序输出如下：

a is at 0x0064FDF4
b is at 0x0064FDF0
c is at 0x0064FDEC
c is at 0x0064FDEC

成员函数 increment() 使用隐式提供的 this 指针来返回 ch 新增后的值。成员函数 whereAmI() 返回给定对象的地址。this 关键字提供了一个内置的自引用指针。就好像 Alpha 隐式声明了私有成员：

Alpha* const this

请注意，this 指针始终定义为不可修改的。

this 最常用于：

- 将对象（或其指针）传递给另一个函数

- 从成员函数返回对象（或其指针）。

例如：

#include <stdio.h>
#include <ctype.h>

class String {
private:
    char *buf;
public:
    :
    : String upperCase();
};

String String::upperCase() {
    for (char* cp = buf; *cp; ++cp)
        if (islower(*cp))
            *cp -= 32;
    return *this;
}

int main() {
    String s("hello");
    s.upperCase().print();
    return 0;
}

output:
HELLO

