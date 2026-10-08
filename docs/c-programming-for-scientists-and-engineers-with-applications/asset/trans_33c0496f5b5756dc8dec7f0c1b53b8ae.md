

## 6.2 单文件中的存储类

当数据文件打开且需要在调用之间保留该值时。
变量 `y` 和 `flag` 不需要静态的，因为它们在使用之前已经初始化了。

### 6.2.4 寄存器存储类 register

计算机中央处理器（CPU）内部有一组通用处理器寄存器。寄存器的访问速度远快于内存。为了计算效率，程序员可能会请求这些寄存器作为计数器和累加器等频繁使用变量的存储空间。但编译器有权决定接受或忽略该请求。如果在提出请求时所有寄存器都已分配，则编译器将不会为请求寄存器的变量分配寄存器，它将自动分配存储类 `auto`。如果无法为变量分配寄存器，寄存器存储类将默认为 `auto` 存储类。通常，寄存器类的声明如下。

```c
{ register int count; }
```

寄存器存储类变量局限于函数和局部块。它们的作用域遵循与 `auto` 变量相同的规则。只有在使用暴力破解算法且有许多情况需要检查时，才需要寄存器存储类。通常，最好避免此类算法。

下表显示了 `auto`、`extern`、`static` 和 `register` 存储类的作用域、初始化、保留状态、访问速度和声明。

| 作用域 | 初始化 | 函数调用间保留值 | 访问速度 | 声明 |
| --- | --- | --- | --- | --- |
| auto | 局部 | 显式 | 否 | 正常 | 块内的默认类 |
| extern | 全局 | 默认0 | 是 | 正常 | 所有块外的默认类 |
| static | 局部/全局 | 0 / 显式 | 是 | 正常 | 显式 |
| register | 局部/全局 | 显式 | 否 | 快 | 显式 |

- `extern` 类变量可以通过显式声明在定义之前进行引用，而 `static` 类变量不能在定义之前引用。`extern` 变量可以跨文件引用，而 `static` 变量不能跨文件引用。

### 6.2.5 复习题

- 1. 判断以下陈述的对错。
  a. `auto` 存储类是默认存储类。
  b. `auto` 变量在声明时会自动初始化为零。
  c. `extern` 存储类变量同时需要定义和声明。
  d. `extern` 存储类变量在声明时不进行初始化。
  e. 所有全局变量都是 `extern` 类变量。
  f. `static` 变量在声明时会自动定义。
  g. `static` 变量可以是多个函数的全局变量，也可以是特定函数的局部变量。
  h. 如果在请求时没有可用的寄存器，`register` 类变量默认为 `auto` 类。

- 2. 回答以下问题。
  a. 执行以下代码会打印什么？
```c
#include <stdio.h>

int x = 5;

float fun1(int, float);

int main()
{
   int a = 10;
   float b = 12.5, c;

   c = fun1(a, b);
   printf("a = %d b = %f c = %f\n", a, b, c);
   printf("x = %d\n", x);

   return 0;
}
```

```c
float func1(int a1, float b1)
{
    int x = 10;

    x = x + (int)(a1 * b1);
    printf("x = %d\n", x);

    return a1 * b1;
}
```

b. 执行以下代码会打印什么？

```c
#include <stdio.h>
int x = 5;

float func1(int, float);
float func2(int);

int main()
{
    int a = 10;
    float b = 12.5, c;

    c = func1(a, b);
    printf("a = %d b = %f\n", a, b, c);
    printf("x = %d\n", x);
    c = func2(a);
    printf(" c = %f\n", c);

    return 0;
}

float w;
float func1(int a1, float b1)
{
    x = x + a1 + (int)b1;
    printf("x = %d\n", x);
    w = w + 5.0;
    return(x + w);
}

float func2(int a2)
{
    float w = 6.5;
    x = x + a2+(int)w;
    printf("x = %d\n", x);
    w = w + 5.0;
    return(x + w);
}
```

c. 执行以下代码会打印什么：

```c
#include <stdio.h>

int func1( void);
int func2(void);

int main() {
    int a, b, i;

    for(i = 0; i < 4; i++) {
        a = func1();
        printf("a = %d\n", a);
        b = func2();
        printf("b = %d\n", b);
    }

    return 0;
}

int func1(void) {
    static int x;

    x = x + 2;
    return x;
}

int func2(void) {
    int x = 10;

    x = x + 5;
    return x;
}
```

## 6.3 多文件中的存储类

只有 `extern` 类变量可以跨文件可见。在一个文件中定义的变量可以通过在另一个文件中对其进行声明从而在另一个文件中可见。

### 6.3.1 外部存储类 Extern

`extern` 存储类具有多文件作用域。这意味着在一个文件中定义的 `extern` 类变量可以通过在另一个文件中声明该变量，使其在另一个文件中可见并被访问。例如，如果在程序 A 中定义了一个 `extern` 变量，则可以在文件 B 中显式声明它，使其在程序 B 中可见并可访问。`extern` 变量在声明时会自动初始化为零。以下代码展示了跨文件访问 `extern` 变量。

文件 A：
```c
#include <stdio.h>

void func1(void);
void func2(void);

int main()
{
    extern int a;      /* a 可见 */
    func1();
    a = a + 5;
    printf("In main a = %d\n", a);
    func2();
}

int a;
void func1(void)
{
    a = 15;
    printf("In func1 a = %d\n", a);
    return;
}
```

文件 B：
```c
int b = 10;
extern int a;
void func2(void)
{
    a = a + 10;
    b = b + 5;
    printf("In func2 a = %d\n", a);
    printf("In func2 b = %d\n", b);
    return;
}
```

输出结果如下：

In func1 a = 15
In main a = 20
In func2 a = 30
In main a = 55

