

## 6.3. 指针变体

你现在将深入研究 C 语言提供的不同指针变体。基本上，C 描述了三种指针变体。

它们是：

- 指针声明；
- 指针算术；
- 指针比较。

以上每种变体都有其要讲述的故事，但讨论将仅限于与你指针知识升级相关的内容。指针声明 如果你认为这又是另一个声明，这与之前的声明完全无关。

指针声明或可以称为指针赋值，是将特定变量的地址分配或初始化给另一个变量。也就是说，一个变量的值将是另一个变量的地址。考虑以下示例 x=&y; 在上述描述中，y 的地址是 x 的值，即，如果 y 的地址是 2457 且赋值完成，则 x 的值也将是 2457。

但变量 x 必须在实际使用前声明。如果你的脑海中仍有疑问，下面的图形表示应该可以消除它。x、y 的地址为 8123 和 2457。

如果地址必须输入到一个变量中，该变量应在 main 之后以特定方式声明。看下面。2457 5 int *x; 这就是指针变量的声明方式。上述声明告诉编译器变量 x 用于存储另一个变量的地址，因此这种类型声明的变量只能用于存储地址，而不能用于其他用途。这些称为指针变量，每个指针变量都应在其前面加上 * 运算符以及数据类型说明。

指针算术 当谈到算术时，你关心的领域将是研究算术是否可以纳入指针的概念中，如果可以，算术在指针中在多大程度上有效。令人遗憾的是，必须声明在指针中只能执行加法和减法运算，除此之外别无他法。

### 6.3.1. 加法

加法运算可以有效地使用指针进行，即可以对指针加上一个数字。

- 示例：
```
#include<stdio.h>
void main()
{
int i=4,*x,*y;
x=&i;
y=x+9;
printf("%d",y);
}
```

上面的示例是一个粗略的程序。你可以看到 x 和 y 被声明为指针变量，i 初始化为 4。下一步是将 i 的地址赋给 x，并将 x 的值加 9 并放入变量 y 中，在下一行打印出来。以类似的方式，也可以使用指针进行减法。y=x-9;

### 6.3.2. 指针比较

指针变量之间的比较可以进行，前提是两个变量都指向相同数据类型的对象。这种比较在两个指针变量都指向同一数组的元素时很有用。比较可以测试相等或不相等，并且指针变量也可以与零进行比较。

下面的程序给出了其如何进行的描述。

```
#include<stdio.h>
void main()
{
static int sub[]={10,20,30,40,50,60};
int *a,*b; a=&sub[4]; b=(sub+4);
if(a==b)
printf("pointers point to the same location.");
else
```

仅当它当前指向一个数组时才跨索引。

考虑以下内容：

```
#include<stdio.h>
void main()
{
static char arr[15]="MyDharm";
char *a = "MyDharm";
printf ("%s\n", arr);
printf("%s", a);
}
```

这里尽管 arr 和 a 的声明不同，但两个 printf 语句的输出是相同的。在第一个声明中，“MyDharm”存储在数组 arr [] 中；但在第二个中，“MyDharm”存储在内存中的某个位置，基地址存储在 a 中，换句话说 a 指向字符串中的第 0 个元素。

## 6.6. 指向指针的指针

这个概念只是指针的扩展。指针如你所知是一个包含变量地址的变量。但如果一个指针变量必须存储另一个指针变量的地址。（这仅在指针中才可能。）声明模式略有改变。存储另一个变量地址的变量在其前面声明一个 *（*i），如果指针变量必须存储另一个指针变量的地址，则该变量将有两个 *，即（**）后跟变量。观察变量是如何声明的。

```
int a; int *b; int **c;
```

这里 a 是一个普通的 int，b 是指向 int 的指针，而 *c 是指向 int 指针的指针。这种指向指针的指针的声明应该对你来说很清晰。尝试理解下一页给出的示例。

```
#include<stdio.h>
void main()
{
int a =3;
int*b; 6. int**c;
```

```
```c
b=&a;
c=&b;
printf("Address of a =%d\n",&a);
printf("Address of a =%d\n",&b);
printf("Address of a =%d\n",&*c);
printf("Address of b =%d\n",&b);
printf("Address of b=%d\n",&*c);
printf("Address of c=%d\n",&c);
printf("Value of b=%d\n",b);
printf("Value of c=%d\n",c);
printf("Value of a=%d\n",a);
printf("Value of a=%d\n",*(&a));
printf("Value of a=%d\n",*b);
printf("Value of a=%d\n",**c);
}
```
```

上述程序的输出将是：Address

Address of a=9876
Address of a =9876
Address of b =8765
Address of b =8765
Address of c =7654
Value of b=9876
Value of c=8765
Value of a =5
Value of a =5
Value of a =5
Value of a =5

将帮助你追踪程序如何打印上述输出。

a b c 5 9876 8765 9876 8765 7654.

## 6.7. 指向函数的指针

在之前的课程中你对函数及其不同类型进行了大量讨论 所以这里再次出现函数。你知道变量有地址，可以显示，或转移到指针变量。但这可以用指针来完成吗？可以，因为在 C 中甚至函数也有地址，你甚至可以将该值分配给另一个指针变量，但让我们慢慢来，先讨论如何找到函数的地址。

观察并分析下面的程序。

```
```c
#include<stdio.h>
main()
{
int disp();
printf(“The address of function is %d”,disp);
disp();
}
disp()
{
printf(“Ever heard of auntie viruses?”);
}
```
```

输出将是：

The address function is 3152

Ever heard of auntie viruses.

要显示函数的地址，你只需在 printf 语句中给出函数名，并且函数应连同数据类型一起声明。现在你知道了如何调用函数的地址，让我们继续学习如何将这些地址分配给指针变量。

```
```c
#include<stdio.h>
void main()
{
int disp();
int (*fun_ptr)();
```

```
fun_ptr=disp;
printf("address is %d",fun_ptr);
(*fun_ptr());
}
disp()
{
printf("aliens are tasty");
}
```

程序的输出将是：
address is 5211
ali ens are tasty.

你在遇到声明 int(*fun-ptr)(); 后一定感到困惑。好吧，把它当作一条规则，即要将函数地址传递给的指针应这样书写。其余程序应该很容易理解。

## 6.8. 返回指针的函数

你一定在想为什么函数要重生。原因是除非指针知识足够，否则这些概念无法解释。现在指针在某种程度上已进入你的血液，请注意函数不仅可以向调用函数返回值，还可以从被调用函数返回指针。然而，必须纳入某些规则才能实现这一壮举。要使函数返回指针，必须在调用函数以及函数声明中明确提及。以下程序说明了这一点。

```
#include<stdio.h>
void main()
{
int *a; int *func();
a=func();
printf("value of A is",a);
}
int *func()
```

