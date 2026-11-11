

### 12.4.1 结构初始化

与其他数据类型一样，结构变量可以在编译时初始化。

```c
main()
{
        struct
        {
                int weight;
                float height;
        }
        student = {60, 180.75};
        .....
        .....
}
```

这将值 60 赋给 **student.weight**，将 180.75 赋给 **student.height**。成员与其初始化值之间一一对应。

初始化结构时可能存在许多变化。以下语句初始化两个结构变量。这里必须使用标记名。

```c
main()
{
        struct st_record
        {
                int weight;
                float height;
        };
        struct st_record student1 = { 60, 180.75 };
        struct st_record student2 = { 53, 170.60 };
        .....
        .....
}
```

另一种方法是在函数外部初始化结构变量，如下所示：

```c
struct st_record
{
        int weight;
        float height;
}
student1 = {60, 180.75};
main()
{
        struct st_record student2 = {53, 170.60};
        .....
        .....
}
```

**程序**

```c
struct class
{
    int number;
    char name[20];
    float marks;
};

main()
{
    int x;
    struct class student1 = {111,"Rao",72.50};
    struct class student2 = {222,"Reddy", 67.00};
    struct class student3;

    student3 = student2;

    x = ((student3.number == student2.number) &&
         (student3.marks == student2.marks)) ? 1 : 0;

    if(x == 1)
    {
        printf("\nstudent2 and student3 are same\n\n");
        printf("%d %s %f\n", student3.number,
               student3.name,
               student3.marks);
    }
    else
        printf("\nstudent2 and student3 are different\n\n");

}
```

**输出**

```text
student2 and student3 are same

222 Reddy 67.000000
```

**图 12.2** 比较和复制结构变量

### 12.5.1 字边界与空闲字节

计算机使用“字边界”的概念存储结构。字边界的大小取决于机器。在字边界为两字节的计算机中，结构的成员按左对齐存储在字边界上，如下所示。字符数据占一个字节，整数占两个字节。它们之间的一个字节未被占用。这个未占用的字节称为*空闲字节*。

![](img/11b034a94fc590add0a7808250a38792_449_0.png)

当我们声明结构变量时，每个变量都可能包含空闲字节，而这些空闲字节中存储的值是未定义的。因此，即使两个变量的成员相等，它们的结构也不一定比较为相等。所以，C 不允许比较结构。但是，我们可以设计自己的函数，比较各个成员来决定结构是否相等。

## 12.6 对单个成员的操作

**LO 12.3**

如前所述，单个成员使用成员运算符（即*点*）来标识。带有*点运算符*的成员及其结构变量可以像任何其他变量名一样对待，因此可以使用表达式和运算符进行操作。考虑图 12.2 中的程序。我们可以执行以下操作：

```c
if (student1.number == 111)
    student1.marks += 10.00;
float sum = student1.marks + student2.marks;
student2.marks *= 0.5;
```

我们还可以对数值类型的成员应用递增和递减运算符。例如，以下语句是有效的：

```c
student1.number++;
++student1.number;
```

*成员*运算符的优先级高于所有*算术*和*关系*运算符，因此不需要括号。

### 访问成员的三种方式

我们已经使用点运算符来访问结构变量的成员。事实上，还有另外两种方式。考虑以下结构：

```c
typedef struct
{
    int x;
    int y;
} VECTOR;
VECTOR v, *ptr;
ptr = &v;
```

标识符 ptr 称为指针，它被赋予了结构变量 v 的地址。现在，可以通过以下三种方式访问成员：

- 使用点表示法：`v.x`
- 使用间接表示法：`(*ptr).x`
- 使用选择表示法：`ptr->x`

第二种和第三种方法将在第 13 章中讨论。

## 12.7 结构数组

**LO 12.4**

我们使用结构来描述若干相关变量的格式。例如，在分析一个班级学生取得的分数时，我们可以使用一个模板来描述学生姓名和各科所得分数，然后将所有学生声明为结构变量。在这种情况下，我们可以声明一个结构数组，数组的每个元素表示一个结构变量。例如：

