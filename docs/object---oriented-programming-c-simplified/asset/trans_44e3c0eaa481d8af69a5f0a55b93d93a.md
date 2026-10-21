

```
time3=time3.sum_time(time1,time2);

time1.show_time("\nTime 1\n");
time2.show_time("\nTime 2\n");

time3.show_time("\nSUM OF TWO DURATION IS\n");

getch();
}
```

# OUTPUT :

Time 1

Hours := 3      Minutes := 35      Seconds := 45

Time 2

Hours := 4      Minutes := 56      Seconds := 45

SUM OF TWO DURATION IS

Hours := 8      Minutes := 32      Seconds := 30

# EXPLANATION :

在程序中我们正在求两个持续时间之和。函数声明 time sum_time (time, time); 告诉编译器 sum_time 是一个函数，它接受两个类类型为 time 的参数（对象）。在此 main 中，我们通过调用函数 input_time 来初始化两个对象 time1 和 time2 的数据成员 hours、minutes 和 secs。在语句

```
time3=time3.sum_time (time1, time2);
```

中，time3 调用函数 sum_time 并将 time1 和 time2 作为参数传递。在函数 sum_time 内部，我们首先计算秒、分钟和小时变量 s、m 和 h，并从中实际为 temp 对象的成员变量赋值。在此 temp 对象的末尾被返回并赋给 main 中的 time3。

## 6.7 对象数组

类似于任何基本数据类型的数组，我们可以创建任何类的对象数组。这在我们想要处理例如员工的薪水、人员账户的处理、学生记录等时非常方便。在所有这些情况下，对象数组使我们的工作更轻松并使处理更快。对于一个类 say demo，它包含两个 int 类型的成员变量 dx 和 dy，按如下方式创建对象数组：

# demo arr[5];

这创建了一个大小为 5 的对象数组。第一个对象由 arr[0] 引用，第二个由 arr[1] 引用，以此类推。对象 arr[0] 的数据成员可以作为 arr[0].dx 和 arr[0].dy 访问。正如我们只在该 demo 类内部有两个 int 类型的成员变量 dx 和 dy，任何该 demo 类对象的大小将为 8 字节。因此，数组的大小为 8*5=40。每个对象将在内存中以 8 字节的距离放置，如图所示：

![](img/ad5299318df8d4d7c6df5eaa86590ea3_268_0.png)

图 6.4. 对象数组的实现。

```
/*PROG 6.34 DEMO OF ARRAY OF OBJECTS */

#include <iostream.h>
#include <conio.h>
#define S 5

class Point
{
    int px;
    int py;
    public :
    void input(int x,int y)
    {
    px=x;
    py=y;
    }
    void show()
    {
    cout << "(" << px << "," << py << ")" << endl;
    }
};

void main()
{
    Point ptarr[S];
    int i;
    clrscr();
    for(i=0;i<S;i++)
    ptarr[i].input(234+i*2,254+i*3);
    cout << "Points are \n";
    for(i=0;i<S;i++)
    ptarr[i].show();
```

```
getch();
}
```

OUTPUT :
Points are
(234,254)
(236,257)
(238,260)
(240,263)
(242,266)

EXPLANATION : 类 Point 存储一个点的 x 和 y 坐标。在 main 内部我们创建了一个大小为 5 的类类型 Point 的数组 ptarr。这类似于创建 5 个具有不同名称的对象。数组 ptarr 是类 Point 类型的对象数组。ptarr [0] 表示第一个对象，ptarr[1] 表示第二个对象，以此类推。在 main 中我们使用 for 循环为所有对象调用 input 函数并传递任意点给函数。每个对象将具有不同的点作为数据成员，因为每个对象的数据成员是唯一的。稍后我们使用 show 和 for 循环显示每个点的点。

```
/* PROG 6.35 DISPLAYING EMP NAME AND SALARY USING ARRAY OF OBJECT */
#include <iostream.h>
#include <conio.h>
#define S 4

class Emp
{
 char ename[15];
 float sal;

public :
 void input();
 void show ();
};

void Emp ::input ()
{
 cout << "Enter the employee name \n";
 cin.getline(ename,15);
 cout << "Enter salary\n";
 cin >> sal;
 cin.ignore( );
}
```

```
void Emp ::show()
{
    cout << ename << "\t" << sal << endl;
}
void main()
{
    Emp earr[S];
    int i;
    clrscr();
    for(i=0;i<S;i++)
        earr[i].input();
    cout << "Employee Details\n";
    cout << "\n NAME \t SALARY\n";
    for(i=0;i<S;i++)
        earr[i].show();
    getch();
}
```

# OUTPUT :

