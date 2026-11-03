
```c
}
default:
{
    printf("\n\t\t u have Entered out of option okay!!!");
}
}
getch();
}

int addi(int a, int b) /* function body & definition*/
{
    return(a+b);
}
int subt(int a, int b) /* function body & definition*/
{
    return(a-b);
}
int multi(int a, int b) /* function body & definition*/
{
    return(a*b);
}
float div(int a,int b) /* function body & definition*/
{
    float z;
    z=(float) (a/b);
    return(z);      /* function return type  */
}
```

![](img/3a2b6e5e90a58a56458b0539952c0cd2_388_0.png)

C 程序员 Harry。

![](img/3a2b6e5e90a58a56458b0539952c0cd2_388_1.png)

## 章节

## ∞ 18- 部分 –II ∞

## (在 C 库中创建并插入自己的函数。)

## 在 C 库中创建并插入自己的函数。

正如你们所熟知，大多数时候我们使用标准的“C”库函数——有时也会使用用户自定义函数。但我最想在这里展示的是，如何将我们自己编写的“C”函数添加到漂亮的“C”标准库中？？

确实是可能的，这是在“C”编程中的专家做法。在将用户自定义函数添加到标准 C 库之后，我们可以随时轻松访问它们，请阅读步骤。

## 第 1 步 -

大多数“C”编译器在编译器实用程序中提供一个特殊的选项菜单，利用此实用程序我们可以轻松完成此任务。我认为在 Turbo C/C++ 编译器中提供了一个名为 “tlib.exe” 的实用程序，Turbo Librarian。让我们使用此实用程序并将函数添加到“C”库中。

## 第 2 步 –

这里我将我的阶乘函数添加到“C”库中 -

(a) 在某个文件中编写 factorial() 的函数定义，可以是 fact.c

```c
int factorial(int num)
{
    int i,f=1;
    for(i=1;i<=num;i++)
        f=f*i;
    return(f);
}
```

(b) 使用 Alt+F9 编译此 “fact.c” 文件，现在会自动创建一个名为 “fact.obj” 的新文件，其中包含机器语言中的编译代码。
(c) 通过发出以下命令将函数添加到库 “maths.lib” 中- c:\>tlib maths.lib+c:\fact.obj

这里，“maths.lib”是库文件名，+ 是一个开关，c:\fact.obj 是要添加到 maths.lib 中的文件的路径

(d) 在头文件中声明 factorial() 函数的原型，例如 “fact.h”，调用函数时应包含此文件，不要忘记。

(e) 例如，请看这里如何在任何程序中使用或调用我们添加的函数-

```c
#include "c:\fact.h"
#include<stdio.h>
#include<conio.h>
void main()
{
int f;
f=factorial(5);
printf("%d",f);
getch();
}
```

## 删除 C 库中的自己的函数。

步骤 - 只需在此处使用减号

(c) 通过发出以下命令将函数添加到库 “maths.lib” 中-

```
c:\>tlib maths.lib -c:fact.obj
```

## 创建自己的 C 库 -

假设你想创建一个自己的库，其中包含三个或更多你想要的自己的函数，例如：

- 1. factorial()
- 2. prime()
- 3. Fibonacci()

注意：这仅适用于 Turbo C/C++ 编译器，请遵循我的以下说明——

## 第 1 步 -

在名为 'myfuncs.c' 的文件中定义函数 factorial()、prime()、fibonacci()。不要在此文件中定义 main()。

```
int factorial(int);
int prime(int);
void fibonacci(int);
```

## 第 2 步:-

从编译器的选项菜单中选择 'Application' 选项，然后从弹出的对话框菜单中选择 'library' 选项

## 第 3 步:-

使用 Alt+F9 编译程序。这将创建名为 'myfuncs.lib' 的库文件。

## 步骤：4:-

完成啦，太棒了！！你的库现在已创建完成。现在你可以轻松使用这些函数，我将向你展示如何使用之前创建的函数库。

```
#include<stdio.h>
#include<conio.h>
#include"myfuncs.h"
void main()
{
int f,result;
f=factorial(5);
result=prime(13);
fibonacci(6);
printf("\n %d %d",f,result);
getch();   }
```

## 注意:-

'myfuncs.h' 文件应与 'sample.c' 文件位于同一目录中。如果不是，则在包含 'myfuncs.h' 时请指定适当的路径。

## 步骤:-

进入编译器菜单 'project' 并选择 'open project' 选项。然后弹出窗口出现，输入项目名称，例如 'sample.prj'，然后确定。

## 步骤:-

从项目菜单中选择 'Add item'，这样会弹出一个文件对话框。选择文件 'sample.c' 然后选择 'Add'，同样以相同的方式添加文件 'myfuncs.h.lib'，选择 Done！

## 步骤:-

使用 Ctrl+F9 编译并执行项目。

![](img/3a2b6e5e90a58a56458b0539952c0cd2_392_0.png)

![](img/3a2b6e5e90a58a56458b0539952c0cd2_392_1.png)

## 章节

## ∞ 19- 部分 –II ∞

