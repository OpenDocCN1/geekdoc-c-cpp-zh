
也可以将模板声明和变量声明合并在一行语句中。

The declaration

```
struct book_bank
{
  char title[20];
  char author[15];
  int pages;
  float price;
} book1, book2, book3;
```

是有效的。标签名的使用是可选的。例如，

```
struct
{
  ........
  ........
} book1, book2, book3;
```

声明 book1、book2 和 book3 为表示三本书的结构变量，但没有包含标签名以便在后续声明中使用。

通常，结构定义出现在程序文件的开头，在任何变量或函数定义之前。它们也可以与宏定义一起出现在 main 之前，例如 #define。在这种情况下，定义是全局的，也可以被其他函数使用。

## 12.3 为成员赋值

我们可以以多种方式为结构成员赋值。如前所述，成员本身不是变量。它们应与结构变量关联起来，使其成为有意义的成员。例如，单词 title 本身没有意义，而短语 'book3 的 title' 具有意义。成员与变量之间的关联是通过成员运算符 '.' 建立的，也称为 'dot operator' 或 'period operator'。例如，

```
book1.price
```

是表示 book1 价格的变量，可以像任何其他普通变量一样处理。以下是我们为 book1 的成员赋值的方式：

```
strcpy(book1.title, "BASIC");
strcpy(book1.author, "Balagurusamy");
book1.pages = 250;
book1.price = 28.50;
```

我们也可以使用 scanf 通过键盘给出值。

```
scanf("%s\n", book1.title);
scanf("%d\n", &book1.pages);
```

是有效的输入语句。

## 12.6 C 编程与数据结构

结构定义连同程序一起显示在图 12.1 中。scanf 和 printf 函数说明了成员运算符 '.' 如何用于将结构成员链接到结构变量。变量名加上句点和成员名可像普通变量一样使用。

### 示例 12.1

```
```c
/* DEFINING AND ASSIGNING VALUES TO STRUCTURE MEMBERS */
struct personal
{
    char name[20];
    int day;
    char month[10];
    int year;
    float salary;
};

main()
{
    struct personal person;
    printf("Input Values\n");
    scanf("%s %d %s %d %f",
           &person.name,
           &person.day,
           &person.month,
           &person.year,
           &person.salary);
    printf("%s %s %d %.2f\n",
           person.name,
           person.day,
           person.month,
           person.year,
           person.salary);
}
```
```

输入值
M.L. Goel 10 January 1945 4500.00
M.L. Goel 10 January 1945 4500.00

![](img/65953ea584e494f3d396b2252cb5ea53_336_0.png)

像其他任何数据类型一样，结构变量可以被初始化。然而，如果要在函数内部初始化结构，则必须将其声明为 static（类似于数组）。

注意：此条件不适用于 ANSI 编译器。ANSI 标准允许使用 auto 存储类别初始化结构变量。因此在使用 ANSI 编译器时我们可以删除 static 关键字。然而，在程序中使用 static 关键字可以使我们在旧标准和 ANSI 标准编译器下都能运行它们。

```
main()
{
    static struct
    {
        int weight;
        float height;
    }
    student = {60, 180.75};
    ....
    ....
}
```

这将值 60 分配给 student.weight，将 180.75 分配给 student.height。成员与其初始化值之间存在一一对应关系。

初始化结构时有很多变化。以下语句初始化两个结构变量。这里，必须使用标签名。

```
main()
{
    struct st_record
    {
        int  weight;
        float height;
    };
    static struct st_record student1 = {60, 180.75};
    static struct st_record student2 = {53, 170.60};
    ....
    ....
}
```

另一种方法是在函数外部初始化结构变量，如下所示：

```
struct st_record  /* No static word */
{
    int  weight;
    float height;
} student1 = {60, 180.75};
main()
{
    static struct st_record student2 = {53, 170.60};
    ....
    ....
}
```

C 语言不允许在模板内初始化单个结构成员。初始化只能在实际变量的声明中进行。

## 12.5 结构变量的比较

相同结构类型的两个变量可以像普通变量一样进行比较。如果 person1 和 person2 属于同一结构，则以下操作是有效的：