Enter the employee name
hari
Enter salary
26000
Enter the employee name
Deshmukh
Enter salary
20000
Enter the employee name
Vivek
Enter salary
21000
Enter the employee name
Malvika
Enter salary
25000
Employee Details

| NAME     | SALARY |
|----------|--------|
| Hari     | 26000  |
| Deshmukh | 20000  |
| Vivek    | 21000  |
| Malvika  | 25000  |

EXPLANATION : 类 Emp 存储有关员工的信息。它只有两个数据成员 ename 和 sal。通过函数 input 我们直接在数据成员 ename 和 sal 中输入员工姓名和薪水。cin.ignore( ) 的使用会刷新输入缓冲区。这相当于 C 中的 fflush(stdin)。在 main 中我们创建了一个名为 earr 的 Emp 对象数组，大小为 S。通过 for 循环和 input 函数我们为数组 earr 的所有 4 个对象元素获取数据，然后使用 for 和 show 显示它们。

```
/* PROG 6.36 STUDENTS MERIT LIST */

#include <iostream.h>
#include <conio.h>
#define S 4

class student
{
    char sname[15];
    int m1, m2, m3;
    float per;

public :

    void input();
    void show();
    float getper();
};

void student ::input()
{
    cout<<"ENTER THE NAME OF STUDENT"<<endl;
    cin.getline(sname,15);
    cout<<"ENTER THE MARKS IN THREE SUBJECTS"<<endl;
    cin>>m1>>m2>>m3;
    per=(m1+m2+m3)/3.0;
    cin.ignore();
}
void student ::show()
{
    cout<<sname<<"\t"<<per<<endl;
}

float student ::getper()
{
```

```
return per;
}

void main()
{
    student sarr[S],temp;
    int i,j;
    clrscr();
    for(i=0;i<S;i++)
        sarr[i].input();
    for(i=0;i<S;i++)
        for(j=i+1;j<S;j++)
            if(sarr[i].getper() < sarr[j].getper())
            {
                temp=sarr[i];
                sarr[i]=sarr[j];
                sarr[j]=temp;
            }
    cout<<"STUDENT MERIT LIST\n";
    cout<<"\nNAME \t Per(%)\n";
    for(i=0;i<S;i++)
        sarr[i].show();
    getch();
}
```

# OUTPUT :

ENTER THE NAME OF STUDENT
Kashap
ENTER THE MARKS IN THREE SUBJECTS
70
78
90
ENTER THE NAME OF STUDENT
Maskara
ENTER THE MARKS IN THREE SUBJECTS
80
67
78
ENTER THE NAME OF STUDENT
Vishnukant
ENTER THE MARKS IN THREE SUBJECTS

```
70
80
76
ENTER THE NAME OF STUDENT
Manish
ENTER THE MARKS IN THREE SUBJECTS
64
79
90

STUDENT MERIT LIST

Kashap        79.333336
Maskara       77.666664
Vishnukant    75.333336
Manish        75
```

**EXPLANATION** : 类 student 有 5 个数据成员：`sname`、`m1`、`m2`、`m3` 和 `per`。用于存储三科成绩的为 `m1`、`m2`、`m3`。用于存储百分比的为 `per`，用于姓名的为 `sname`。我们假设所有成绩均以 100 为满分。 （尽管没有通过 if 进行检查）。在函数 input 中，在获取成绩后我们计算百分比并将其存储在 `per` 中。在 `main` 中，我们根据百分比进行排序，因为我们正在生成学生的成绩单。由于 `per` 是 `private`，我们创建了一个 `public` 成员函数 `getper` 来返回 `per`。在 `main` 中排序是基于此函数 getper 进行的。注意在排序过程中整个对象已被交换。为此我们取了一个临时对象 `temp`。稍后我们使用 `show` 和 `for` 循环显示成绩单。

## 6.8 友元函数

友元函数是 C++ 中的一个全新概念。如名称所示，它将是某人的朋友。我们可以使一个函数成为一个类的友元，并允许该友元函数访问该类的私有和公共数据成员。**友元函数主要用于两个或多个类想要共享一个公共函数时。**我们提出了关于友元函数的若干要点。

- 1. 首先 **friend** 是关键字。友元函数是通过在函数声明中放置关键字 **friend** 而创建的，但在函数定义中不放置。例外情况是如果在同一位置声明和定义。
- 2. 一个 **friend** 函数是它所声明的类的 **friend**。
- 3. 一个 **friend** 函数不是类的成员函数，不能使用 **dot** 运算符从类的任何对象调用。
- 4. 一个 **friend** 函数可以完全访问它所为之成为 **friend** 的类的 **public**、**private** 和 **protected** 数据成员。