```c
struct class student[100];
```

定义了一个名为 **student** 的数组，它由 100 个元素组成。每个元素定义为 **struct class** 类型。考虑以下声明：

```c
struct marks
{
    int   subject1;
    int   subject2;
    int   subject3;
};
main()
{
    struct marks student[3] =
        {{45,67,81}, {75,53,69}, {57,36,71}};
}
```

这将 **student** 声明为包含三个元素 **student[0]**、**student[1]** 和 **student[2]** 的数组，并按如下方式初始化其成员：

```c
student[0].subject1 = 45;
student[0].subject2 = 67;
....
....
student[2].subject3 = 71;
```

注意，该数组的声明方式与任何其他数组一样。由于 **student** 是一个数组，我们使用通常的数组访问方法来访问各个元素，然后使用成员运算符访问成员。请记住，**student** 数组的每个元素都是一个具有三个成员的结构变量。

结构数组在内存中的存储方式与多维数组相同。数组 **student** 实际上如图 12.3 所示。

### 例题 12.4

对于上面讨论的 **student** 数组，编写一个程序来计算各科总分和学生总分，并将它们作为结构的一部分存储。

该程序如图 12.4 所示。我们声明了一个四成员结构，第四个成员用于保存学生总分。我们还声明了一个数组 total 来保存各科总分和总计。总计由 **total.total** 给出。注意，成员名可以是任何有效的 C 名称，并且可以与现有的结构变量名相同。链接名 **total.total** 表示结构变量 **total** 的 **total** 成员。

| 成员 | 值 |
| --- | --- |
| student[0].subject1 | 45 |
| .subject2 | 67 |
| .subject3 | 81 |
| student[1].subject1 | 75 |
| .subject2 | 53 |
| .subject3 | 69 |
| student[2].subject1 | 57 |
| .subject2 | 36 |
| .subject3 | 71 |

**图 12.3** *内存中的数组 student*

**程序**

```c
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
    struct marks student[3] = {{45,67,81,0},
                               {75,53,69,0},
                               {57,36,71,0}};

    struct marks total;
    for(i = 0; i <= 2; i++)
    {
        student[i].total = student[i].sub1 +
                           student[i].sub2 +
                           student[i].sub3;
        total.sub1 = total.sub1 + student[i].sub1;
        total.sub2 = total.sub2 + student[i].sub2;
        total.sub3 = total.sub3 + student[i].sub3;
        total.total = total.total + student[i].total;
    }
    printf(" STUDENT     TOTAL\n\n");
    for(i = 0; i <= 2; i++)
        printf("Student[%d]      %d\n", i+1,student[i].total);

    printf("\n SUBJECT      TOTAL\n\n");
    printf("%s           %d\n%s      %d\n",
           "Subject 1  ", total.sub1,
           "Subject 2  ", total.sub2,
           "Subject 3  ", total.sub3);

    printf("\nGrand Total = %d\n", total.total);
}
```

**输出**

```text
STUDENT          TOTAL
Student[1]       193
Student[2]       197

Student[3]       164

SUBJECT          TOTAL
Subject 1        177
Subject 2        156
Subject 3        221

Grand Total   = 554
```

**图 12.4** *结构数组：带下标结构变量的示例*

## 12.8 结构中的数组

**LO 12.4**

C 允许使用数组作为结构成员。我们已经在结构中使用过字符数组。类似地，我们可以使用 **int** 或 **float** 类型的一维或多维数组。例如，以下结构声明是有效的：

```c
struct marks
{
    int number;
    float subject[3];
} student[2];
```

这里，成员 **subject** 包含三个元素 **subject[0]**、**subject[1]** 和 **subject[2]**。可以使用适当的下标访问这些元素。例如，名称 `student[1].subject[2]` 将指第二个学生在第三个科目中获得的分数。

