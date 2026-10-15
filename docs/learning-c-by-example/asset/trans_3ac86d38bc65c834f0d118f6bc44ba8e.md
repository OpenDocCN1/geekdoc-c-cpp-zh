
## 2.4 注释

你可以通过编写 C 语言来解释你的代码是如何工作的。为此，你可以使用 // 和 /* */ 语法。以下是示例代码：

```
// bank account
char accountCode;

/* parameters*/
int p1, p2, p3, p4;
```

## 2.5 控制台输入与输出

你可能想要使用 C 语言在控制台上显示消息。可以使用 printf() 在控制台上写入消息。printf() 内部也可以传入参数，使用 %d 表示整数数值，使用 %f 表示浮点数值。对于字符数据类型，我们可以使用 %c 来传入参数。

以下是示例代码

```
#include <stdio.h>

int main() {
    int n = 10;
    float m = 1.245;
    char c = 'A';

    printf("%d \n",n);
    printf("%f \n",m);
    printf("%.2f \n",m);
    printf("%.3f \n",m);
    printf("%c \n",c);

    return 0;
}
```

将这段代码保存到一个名为 inout.c 的文件中。

编译并运行这段代码

![](img/4e69d9ab92a6fdfd6a6bac3671deb952_21_0.png)

你可以看到 %f 输出了带 6 位小数的浮点数据。你可以通过在点号（.）后传入数值来指定小数位数，例如 %.2f 和 %.3f。

## 2.6 算术运算

C 语言支持四种基本算术运算，如加法、减法、乘法、除法。以下是基本算术的代码示例：

```
```c
#include <stdio.h>

int main() {
        int a,b,c;
        a = 10;
        b = 6;

        c = a + b;
        printf("%d + %d = %d\n",a,b,c);

        c = a - b;
        printf("%d - %d = %d\n",a,b,c);

        c = a * b;
        printf("%d * %d = %d\n",a,b,c);

        float d = a / b;
        printf("%d / %d = %.2f\n",a,b,d);

        float e =(float)a / b;
        printf("%d / %d = %.2f\n",a,b,e);

        return 0;
}
```
```

将此程序保存到一个名为 **arith.c** 的文件中。编译并运行它。

程序运行：

![](img/4e69d9ab92a6fdfd6a6bac3671deb952_22_0.png)

## 2.7 数学函数

C 语言提供了数学库来处理数学运算。你必须包含 **math.h** 才能实现数学运算。

以下是数学函数使用的示例代码：

```
```c
#include <stdio.h>
#include <stdlib.h>

#include <math.h>

int main() {
        float a;
        float b;
        float pi = 3.14;

        a = 0.25;
        printf("value a = %.2f \n", a);

        b = abs(-a);
        printf("abs(a)=%.2f \n", b);

        b = acos(a);
        printf("acos(a)=%.2f \n", b);

        b = asin(a);
        printf("asin(a)=%.2f \n", b);

        b = atan(a);
        printf("abs(a)=%.2f \n", b);

        b = atan2(a,5);
        printf("atan(a,5)=%.2f \n", b);

        b = cos(a);
        printf("cos(a)=%.2f \n", b);

        b = sin(a);
        printf("sin(a)=%.2f \n", b);

        b = tan(a);
        printf("tan(a)=%.2f \n", b);

        b = sqrt(a);
        printf("sqrt(a)=%.2f \n", b);

        return 0;
}
```
```

将这段代码保存到一个名为 **mathdemo.c** 的文件中。然后编译并运行它。由于我们使用了 math.h，编译时需要添加 -lm 参数。

```
```bash
$ gcc mathdemo.c -lm -o mathdemo
$ ./mathdemo
```
```

程序输出如下图所示。

![](img/4e69d9ab92a6fdfd6a6bac3671deb952_24_0.png)

## 2.9 逻辑运算符

这些运算符可用于判断变量或值之间的逻辑关系。

| && | 与 |
| || | 或 |
| ! | 非 |

为了演示如何在 C 代码中使用逻辑运算符，你可以编写以下代码。

```
#include <stdio.h>

int main() {
    int a,b;
    a = 5;
    b = 8;

    printf("%d \n",a>b && a!=b);
    printf("%d \n",!(a>=b));
    printf("%d \n",a==b || a>b);

    return 0;
}
```

将这段代码保存到一个名为 logical.c 的文件中。编译并运行它。

![](img/4e69d9ab92a6fdfd6a6bac3671deb952_26_0.png)

## 2.10 自增与自减

想象你有如下操作

```
num = num + 1;
```

你可以使用 ++ 简化这个语法。

```
num++;
```

对于以下情况，使用相同的方法

```
num = num - 1;
```

你可以使用 -- 语法。

```
num--;
```

现在看看如何在代码中实现它们。让我们编写以下代码。

