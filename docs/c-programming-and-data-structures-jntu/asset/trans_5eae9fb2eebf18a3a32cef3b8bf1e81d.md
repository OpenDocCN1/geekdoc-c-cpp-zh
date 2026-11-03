
## C.24 已解答试题

```c
#include<stdio.h>
#include<conio.h>
#include<math.h>

void square(int);

main()
{
    int x,y;
    printf("enter the value of x");
    scanf("%d",&x);
    square(x);
    y=sqrt(x); /* call to a built-in function */
    printf("%d",y);
}

void square(int a)
{
    int p;
    p=a*a;
    printf("%d",p);
}
```

### 3. 使用数组有什么优点？给出一维数组的声明、访问和打印语法。

答：

数组是赋予一组相似元素的集合名称，而变量是程序执行期间的任意实体。

以下是数组的优点。

- 数组是一种能够处理多个值的变量，而普通变量一次只能保存一个值。例如，数组初始化可以写成 `int number[8];`，此时会保留八个存储位置，可存储八个属于同一类型的不同值。普通变量初始化可以写成 `int number;`，只保留一个存储位置，一次只能保存一个值。
- 数组元素可以在声明它们的时间和位置进行初始化。

```c
int a[4] = {5,6,7,8};
```

在上面的示例中，数组 `a` 中存储了四个元素。数组元素存储在连续的内存位置中。数组元素从 '0' 开始读取，即 `a[0]` 被赋值为 '5'。类似地，`a[1]` 被赋值为 6。`a[4]` 中的数字 4 表示元素的总数。

需要满足的条件是数组的所有元素必须具有相同的数据类型。所声明数组的类型。以上是关于使用数组的优点。下面介绍一维数组的声明、访问和打印语法。

### 一维数组

它是最简单的数组形式，其中元素列表存储在连续的内存位置中，并且仅使用一个下标进行访问。

示例：

```c
int abc[10];
```

这里 `abc` 是一个包含 10 个整数的数组。

### 一维数组的声明

声明数组的一般格式如下：`dataType array_name [size];`，其中 `dataType` 是数组元素的数据类型，`array_name` 是数组变量的名称，`size` 指定数组中元素的数量。数组的大小在编译时固定，在程序执行期间不能更改。

示例：

```c
int a[50];
```

这里，数组 `a` 可以保存 50 个整数。

数组的总大小为 2*50=100 字节。这是因为每个整数元素需要 2 字节存储。

### 初始化和访问

我们可以在声明数组元素的位置直接初始化它们。这种初始化的一般格式为：`Type array_name [size]={list of elements separated by commas}`

示例：`int a[4]={5,10,1,55};` 这里该数组的大小为 4，5 被赋给第一个元素，即 `a[0]=5`，10 被赋给第二个元素，即 `a[1]=10`，1 被赋给第三个元素，即 `a[2]=1`，55 被赋给第四个元素 `a[3]=55`。假设指定的元素列表少于数组大小，则只初始化相应数量的元素。其余元素被赋予垃圾值。

示例：`int xyz[5]={10,5,20};` 这里，第一个元素被赋值为 10，第二个元素被赋值为 5，第三个元素被赋值为 20。由于元素列表少于数组大小，其余两个元素被赋予垃圾值。索引通常从 0 到 n-1，即对于数组 `a[n]`，其值从 `a[0],a[1],.....a[n-1]`。`xyz[0]=10, xyz[1]=5, xyz[2]=20, xyz[3]` 被赋予垃圾值。`xyz[4]` 被赋予垃圾值。

考虑以下语句

```c
int xyz[] = {5,6,7,8,9};
```

在上面的语句中，我们没有指定数组的大小。在这种情况下，编译器会根据列表中的值的数量来确定数组的大小。在上面的语句中，由于列表中有五个值，因此数组的大小为 5。

