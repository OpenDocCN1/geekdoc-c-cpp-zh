
```c
int re;
int im;
struct complex con(struct complex);
main()
{
    struct complex num={2,3};
    printf("After conjugation, the real and imaginary parts are %%%d and %%%d\n", con(num).re, con(num).im);
}
struct complex con(struct complex)
{
    num.im=-num.im;
    return num;
}
```

是的，这段代码在语法上是正确的，并在执行时输出为：

After conjugation, the real and imaginary parts are 2 and -3

如果 `f` 是一个返回结构或联合体的函数，且 `x` 是该结构或联合体的成员，那么 `f(x)` 是一个有效的表达式。因此，`con(num).re` 和 `con(num).im` 是有效的表达式，并分别求值为 2 和 -3。

### 15. 像数组名和函数名一样，结构名指向结构的基地址吗？

不，不像数组名和函数名（即函数描述符），结构名并不指向结构的基地址。结构名指的是整个结构。

### 16. 像数组一样，可以确定结构对象的成员是存储在连续的内存位置中吗？

不，同样不能确定结构对象的成员是存储在连续的内存位置中。结构对象的成员之间可能会有填充字节。

### 17. 假定以下类型定义和对象声明：

```c
struct { int i; int ci; };
struct t;
const t ct;
```

以下表达式的类型是什么？

1. `t.i`
2. `t.ci`
3. `ct.i`
4. `ct.ci`

给定的表达式属于以下类型：

1. `t.i` -> `int`
2. `t.ci` -> `const int`
3. `ct.i` -> `const int`
4. `ct.ci` -> `const int`

### 18. 为什么结构对象的相等运算符、不等于运算符和关系运算符无效？

因为结构对象没有自动以逐个成员的方式进行对齐并进行比较。

### 19. 如何找到结构中成员的偏移量？

结构中成员的偏移可以通过 `stddef.h` 头文件中的 `offsetof` 宏找到。`offsetof` 宏接受结构名称作为第一个参数，接受要找到的成员名称作为第二个参数。它返回字节数。

```c
#include <stddef.h>
struct type {
    char a;
    int b;
    char c;
    float d;
};
int main() {
    printf("Offset of a: %zu\n", offsetof(type, a));
    printf("Offset of b: %zu\n", offsetof(type, b));
    printf("Offset of c: %zu\n", offsetof(type, c));
    printf("Offset of d: %zu\n", offsetof(type, d));
    return 0;
}
```

上述代码的输出为：

Offset of a: 0

Offset of b: 4

Offset of c: 8

Offset of d: 12

（注意：实际值取决于编译器和对齐规则）。

### 20. `struct {...};` 与 `typedef struct {...} type;` 有什么区别？

这些语句之间的区别如下：

| `struct {...};` | `typedef struct {...} type;` |
|---|---|
| 1. 声明了一个结构标签（即 `type`） | 1. 声明了一个类型名（即别名）`type` |
| 2. 在声明该类型的对象时必须使用关键字 `struct` | 2. 可以仅使用类型名声明对象。不需要使用 `struct` 关键字 |
| 3. 使用 `struct` 关键字来声明定义结构的实例有点不方便 | 3. 这种声明形式稍微抽象。例如，从声明语句 `type objects` 来看，用户不知道 `type` 指的是结构，因为没有使用关键字 `struct` |

### 21. 我听说结构可以有一个指向自身的指针，但这段代码无法工作并给出了编译错误。为什么？

存储分类符 `typedef` 为类型创建了一个新名称（即别名）。我们可以同时定义一个新的结构类型并为其创建一个类型名（即别名）。然而，类型名在定义之前是无法使用的。在问题中，类型名 `NODE` 在定义之前就被使用了。这导致了编译错误。有两种方法解决这个问题：

1. 不要定义匿名类型，而是通过给结构一个标签名称来定义命名类型（例如 `struct node`）。然后将字段 `link` 声明为 `struct node* link`。纠正后的代码如下：

```c
typedef struct node {
    int data;
    struct node* link;
} NODE;
```

2. 将 `typedef` 定义与结构定义解离开，并将其放在结构定义之前，如下：

