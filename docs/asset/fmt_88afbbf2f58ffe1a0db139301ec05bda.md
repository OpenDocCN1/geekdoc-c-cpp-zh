
| 示例 12.1 | 定义一个结构 `struct person`，它将包含姓名、入职日期和工资。使用该结构，编写一个程序从键盘读取一个人的这些信息并在屏幕上打印相同的内容。 |

结构定义及程序如图 12.1 所示。`scanf` 和 `printf` 函数说明了如何使用成员运算符 `.` 将结构成员链接到结构变量。带有名称和点的变量可以像普通变量一样被使用。

```c
Program
struct personal {
    char name[20];
    int day;
    char month[10];
    int year;
    float salary;
};
main() {
    struct personal person;
    printf("Input Values\n");
    scanf("%s %d %s %f", &person.name, &person.day);
(续)
```

```c
person.month,
&person.year,
&person.salary);
printf("%s %d %s %d\n",
person.name,
person.day,
person.month,
person.year,
person.salary);
```

输出

Input Values

M.L.Goel 10 January 1945 4500

M.L.Goel 10 January 1945 4500.

图 12.1 定义和访问结构成员

## 结构初始化

与任何其他数据类型一样，结构变量可以在编译时初始化。

```c
main()
    struct {
        int weight;
        float height;
    }
    student = {60, 180.75};
    ....
```

这将 60 赋值给 `student.weight`，将 180.75 赋值给 `student.height`。成员与其初始化值之间存在一一对应的关系。

初始化结构时可以有很多变化。以下初始化了一个结构。

```c
main()
    struct {
        int weight;
        float height;
    }
    student = {60, 180.75};
    ....
```

这将 60 赋值给 `student.weight`，将 180.75 赋值给 `student.height`。成员与其初始化值之间存在一一对应的关系。

# 计算机概念与C语言编程

另一种方法是初始化结构如下：

```c
struct {
    int weight;
    float height;
}
student = {60, 180.75};
```

这将 60 赋值给 `student.weight`，将 180.75 赋值给 `student.height`。成员与其初始化值之间存在一一对应的关系。

# 边界边界与空字节

| | 0 | 1 | 2 | 3 |

|---|---|---|---|---|

| | | | int |

- - 计算机使用“字边界”的概念存储数据。在具有两个字节字边界的计算机中，结构的每个元素都左对齐设置在字边界上，如下所示。字符数据占用一个字节，整数占用两个字节。它们之间留了一个未占据的字节。这个未占据的字节被称为空字节。

当我们声明变量时，每个变量都可能包含空字节，且空字节中存储的值是未定义的。

## 12.7 个体成员的操作

如前所述，个体成员是通过成员运算符——即*点*（dot）——来标识的。在结构变量上使用*点*运算符的成员可以像任何其他变量一样被处理，因此可以使用表达式和运算符对其进行操作。考虑图 12.2 中的程序。我们可以执行以下操作：

```c
if student1.number == 111
    student1.marks += 10.00;
float sum = student1.marks + student2.marks;
student2.marks *= 0.5;
```

我们也可以对数值类型的成员应用递增和递减运算符。例如，以下语句是有效的：

```c
student1.number ++;
++ student1.number;
```

*成员运算符*的优先级高于任何*算术和关系运算符*，不需要括号。

## 访问成员的三种方法

我们使用了点运算符来访问结构变量的成员。事实上，还有另外两种方法。考虑以下结构：

```c
typedef struct {
    int x;
    int y;
} VECTOR;
VECTOR v, *ptr;
ptr = &v;
```

标识符 `ptr` 被称为指针，它被分配了结构变量 `v` 的地址。现在，可以通过三种方式访问成员：

- 使用点法

- 使用间接引用法（induction notation）

- 使用选择法（selection notation）

第二和第三方法将在第 12 章中讨论。

## 12.8 结构数组

我们使用结构来描述一组相关变量的格式。例如，在分析一个班级学生的成绩时，我们使用模板来描述学生姓名和各科的成绩，并将所有数组声明为结构变量。在这种情况下，我们可以声明一个结构数组，每个元素代表一个结构变量。例如：

```c
struct class student[100];
```

这定义了一个名为 `student` 的数组，它包含 100 个元素。每个元素被定义为 `struct class` 类型。考虑以下声明：

```c
struct marks
{
    int subject1;
    int subject2;
    int subject3;
};
main()
{
    struct marks student[3] =
    {{45,68,81}, {75,53,69}, {57,36,71}};
}
```

这声明该结构为包含三个元素的数组 `student[0]`、`student[1]` 和 `student[2]`，并如下初始化它们的成员：

```c
student[0].subject1 = 45;
student[0].subject2 = 65;
student[2].subject3 = 71;
```

注意，数组的声明方式与任何其他数组相同。由于 `student` 是一个数组，我们使用数组访问方法来访问单个元素，并使用成员运算符访问成员。`student` 数组的每个元素都是具有三个成员的结构变量。结构数组在内存中的存储方式与多维数组相同。数组的实际结构如图 12.3 所示。