如果我们想要初始化一个大尺寸数组的元素（假设有 250 个元素），那么在声明时初始化这样的数组是很困难的。在这种情况下，必须显式地进行声明。在 C 语言中，我们使用循环（while、for、do-while）来初始化元素。在 C 语言中，初始化这种大小的数组没有捷径。

下面是一个关于一维数组的程序。

```c
/* Program showing one-dimensional array */
#include<stdio.h>
#include<conio.h>

main ( )
{
    int i;
    float x[10], value, total;
    /* reading values into array */
    printf("enter 10 real numbers\n");
    for(i=0;i<10;i++)
    {
        scanf("%f",&value);
        x[i]=value;
    }
    /* computation of total */
    total = 0.0;
    for(i=0;i<10;i++)
        total= total+x[i]*x[i];
    /* printing of x[i] values and total */
    printf("\n");
    for(i=0;i<10;i++)
        printf("x[%2d]=%5.2f \n", i+1,x[i]);
    printf("\n total =%2f \n", total);
}
```

10 个实数的输出：1.1, 2.2, 3.3, 4.4, 5.5, 6.6, 7.7, 8.8, 9.9,10.10。

### 4. 定义结构体，并写出声明和访问成员的一般格式。

答：结构体：

当你想要访问由不同类型元素组成的数据时，不能使用数组来实现，因为数组是相似数据项的集合。假设你想存储有关学生的信息。每个学生都有姓名、学号和所学专业。这整个信息不能存储在单个数组中，因为学生信息由不同类型的数据组成[姓名是字符串，学号是整数，专业是字符串]。为处理这类数据，C 提供了一种称为结构体的派生数据类型。

![](img/65953ea584e494f3d396b2252cb5ea53_528_0.png)

### 结构体定义

结构体是不同数据类型的数据项在单一名称下的集合。或者说，结构体是异构数据项的集合。

结构体的声明如下

```c
struct <tag>
{
    data type member1;
    data type member2;
    .........
    ..........
    data type member n;
};
```

- 在此声明中，`struct` 是关键字。
- `<tag>` 是赋予所声明结构体的名称。
- 数据类型可以是整型、浮点型、字符型或任何其他数据类型。
- `member1, member2,......member n` 是结构体的成员。各个成员可以是变量、指针、数组或其他结构体。
- 各个成员不能在结构体定义内初始化。在结构体声明之后，各个结构体类型变量的声明如下：

  ```c
  struct <tag> variable1,variable2........variable n;
  ```

- `variable1, variable2..........variable n` 是类型为 `tag` 的结构体变量。
- 右花括号之后必须指定分号 ';'。
- 结构体成员本身不占用任何空间。只有在声明结构体变量之后才会分配内存。

结构体可以这样声明：

```c
struct tag
{
    Type 1 data 1;
    Type 2 data 2;
    ..........
    Type n data n;
} variable1, variable2, ......variable n;
```

在上述声明中，tag 是可选的

```c
struct
{
    char name[26];
    int age;
    char gender[6];
    char occupation[25];
} p1,p2;
```

在上述声明中，无需指定结构体名称。

### 访问结构体成员

可以通过编写 `variable name.member` 来访问结构体成员。点（`.`）运算符将结构体变量与数据成员关联起来。它是优先级最高的运算符，并且从左到右结合。

### 为结构体赋值

一种方法是在声明结构体变量时赋值。

```c
struct person p1={"ravi","21","male"};
```

另一种方法是分别给每个成员赋值，如下所示。

```c
strcpy(p1.name,"ravi");
p1.age=21;
strcpy(p1.gender,"male");
strcpy(p1.occupation,"student");
```

下面是一个演示带有初始化值的结构体的示例。

```c
/* structure with initialized values */
#include<stdio.h>
#include<conio.h>
void main ()
{
    struct organization
    {
        char name[20];
        char designation[20];
        int sal;
    };
    struct organization emp1={"ramu","secretary","8000"};
    struct organization emp2={"raju","manager","18000"};
}
```