```c
typedef struct node {
    int data;
    NODE* link;
} NODE;
```

### 22. 下面联合类型的定义在语法上是正确的吗？如果是，该联合体类型对象的大小是多少？

```c
union numbers {
    struct {char a[10];} one;
    struct {int a[10];} two;
    struct {float a[10];} three;
};
```

## 9. 结构体与联合体

是的，联合体类型 `union numbers` 的定义在语法上是有效的。分配给联合体对象的内存量等于其最大成员的大小。在给定的联合体类型 `union numbers` 中，最大的成员是三个（即 4×10=40 字节），因此类型 `union numbers` 对象的大小为 40。

### 23. 下面这段代码在语法上是正确的吗？如果是，它的输出是什么？

```c
typedef struct error
{
  int warning, exception;
} error;

main()
{
  error err;
  err.exception = 2;
  switch(err.exception) {
    case 1: printf("Some warnings are there\n"); break;
    case 2: printf("Some error occurred\n"); break;
    case 3: printf("Some exception is there\n");
  }
}
```

是的，下面这段代码在语法上是正确的，并在执行时会输出 'Some error occurred'。根据上下文，编译器可以区分名称 `error` 的不同用法。例如，在语句 `error err;` 中，`error` 被视为类型定义别名。在语句 `err.error=2;` 中，`error` 被视为成员名。如果存在类似 `struct err;` 的语句，则 `error` 将被视为结构体标签名。

### 24. 我如何跟踪联合体中哪个字段正在被使用？

没有自动的方法来跟踪哪个联合体字段正在使用。但是，我们可以创建一个带有额外成员的类型，该成员用于记录当前正在使用的联合体字段。以下代码段演示了此类类型的定义：

```c
struct trackedunion
{
  enum {UNKNOWN, CHAR, INT, FLOAT, LONG, DOUBLE} code;
  union {
    char a;
    int b;
    float c;
    long d;
    double e;
  };
};
```

最初，`code` 的值被设置为 `UNKNOWN`，因为不知道哪个联合体字段正在使用。之后，每当给联合体字段赋值时，`code` 字段就会被相应设置。因此，`code` 字段可以记录正在写入的是哪个联合体字段。

### 25. 符号常量和枚举常量之间有什么区别？

符号常量和枚举常量之间的重要区别如下：

## 9.70 结构体与联合体

| 符号常量 | 枚举常量 |
| --- | --- |
| 1. 符号常量通过 `#define` 指令辅助创建 | 1. 枚举常量作为枚举类型定义的一部分创建 |
| 2. 符号常量具有全局作用域。定义后，它们可以在整个编译单元（即文件）中使用 | 2. 枚举常量具有局部作用域。它们只能在定义枚举类型的作用域内使用 |
| 3. 符号常量没有与之关联的类型 | 3. 枚举常量是整数类型 |
| 4. 符号常量的值需要显式列出 | 4. 枚举常量的值自动设置。默认情况下，第一个枚举常量的值为 0 |

### 26. 与其打印枚举常量的值，我想以符号的形式打印它们。我该怎么做？

枚举类型的唯一局限性是无法以符号形式打印枚举对象的值。默认情况下，枚举对象的值以整数形式打印。但是，你可以编写一个函数将枚举值映射为字符串。以下代码段演示了这样一个将枚举值映射为字符串的函数：

```c
#include<stdio.h>

enum BOOLEAN {FALSE, TRUE};

char* map(enum BOOLEAN a)
{
    switch(a)
    {
        case FALSE:
            return "FALSE";
        case TRUE:
            return "TRUE";
    }
}

int main() {
    enum BOOLEAN a, b;
    a=FALSE;
    b=TRUE;
    printf("The values of a and b in integer form are %d and %d\n", a, b);
    printf("The values of a and b in symbolic form are %s and %s\n", map(a), map(b));
    return 0;
}
```

上述代码的执行输出为：

The values of a and b in integer form are 0 and 1

The values of a and b in symbolic form are FALSE and TRUE

### 27. 下面这段代码在语法上是正确的吗？如果是，它的输出是什么？

