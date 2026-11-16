

因此在 C++ 中，我们可以像使用预处理器值一样使用 const：

```
// const.cpp

#include <iostream>

using namespace std;

const int TOP = 100;
const int BOTTOM = 47;
const int SIZE = TOP - BOTTOM;

int main() {
    int a[SIZE * 2];
    for (int i = 0; i < SIZE; i++)
        a[i] = 0;
    cout << "SIZE * 2 = " << SIZE * 2 << endl;
}
```

上面的常量表达式：

```
const int SIZE = TOP - BOTTOM;
```

在编译时求值，因此可以用于数组定义。此处产生的输出是：

SIZE * 2 = 106

在 C++ 中，const 具有使用预处理器的所有优点。没有哪种情况更适合使用 #define 进行变量替换。使用 const 始终能获得更好的优势。

## const 变量

实际上，const 标识符是 C++ 的创新，并被 ANSI C 采用。将变量声明为 const 实际上使该变量成为只读。可以为其赋初始值，但其他语句无法更改它。

## 例如：

```
const int w = 10; // declares w as a read-only variable

int x = w; // legal - just accessing constant w

w = 25; // illegal - cannot change value to const w

const y = 5; // legal - can omit the int keyword

const int z; // illegal - const must be initialized when defined
```

将内置类型的对象声明为 `const` 的原因是让编译器确保它不会被更改。你也可以告诉编译器，用户定义类型的对象是 `const`，尽管它不存储在符号表中。实际上会为该对象分配存储空间！稍后详述。

## const 与指针（此部分只需大致了解）

某些 C++ 结构经常成为混淆的根源。其中之一是 `const` 与指针的共同使用。有时不清楚被引用的项目、指针还是两者都是常量。我们将查看：

- 指向常量的指针
- 常量指针
- 指向常量的常量指针

使用指针时，涉及两个事物：

- 指针本身
- 被指向的对象

两者都可以声明为 `const`，因此不能被赋值。在指针声明中，`const` 的位置指示是指针还是被指向的对象不可更改。

## 指向常量的指针

在指针声明前加上 `const` 会使被指向的对象（而非指针本身）成为常量。

```
syntax: const <type> *pc;
```

在此，pc 指向类型 <type> 的常量值。例如：

```
const char *pc = "Haley";
```

这定义了一个指向常量的指针，或者更具体地说，是一个指向字符常量的指针，即指向只读内存的指针。这类声明实际上最好从右向左读取以理解其含义：pc 是指向常量字符的指针。换句话说，pc 是指向类型 char 的常量对象的指针，因此通过 pc 无法修改 pc 所寻址对象的值：

```
pc[3] = 'x'; // error
*pc = 'x'; // error
```

上述每个示例均无效，因为 pc 所寻址的字符无法更改。但是，pc 本身不是常量，因此 pc 可以更改为寻址不同类型 char 的变量，如下所示：

```
pc = "Samantha"; // ok
```

在此，pc 被更改为寻址另一个字符。

将某物声明为指向常量的指针，是关于指针的声明，而不是关于被指向空间的声明。编译器不会确保被指向的数据不会更改。它只确保不会通过该指针更改。被指向的对象仍可通过其他方式更改。因此，声明指向常量的指针，即声明该指针不能用于更改被指向的对象。

## 常量指针

要声明指针本身为常量（而非被指向的事物），使用 *const：

```
syntax: <type> *const cp;
```

在此，cp 是指向类型 <type> 对象的常量指针。例如：

```
char *const cp = "Haley";
```

这定义了一个常量指针，或者更具体地说，是一个指向字符的常量指针，即指向内存的只读指针。我们说 cp 是指向字符的常量指针。常量指针 cp 始终指向同一块内存，因此必须在声明时初始化：

```
cp = "Haley" // error
```

虽然常量指针不能被修改，但它所指向的对象可以：

```
cp[3] = 'x'; // ok
*cp = 'x'; // ok
```

在此，我们只是修改 cp 所寻址的字符。

另一个示例：

```
int errNum; // possible error states of program
int *const curErr = &errNum; // constant pointer
```

在上述声明中，curErr 是指向 int 类型对象的常量指针。因此我们可以修改 curErr 所寻址对象的值：

```
if (*curErr) {
    errorHandler();
    *curErr = 0;
}
```

但不能修改 curErr 包含的地址：

```
curErr = &myError; // illegal
```

## 指向常量的常量指针

要使指针和被指向的对象都成为常量，两者都必须声明为 const。

```
syntax: const <type> *const cpc;
```

在此，cpc 是指向类型 <type> 常量值的常量指针。

例如：

```
const char *const cpc = "Haley";
```

这定义了一个指向常量的常量指针。cpc 是指向常量字符的常量指针。在这种情况下，cpc 所寻址对象的值和地址本身都不能更改，即 cpc 不能更改，它所指向的事物也不能更改：

```
cpc[3] = 'x'; // error
*cpc = 'x'; // error
cpc = "Samantha"; // error
```

## 向函数传递 const 参数

C++ 允许你将函数参数声明为 `const`：

```
void foo(const int num);
```

你为何要以这种方式声明函数？因为函数接收的是实际参数的副本，函数的调用者并不在意函数是否修改其副本。这称为按值传递。

但如果你仅出于效率目的传递指向某物的指针呢？你可能希望确保被调用的函数不使用指针来修改被引用的实体。通过将指针参数声明为 `const`，函数被禁止修改参数所指向的内容。

例如：

```
void foo(const int *num);
void foo(const char *buf);
void foo(const bigStruct *bs);
char *strcpy(char *p, const char *q);
void foo(const int & num);
```

声明返回 `const` 的函数也是合法的：

```
const int foo();
```

因此，返回的值只能像使用 `const int` 一样使用。例如：

```
// return.cpp

#include <iostream>

using namespace std;

int main() {
    const char *pc = getName();
    cout << pc << endl;
}

const char *getName() {
    return "Haley";
}
```

变量 pc 指向一个常量字符串。任何通过 pc 修改常量字符串的尝试都会导致编译时错误。

## 常量数组

为防止对数组元素进行更改，可以在数组声明前加上 const：

```
const int num[] = { 0, 1, 2, 3, 4 };
```

当程序由不同的人维护时，这尤其有用，他们可能会试图破坏模块的设计规则。请注意，由于 `const` 修饰符，任何试图更改数组值的语句都无法编译：

```
num[3]++;    // illegal
```

你可以按值传递数组，以确保数组成员不能被更改。使用定义了 `const` 关键字的指针参数传递数组：

```
int foo(const int *num) {
    num[i] = 25;    // illegal
    return num[i];  // ok
}
```

语句：

```
num[i] = 25;
```

是非法的，因为参数 num 被声明为指向常量整数数组的指针，不能被修改。

## 常量类成员和构造函数初始化列表

你可以将类的成员设为 const，但其含义恢复为 C 语言的含义。const 数据成员始终会分配存储空间，因此 const 在类内部占用空间。const 仍必须在定义时初始化。但是，对象的存储空间直到对象创建时才分配，而这正是 const 必须初始化的时点。因此，对于类成员而言，const 的含义是该对象在其生命周期内保持常量。

因此，const 的初始化必须在构造函数中进行。这是一个特殊操作，必须以特殊方式发生，以确保其值始终被设置。这在构造函数初始化列表中执行，该列表位于构造函数参数列表之后、函数体之前。这表明代码在进入构造函数体之前执行。例如：