| 操作 | 含义 |
|---|---|
| person1 = person2 | 将 person2 赋给 person1。 |
| person1 == person2 | 比较 person1 和 person2 的所有成员，若相等则返回 1，否则返回 0。 |
| person1 != person2 | 若所有成员都不相等则返回 1，否则返回 0。 |

请注意，并非所有编译器都支持这些操作。例如，Microsoft C 版本不允许对结构变量进行任何逻辑操作。在这种情况下，可以使用逻辑运算符比较单个成员。

### 示例 12.2

编写一个程序来说明结构变量的比较。

图 12.2 所示的程序说明了如何将一个结构变量复制到同一类型的另一个结构变量中。它还执行逐成员比较以判断两个结构变量是否相同。

## 12.6 结构数组

我们使用结构来描述多个相关变量的格式。例如，在分析班级学生成绩时，我们可以使用模板来描述学生姓名和各科成绩，然后将所有学生声明为结构变量。在这种情况下，我们可以声明一个结构数组，数组的每个元素代表一个结构变量。例如，

```
struct class student[100];
```

定义了一个名为 student 的数组，由 100 个元素组成。每个元素被定义为 struct class 类型。考虑以下声明：

```
struct marks
{
    int subject1;
    int subject2;
    int subject3;
};
main()
{
    static struct marks student[3] = {
        {45,68,81}, {75,53,69}, {57,36,71}};
```

## 结构和联合 12.9

这声明 student 为包含三个元素 student[0]、student[1] 和 student[2] 的数组，并按如下方式初始化其成员：

```
student[0].subject1 = 45;
student[0].subject2 = 68;
.....
student[2].subject3 = 71;
```

```
Program
/* COMPARISON OF STRUCTURE VARIABLES */
struct class {
int number;
char name[20];
float marks;
};
main()
{
int x;
static struct class student1 = {111,"RAO",72.50};
static struct class student2 = {222,"Reddy",67.00};
struct class student3;
student3 = student2;
x = ((student3.number == student2.number) && (student3.marks == student2.marks)) ? 1 : 0;
if(x == 1)
{
printf("\nstudent2 and student3 are same\n");
printf("%d %s %f\n", student3.number, student3.name, student3.marks);
}
else
{
printf("\nstudent2 and student3 are different\n");
}
Output
student2 and student3 are same
222 Reddy 67.000000
```

![](img/65953ea584e494f3d396b2252cb5ea53_339_0.png)

请注意，数组的声明方式与任何其他数组一样。因为 student 是一个数组，所以我们使用通常的数组访问方法来访问各个元素，然后使用成员运算符来访问各个成员。

结构数组在内存中存储的方式与多维数组相同。数组 student 实际看起来如 图 12.3 所示。

### 示例 12.3

对于上面讨论的 **student** 数组，编写一个程序来计算按科目和按学生的总和，并将其作为结构的一部分存储。

|  |  |
|---|---|
| student[0].subject1 | 45 |
| . subject2 | 68 |
| . subject3 | 81 |
| student[1].subject1 | 75 |
| . subject2 | 53 |
| . subject3 | 69 |
| student[2].subject1 | 57 |
| . subject2 | 36 |
| . subject3 | 71 |

**图 12.3** *内存中 student 数组*

程序显示在图 12.4 中。我们声明了一个四成员结构，第四个用于保存学生总和。我们还声明了一个数组 total 来保存科目总和和总总和。总总和由 **total.total** 给出。请注意，成员名可以是任何有效的 C 名称，并且可以与已有的结构变量名相同。链接名 **total.total** 表示结构变量 total 的 **total** 成员。

```
Program
/*------------------------------------------------------------*/
/* ARRAYS OF STRUCTURES */
/*------------------------------------------------------------*/
struct marks
{
 int sub1;
 int sub2;
 int sub3;
 int total;
};
main()
{
 int i;
 static struct marks student[3] = { {45,67,81,0},
 {75,53,69,0},
 {57,36,71,0}};
 static struct marks total;
 for(i = 0; i <= 2; i++)
 {
 student[i].total = student[i].sub1 +
 student[i].sub2 +
 student[i].sub3;
 total.sub1 = total.sub1 + student[i].sub1;
 total.sub2 = total.sub2 + student[i].sub2;