| student[0].subject1 | 45 |

| .subject2 | 68 |

| .subject3 | 81 |

| student[1].subject1 | 75 |

| .subject2 | 53 |

| .subject3 | 69 |

| student[2].subject1 | 57 |

| .subject2 | 36 |

| .subject3 | 71 |

**图. 12.3** 内存中的学生

**示例 12.3** 对于上述数组，编写一个程序计算每个学生的总分以及各科的总分，并将它们存储为结构的一部分。

程序如图 12.4 所示。我们声明了一个具有四个成员的结构，其中四个成员用于存储学生的总分。我们还声明了一个数组 `total` 来存储学生的总分和总总分。总分通过 `total.total` 给出。注意，成员名称可以是任何有效的 C 标识符，并与现有变量名相同。链接名称 `total.total` 代表结构变量 `total` 的总成员。

```c
Program struct marks
{
    int sub1;
    int sub2;
    int sub3;
    int total;
}
main() {
    int i;
    struct marks student[3] = {{45,68,81}, {75,53,69}, {57,36,71}};
    struct marks total;
    for(i = 0; i < 3; i++) {
        student[i].total = student[i].sub1 + student[i].sub2 + student[i].sub3;
        total.sub1 = total.sub1 + student[i].sub1;
        total.sub2 = total.sub2 + student[i].sub2;
        total.sub3 = total.sub3 + student[i].sub3;
        total.total = total.total + student[i].total;
    }
    printf("STUDENT\t\n");
    for(i = 0; i < 3; i++) {
        printf("%d\t%d\n", i+1, student[i].total);
    }
    printf("\nSUBJECT\t\n");
    for(i = 0; i < 3; i++) {
        printf("%s\t%d\n", "Subject 1", total.sub1);
        printf("%s\t%d\n", "Subject 2", total.sub2);
        printf("%s\t%d\n", "Subject 3", total.sub3);
    }
    printf("\nGrand Total = %d\n", total.total);
}
```

Output

STUDENT	TOTAL

Student[1]	93

Student[2]	97

Student[3]	164

SUBJECT	TOTAL

Subject 1	177

Subject 2	156

Subject 3	221

Grand Total	554

**图. 12.4** 结构数组：下标变量示意

## 12.9 结构中的数组

C 允许将数组作为结构成员。我们已经使用过结构中的字符数组。同样，可以使用一维或多维的 `int` 或 `float` 数组。例如，以下结构声明是有效的：

```c
struct marks
{
    int number;
    float subject[3];
} student[2];
```

在这里，成员包含三个元素 `subject[0]`, `subject[1]` 和 `subject[2]`。可以使用适当的下标访问这些元素。例如，`student[1].subject[2]` 代表学生的第三科成绩。

**示例 12.4** 使用数组成员重写 12.3 的程序以表示三门科目。修改后的程序如图 12.5 所示。代码中使用了科目的数组名称。

```c
Program main()
{
    struct marks
    {
        int sub[3];
        int total;
    };
    struct marks student[3] = {{45,67,81}, {75,53,69}, {57,36,71}};
    struct marks total;
    for(i = 0; i < 3; i++) {
        for(j = 0; j < 3; j++) {
            student[i].total += student[i].sub[j];
        }
        total.total += student[i].total;
    }

    printf("\nSTUDENT TOTAL:\t\n");
    for(i = 0; i < 3; i++) {
        printf("%d\t%d\n", i+1, student[i].total);
    }

    printf("\nSUBJECT TOTAL:\t\n");
    for(j = 0; j < 3; j++) {
        printf("Subject-%d \t%d\n", j+1, total.sub[j]);
    }

    printf("\nGrand Total %d\n", total.total);
}
```

（续）

Output

| STUDENT | TOTAL |

| --- | --- |

| Student[1] | 193 |

| Student[2] | 197 |

| Student[3] | 164 |

| SUBJECT | TOTAL |

| Student-1 | 177 |

| Student-2 | 156 |

| Student-3 | 221 |

| Grand Total | 554 |

**图. 12.5** 结构中下标数组的使用

## 12.10 嵌套结构

结构中的结构意味着结构的嵌套。C 允许结构嵌套。让我们考虑以下用于存储员工工资信息的结构：

```c
struct salary {
    char name;
    char department;
    int basic_pay;
    int dearness_allowance;
    int house_rent_allowance;
    int city_allowance;
}
employee;
```

该结构定义了姓名、部门、基本工资和三种津贴。我们可以将所有与津贴相关的项分组，并在如下子结构下声明它们：

`salary` 结构包含一个名为 `allowance` 的成员，它本身是一个带有三个成员的结构。内部结构名为 `dearness`、`house_rent` 和 `city` 的成员可以引用为：

`employee.allowance.dearness`

`employee.allowance.house_rent`

`employee.allowance.city`
