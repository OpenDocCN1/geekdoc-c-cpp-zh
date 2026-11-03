
因为变量被声明为 *static*，其值在函数调用之间得以保留。

- 作为奖励，*static* 变量声明会被初始化为零。
- 关键字 *static* 定义了一种存储类别。参见附近的侧边栏，“变量关键字汇总”。
- 除非变量的值必须在每次函数调用时保留，否则无需将变量声明为 *static*。这种情况时有发生。另请参阅后面的章节“使用外部变量”。
- 从函数返回的值无需声明为 *static*。当你返回一个值，例如

  ```c
  return(a);
  ```

  只有变量的值被返回，而不是变量本身。这种方法唯一的挑战出现在分配内存作为缓冲区时。缓冲区的数据会被丢弃，如果你希望调用函数能够访问它，则应将其声明为 *static*。参见第19章。

## 到处都是变量

有时，变量必须像蜂窝电话服务一样：无处不在且可从任何函数访问。通常被称为 *global* 变量，在 C 中它正式称为外部变量。

## 使用外部变量

外部变量通过使变量声明对源代码文件中的所有函数可用，从而解决特定问题。任何函数都可以访问该变量。它不必作为参数传递给函数或从函数返回。

Listing 16-6 显示了外部变量是如何声明和使用的。变量 *age* 和 *feet* 是外部的。它们都被源代码中的所有函数使用并操作。

## LISTING 16-6: 到处抛掷你的年龄

```c
#include <stdio.h>

void half(void);
void twice(void);

int age;
float feet;

int main()
{
    printf("How old are you: ");
    scanf("%d",&age);
    printf("How tall are you (in feet): ");
    scanf("%f",&feet);
    printf("You are %d years old and %.1f feet tall.\n", age,feet);
    half();
    twice();
    printf("But you're not really %d years old or %.1f feet tall.\n",age,feet);
    return(0);
}

void half(void)
{
    float a,h;
    a=(float)age/2.0;
    printf("Half your age is %.1f.\n",a);
    h=feet/2.0;
    printf("Half your height is %.1f.\n",h);
}

void twice(void)
{
    age*=2;
    printf("Twice your age is %d.\n",age);
    feet*=2;
    printf("Twice your height is %.1f\n",feet);
}
```

第6行声明外部 int 变量 age，第7行创建外部 float 变量 feet。这些变量在任何函数之外声明，位于 #include、#define 和原型声明区域。变量对每个函数都可用。即使在 twice() 函数中更改了这些值，main() 函数也会使用新值。

请注意 main() 函数中的两个 printf() 语句将其文本用单引号括起来。你不需要在文本编辑器中将这些语句括起来；只需将每一行输入为单行即可。

练习 16-7：将 Listing 16-6 的源代码输入到你的编辑器中，创建一个新程序。构建并运行。

尽管 age 和 feet 变量都是外部的，但 extern 关键字并未用于声明它们。该关键字仅在链接多个源代码文件（模块）时才需要。在这种配置下，该关键字标识在单个源代码文件中可用但未在当前文件中声明的外部变量。第24章详细解释了如何使用 extern 关键字。

![](img/dcc0cd79d4a45cfce24fa49d85442884_258_0.png)

![](img/dcc0cd79d4a45cfce24fa49d85442884_258_1.png)

> 不要懒于使用全局变量！如果可以把值传递给函数，就这样做！这是正确的做法。太多懒惰的程序员将所有变量声明为外部变量来“解决问题”。这种做法很粗糙也不恰当。
> 
> 全局变量的良好示例包括程序中所有函数必须访问的信息。例如，状态设置、用户信息以及难以传递给每个函数的其他项目，都是外部变量的绝佳候选。
> 
> 在我的编程历史中，很少有代码需要外部变量。只有当我无法想出其他方法使信息可用时，我才会将变量声明为全局。

## 创建外部结构体变量

当向函数传递结构体时，就会出现完全需要外部变量的情况。在这种情况下，你必须在外部声明结构体，以便所有函数都可以访问给定结构体类型的变量。此外，结构体必须在结构体作为参数出现的任何函数原型之前声明。

不要让 Listing 16-7 的庞大长度吓到你！你最终编写的大多数“真实”程序会更长！

## **LISTING 16-7:** 向函数传递结构体

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

struct bot {
    int xpos;
    int ypos;
};

struct bot initialize(struct bot b);

int main()
{
    const int SIZE = 5;
    struct bot robots[SIZE];
    int x;

    srand((unsigned)time(NULL));

    for(x=0;x<SIZE;x++)
    {
        robots[x] = initialize(robots[x]);
        printf("Robot %d: Coordinates: %d,%d\n",
            x+1,robots[x].xpos,robots[x].ypos);
    }
    return(0);
}

struct bot initialize(struct bot b)
{
    int x,y;

    x = rand();
    y = rand();
    x%=20;
    y%=20;
    b.xpos = x;
    b.ypos = y;
    return(b);
}
```

要向函数传递结构体，必须在外部声明结构体，这在 Listing 16-7 的第5行到第8行之间发生。该声明必须在函数原型化之前进行，而原型化在第10行进行。

*initialize()* 函数从第39行运行到第40行。结构体被传递给函数并返回。请注意，结构体变量必须作为参数完全定义。在第29行，结构体在函数内部被赋予变量名 `b`。

第39行的 *return* 语句将结构体传回调用函数。的确，*initialize()* 函数被定义为结构体 `bot` 数据类型。这是它返回的值的类型。

**练习 16-8：** 鼓起勇气，将 Listing 16-7 中的所有源代码行输入到你的编辑器中。构建并运行。

输出演示了结构体数组是如何一次一个元素地传递给函数、在函数中修改，然后返回的。

## 枚举

*enum* 关键字不必让你困惑。相反，每当你必须声明一系列顺序编号的常量时，就沉浸在它的温暖舒适中。Listing 16-8 显示了一个你可能熟悉的示例。

**LISTING 16-8:** 验证输入值

```c
#include <stdio.h>

int verify(int check);

int main()
{
    int s;

    printf("Enter a value (0-100): ");
    scanf("%d",&s);
    if(verify(s))
    {
        printf("%d is in range.\n",s);
    }
    else
{
	printf("%d is out of range!\n",s);
}
return(0);
}

int verify(int check)
{
	enum { false, true };
	if(check < 0 || check > 100)
	return false;
	return true;
}
```

Listing 16-8 中显示的代码是对第10章练习10-15解决方案的修改。enum 关键字在第24行用于声明两个常量值：false 和 true。这些常量被赋值为 0 和 1，在代码中用于表示 TRUE 和 FALSE 条件。

练习 16-9：将 Listing 16-8 的源代码输入到你的编辑器中。保存。构建。运行。

enum 关键字非常适合声明一组顺序常量。在 Listing 16-8 中，它声明了 false 和 true，将零赋给 false 的值，将 1 赋给 true。该关键字节省了多次常量声明的时间。例如。

```c
const int zero = 0;
const int one = 1;
const int two = 2;
const int three = 3;
```

这四条语句可以通过使用单个 enum 语句来表达：

```c
enum { zero, one, two, three };
```

enum 关键字后面跟着一组大括号。它们包含常量声明，以逗号分隔，如刚才所示。第一个常量被赋值为零，每个后续常量的值递增一。该语句可以出现在函数中，如 Listing 16-8 所示，也可以外部声明。