## (Graphics programming)

## *****Graphics programming*****

## *******************************

## 介绍-

要运行图形代码，请确保已在操作系统中安装了图形驱动软件。某些图形代码需要超过 250 MB 内存的显卡。

## 130. 编写程序在“C”中绘制椭圆或圆。

```c
#include<stdio.h>
#include<conio.h>
#include<graphics.h>
void main()
{
int gd=DETECT,gm;   /*initiate graphics mode*/
initgraph(&gd,&gm,""); /*initiate graphics driver & mode*/

circle(200,200,100); /*To draw a circle*/
ellipse(450,200,0,360,150,100);
outtextxy(175,200,"circle");
outtextxy(425,200,"ellipse");
getch();
}
```

## 131. 编写程序使用线函数（全部三种）绘制矩形。

```c
#include<stdio.h>
#include<conio.h>
#include<graphics.h>
void main()
{
int gd=DETECT,gm;   /*initiate graphics mode*/
initgraph(&gd,&gm,""); /*initiate graphics driver & mode*/
line(75,50,200,50);
```

```
line(200,50,200,100);
line(200,100,75,100);
line(75,100,75,50);
outtextxy(10,50,"(50,50)");
outtextxy(200,50,"(200,50)");
outtextxy(200,100,"(200,100)");
outtextxy(10,100,"(50,100)");
outtextxy(75,115,"(50,100)");
moveto(75,150);   /*it moves starting position*/
lineto(200,150);
lineto(200,200);
lineto(75,200);
lineto(75,150);
outtextxy(75,215,"using function lineto()");
moveto(75,250);
linerel(125,0);
linerel(0,50);
linerel(-125,0);
linerel(0,-50);
outtextxy(75,315,"using function linerel()");
getch();
}
```

## 132. 编写程序使用不同的线型绘制矩形。

```c
#include<stdio.h>
#include<conio.h>
#include<graphics.h>
void main()
{
int gd=DETECT,gm;   /*initiate graphics mode*/
initgraph(&gd,&gm,"");/*initiate graphics driver & mode*/
setlinestyle(1,0,3);
line(75,50,200,50);
line(200,50,200,100);
line(200,100,75,100);
line(75,100,75,50);
outtextxy(10,50,"(50,50)");
outtextxy(200,50,"(200,50)");
```

```
outtextxy(200,100,"(200,100)");
outtextxy(10,100,"(50,100)");
outtextxy(75,115,"(50,100)");
setlinestyle(2,0,1);
moveto(75,150);   /*it moves starting position*/
lineto(200,150);
lineto(200,200);
lineto(75,200);
lineto(75,150);
outtextxy(75,215,"using function centreline()");
setlinestyle(0,0,3);
moveto(75,250);
linerel(125,0);
linerel(0,50);
linerel(-125,0);
linerel(0,-50);
outtextxy(75,315,"using function solidline()");
getch();
}
```

## 其他图形命令或函数，你可以使用任何类似的函数 -

- 1, bar() -用于绘制条形。
- 语法:- bar(int left,int top,int right,int bottom);
- 2, bar3d() -用于绘制 3d 条形。
- 语法:- bar3d(int left,int top,int right,int bottom,int depth,int top flor);
- 3, cleardevice() - 用于清除图形屏幕。
- 语法:- cleardevice();
- 4, closegraph() - 危险，它关闭图形系统。
- 语法:- closegraph();
- 5, drawpoly() - 它绘制多边形的轮廓
- 语法:- drawpoly(int numpoints,int farpolypoints)
- 6, getbkcolor - 它返回背景颜色。
- 语法:- int A= getbkcolor();

7, getcolor() - 它返回当前绘图颜色。
**语法:-** int A= getcolor();

8, getmaxx() - 返回屏幕 x 的最大值。
**语法:-** int A= getmaxx();

9, getmaxy() - 返回屏幕 y 的最大值。
**语法:-** int A= getmaxy();

10, getpixel() - 它获取指定像素的颜色。
**语法:-** unsigned A= getpixel(int x,int y);

11, getx() - 它返回 x 的当前位置。
**语法:-** int A= getx();

12, gety() - 它返回 y 的当前位置。
**语法:-** int A= gety();

13, outtext() - 它在图形模式下在 x 和 y 的当前位置显示字符串。
**语法:-** outtext("string");

14, outtextxy() - 它在图形模式下在指定位置显示字符串。
**语法:-** outtextxy(int x,int y,"string");

15, setbkcolor() - 如果设置背景颜色。
**语法:-** setbkcolor(int color);

16, setcolor() - 设置绘图颜色。
**语法:-** setcolor(int color);

## 绘制和填充图像函数 -

- 1, EMPTY-FILL 0 -用于填充背景颜色。
- 2, SOLID-FILL 1 -用 BG 颜色填充区域。
- 3, LINE-FILL 2 -用 SMACK BG 颜色填充区域。
- 4, BKSLASH-FILL 3 -用粗线填充。
- 5, HATCH-FILL 7 -用浅斜线填充。