```
#include <stdio.h>

int main() {
    int a = 10;

    a++;
    printf("%d \n",a);

    a++;
    printf("%d \n",a);

    ++a;
    printf("%d \n",a);

    a--;
    printf("%d \n",a);

    a--;
    printf("%d \n",a);

    --a;
    printf("%d \n",a);

    return 0;
}
```

将这段代码保存到一个名为 incdec.c 的文件中。

编译并运行它。以下是程序输出示例。

agusk@ubuntu01:~/Documents/codes$ gcc incdec.c -o incdec
agusk@ubuntu01:~/Documents/codes$ ./incdec
11
12
13
12
11
10
agusk@ubuntu01:~/Documents/codes$

## 2.11 判断

在 C 语言中，有两种实现判断的方法。我们可以使用 if..then 和 switch..case。

### 2.11.1 if..then

if..then 的语法模型可以表示为以下形式：

```
if (conditional) {
    // do something
}else{
    // do another job
}
```

条件可以通过逻辑运算和/或比较运算得到。

以下是示例代码：

```
#include <stdio.h>

int main() {
    int a, b;
    a = 5;
    b = 8;

    if(a>b || a-b<a){
        printf("conditional-->a>b || a-b<a \n");
    }else{
        printf("..another \n");
    }
    return 0;
}
```

将此程序保存到一个名为 ifdemo.c 的文件中。然后运行该文件。

程序运行：

![](img/4e69d9ab92a6fdfd6a6bac3671deb952_29_0.png)

### 2.11.2 switch..case

switch..case 可以声明如下：

```
switch(option){
    case option1:
        // do option1 job
        break;
    case option2:
        // do option2 job
        break;
}
```

以下是 switch..case 用法的示例代码：

```
#include <stdio.h>

int main() {
    // you can obtain input value from keyboard
    // or any input device
    int input = 3;

    switch(input){
    case 1:
        printf("choosen 1\n");
        break;
    case 2:
        printf("choosen 2\n");
        break;
    case 3:
    case 4:
        printf("choosen 3\n");
        break;
    }
    return 0;
}
```

将这段代码保存到一个名为 switch.c 的文件中。尝试编译并运行它。

程序运行：

```
```bash
agusk@ubuntu01:~/Documents/codes$ ls
a.out      comp.c     ifdemo.c    linout.c    mathdemo.c    var1
arith      comp.c~    ifdemo.c~   logical     mathdemo.c~   var1.c
arith.c    hello      incdec      logical.c   switch.c      var1.c~
arith.c~   hello.c    incdec.c    logical.c~  switch.c~     var.c
comp       hello.c~   incdec.c~   mathdemo    var          var.c~
agusk@ubuntu01:~/Documents/codes$ gcc switch.c -o switch
agusk@ubuntu01:~/Documents/codes$ ./switch
choosen 3
agusk@ubuntu01:~/Documents/codes$
```
```

## 2.12 迭代

迭代操作在需要重复执行某些活动时非常有用。我们使用 for 和 *while* 语法。

### 2.12.1 For 循环

展示迭代场景的简单示例是显示数字列表。我们进行迭代，直到数字值小于 10。

```
#include <stdio.h>

int main() {
    int i;
    for(i=0;i<10;i++){
        printf("data %d\n",i);
    }
    return 0;
}
```

将这段代码保存到一个名为 for.c 的文件中。编译并运行它。

以下是程序输出：

![](img/4e69d9ab92a6fdfd6a6bac3671deb952_32_0.png)

### 2.12.2 While 循环

以下是与 2.12.1 场景相同的代码，但它使用了 *while* 语法。

```
#include <stdio.h>

int main() {
    int num = 0;
```

```
while(num<10){
    printf("data %d\n",num);
    num++;
}
return 0;
}
```

将这段代码保存到一个名为 **while.c** 的文件中。尝试编译并运行它。

![](img/4e69d9ab92a6fdfd6a6bac3671deb952_33_0.png)

## 2.13 结构体

我们可以定义一个结构体来声明一个新的数据类型。我们使用 struct 关键字。例如，我们定义一个名为 employee 的新数据类型。

创建一个名为 **structdemo.c** 的文件，并编写以下代码。

```
#include <stdio.h>

// define a struct
struct employee{
    int id;
    char name[10];
    char country[5];
};

int main() {
    // declare struct variable
    struct employee emp;
    // set values
    emp.id = 10;
    sprintf(emp.name,"jane");
    sprintf(emp.country,"DE");
    // display
    printf("id: %d, name: %s, country: %s\n",emp.id,emp.name,emp.country
    return 0;
}
```

保存这段代码。

现在编译并运行这个程序。

```
$ gcc -o structdemo structdemo.c
$ ./structdemo
```

程序输出示例见下图，Mac 平台。

