

# 370 存储类

在 main 中 a = 55
在 main 中 b = 52

注意 a 定义在 File A 中，而 b 定义在 File B 中。通过将 a 声明为 extern 变量，在 File A 中定义的 extern 变量 a 在 File B 中变得可见。通过在 File A 中将 b 声明为 extern 变量，在 File B 中定义的变量 b 在 File A 中可见（在 main 和 func1 内部）。以下代码显示了 File B 中定义的变量可以在 File A 中声明为全局 extern 变量。

File A:
```c
#include <stdio.h>
void func1(void);
void func2(void);
```

```c
extern int b;
int main ()
{
    extern int a;
    func1();
    a = a + 5;
    b = b + 12;
    printf("In main a = %d\n", a);
    printf("In main b = %d\n", b);
    func2();
    a = a + 25;
    b = b + 15;
    printf("In main a = %d\n", a);
    printf("In main b = %d\n", b);

    return 0;
}
```

```c
void func1(void)
{
    a = 15;
    b = b + 10;
    printf("In func a = %d\n", a);
    printf("In func b = %d\n", b);

    return;
}
```

File B:
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

输出如下：

In func1 a = 15
In func1 b = 20
In main a = 20
In main b = 32
In func2 a = 30
In func2 b = 37
In main a = 55
In main b = 52

# 6.3.2 复习题

- 1. 判断下列陈述的对错。
   a. auto 变量是跨文件可见的。
   b. static 变量是跨文件不可可见的。
   c. static 变量具有文件作用域。
   d. extern 变量不是跨文件可见的。
   e. 在一个文件中定义的 extern 变量可以在另一个文件中访问。
   f. 在一个文件中定义的 static 变量不能在另一个文件中声明。
- 2. 执行以下代码会打印什么？

```c
FILE A:
#include <stdio.h>
void func1(void);
```

# 372 存储类

```c
int main() 
{
    extern int x;

    x = x + 10;
    printf("In main x = %d\n", x);

    func1();
    x = x + 5;
    printf("In main x = %d\n", x);
    return 0;
}
```

FILE B:
```c
int x;
void func1(void)
{
    x = x + 5;
    printf("In func x = %d\n", x);
}
```

- 3. 执行以下代码会打印什么？

FILE A:
```c
#include <stdio.h>
void func1(void);
```

```c
int y;
int main()
{
    extern int x;
    y = y + 15;
    x = x + 10;
    printf("In main y = %d\n", y);
    printf("In main x = %d\n", x);

    func1();
    x = x + 5;
    y = y + 20;
    printf("In main y = %d\n", y);
    printf("In main x = %d\n", x);

    return 0;
}
```

FILE B:
```c
extern int y;
int x;

void func1(void) {
    y = y + 15;
    x = x + 5;
    printf("In func1 y = %d\n", y);
    printf("In func1 x = %d\n", x);
    return;
}
```

# 6.4 示例程序

示例程序展示了存储类的用法。这些程序已经执行过，输出位于每个程序的末尾。程序选取自科学与工程应用。

# 6.4.1 管道流量

编写一个程序来计算不同管道的流量，给定管道数量以及每个管道的直径（英尺）和流速（英尺/秒）。main 函数执行输入和输出，main 调用另一个文件中的计算函数。使用 extern 存储变量在两个文件之间传递数据。

流量的公式为：

$q = a \times v$

其中 $q$ 是以立方英尺为单位的流量，$a$ 是管道的截面积（平方英尺），$v$ 是水流通过管道的速度（英尺/秒）。

管道截面积的计算方式如下：

```
$a = \pi d^2 / 4.0$
```

其中 $d$ 是管道的直径（英尺）。

# 数据

- 输入数据是：直径 $d$（英尺）
- 流速 $v$（英尺/秒）

# 伪代码

```
FILE A
main
调用 funcinput()
调用 funccompute()
调用 funcoutput()
停止
```

funcinput:
输入直径和流速

funcoutput:
输出直径和流速
输出流量

FILE B: 需要访问名为 diameter 和 velocity 的变量，提供对名为 flowrate 变量的访问。

funcompute:
计算截面积

# 程序: flowa.c

#376 存储类

```c
#include <stdio.h>

#define NUMPIPS 5

int funcinput();
void funcoutput();
int funccompute();

FILE *inptr, *outptr;

float diameter, velocity;

int main()
{
    int count = 0;
    int flag;
    inptr = fopen("flowin.dat", "r");
    outptr = fopen("flowout.dat", "w");
    while(count < NUMPIPS) {
        flag = funcinput();
        if(flag) {
            funccompute();
            funcoutput();
        }
        count++;
    }
    fclose(inptr);
    fclose(outptr);
    return 0;
}
```

```c
************************************
/* funcinput: Input the Data */
************************************
/* Input Variables: */
/* diameter - diameter of feet */
/* velocity - velocity of feet per sec */
/* Returns status of input */
**************************************
int funcinput() {
    scanf(inptr, "%f %f", &diameter, &velocity);
    if(diameter <= 0 || velocity <= 0)
        return 0;
    return 1;
}
```

```c
************************************
/* funcoutput: Output the Data */
************************************
/* Output Variables: */
/* diameter - diameter of feet */
/* velocity - velocity of feet per sec */
/* flowrate - flow rate in cubic feet */
************************************
void funcoutput() {
    fprintf(outptr, "Diameter: %.2f feet Velocity: %.2f ft/sec\nFlow Rate: %.2f cft per sec\n", diameter, velocity, flowrate);
}
```

```c
************************************
/* funccompute: Computes the Flow Rate */
************************************
/* Constant: */
/* PI = 3.141593 */
************************************
void funccompute() {
    float area;
    area = PI*((diameter/12.0) * (diameter/12.0))/4.0;
    flowrate = area * velocity;

    return;
}
```

Input and Output
====================
INPUT FILE: "flowin.dat"
1.0 50.0
0.5 25.0
0.71 36.7
0.88 80.0
1.33 40.0

OUTPUT FILE: "flowout.dat"
Diameter: 1.00 feet Velocity: 50.00 ft/sec
Flow Rate: 39.27 cft per sec
Diameter: .50 feet Velocity: 25.00 ft/sec
Flow Rate: 4.91 cft per sec

Diameter: .71 feet Velocity: 36.70 ft/sec
Flow Rate: 14.53 cft per sec
Diameter: .88 feet Velocity: 80.00 ft/sec
Flow Rate: 15.57 cft per sec
Diameter: 1.33 feet Velocity: 40.00 ft/sec
Flow Rate: 47.33 cft per sec