```c
typedef enum {warning, exception} error;

main()
{
  error err;
  err=exception;
  switch(err) {
    case 1: printf("Some warnings are there\n"); break;
    case 2: printf("Some error occurred\n"); break;
    case 3: printf("Some exception is there\n");
  }
}
```

不是，上述代码在语法上是错误的，编译会导致 'Multiple declarations for 'error''（error 重复定义）。编译器根据上下文显示，无法区分 `err=exception` 语句中 `error` 作为别名和枚举常量的用法。

### 28. 存储值的有效方法是什么？

标志位（Flags）通常用于控制或指示不同的操作。例如，标志位通常用于控制或指示不同的操作。最重要的位被设置为 1。

### 29. 什么是位域（Bit-fields）？为什么要使用它们？

位域通常用于节省空间。位域在结构体中被使用。

### 30. '使用标准函数会增加文件的大小，但内联函数不会。' 这种说法正确吗？

不，这种陈述是错误的。内联函数可能会增加文件的大小，因为编译器会将函数体展开到每个调用处。

### 31. 确定以下代码的输出。假设由于头文件的包含会导致错误。

```c
struct book
{
  char title[20];
  char author[20];
  int pages;
  float price;
}

main()
{
  struct book book;
  printf("The size of object is %d bytes\n", sizeof(book));
}
```

### 32.

```c
struct book
{
  char title[20];
  char author[20];
  int pages;
  float price;
}

main()
{
  struct book book;
  printf("The size of type book is %d bytes\n",sizeof(struct book));
}
```

### 33.

```c
struct book
{
  char title[20];
  char author[20];
  int pages;
  float price;
}

main()
{
  struct book book;
  printf("%s by %s is %f rupees\n", book.title, book.author, book.price);
}
```

### 34.

```c
struct car
{
  struct engine e;
  struct chassis c;
}

struct engine
{
  int hp;
  int cc;
}

struct chassis
{
  int length;
  int width;
}

main()
{
  struct car yourcar={{68, 1400}, {3200, 2538}};
  if(yourcar.e.cc<1400)
    printf("It is a small car\n");
  else if(yourcar.e.cc==1400 || yourcar.e.cc<1600)
    printf("It is a middle segment car\n");
  else
    printf("It is a big car\n");
}
```

```c
struct car {
  struct engine {int hp; int cc;};
  struct chassis {int length; int width;};
}

main() {
  struct car yourcar={{68, 1400}, {3200, 2538}}; mycar={{52, 1000}, {3500, 2500}};
  if(yourcar.length>mycar.length)
    printf("Your car is longer than mine\n");
  else
    printf("My car is longer than yours\n");
}
```

//假设使用的编译器是 Borland Turbo C 4.5

```c
struct car {
  char *make;
  char *model;
  char *reg_no;
  struct {int hp; int cc;};
  struct {int length; int width; char* color;} c;
  float cost;
}

main() {
  struct car mycar;
  printf("The size of type car is %d\n",sizeof(struct car));
  printf("The objects of type car will take %d bytes of memory\n",sizeof(mycar));
}
```

```c
struct car {
  char *manufacturer="Maruti";
  char *make;
}
```

# 9.74 结构与联合体

```c
main()
{
    struct car mycar, yourcar;
    mycar.make = "Swift";
    yourcar.make = "Dzire";
    printf("We own %s and %s cars manufactured by %s", mycar.make, yourcar.make, mycar.manufacturer);
}
```

### 38.

```c
struct car
{
    char *make;
    char *model;
}
main()
{
    struct car mycar={"Maruti", "Dzire"};
    struct car yourcar=mycar;
    strupr(yourcar.make);
    strupr(yourcar.model);
    printf("My car is %s-%s\n",yourcar.make, yourcar.model);
}
```

### 39.

```c
struct car
{
    char *make;
    char *model;
}
main()
{
    struct car mycar={"Maruti", "Dzire"}, yourcar={"Maruti", "Dzire"};
    if(mycar==yourcar)
        printf("Both of us own car of same make and model");
    else
        printf("We own different types of cars");
}
```
