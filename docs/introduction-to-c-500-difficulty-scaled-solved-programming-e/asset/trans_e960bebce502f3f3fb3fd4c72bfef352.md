

# 13 • 结构与联合体 387

```cpp
return &v[i]; /* 如果找到了代码，函数将终止并返回该结构的地址。 */
}
```

```cpp
return nullptr; /* 如果代码执行到这一点，意味着
未找到该产品，函数返回 nullptr。 */
```

**C.13.6** 定义结构 `Coord`，包含一个点的坐标（例如 x 和 y）。定义结构类型 `Rectangle`，其包含两个 `Coord` 类型的结构（例如 `Point_A` 和 `Point_B`）。编写一个函数，将矩形的两个端点作为参数传入。每个端点都应该是一个 `Coord` 类型的结构。该函数应计算并返回矩形的面积。编写一个程序，使用该 `Rectangle` 类型读取矩形对角线的坐标，并使用函数显示其面积。

```cpp
#include <iostream>
using std::cout;
using std::cin;
```

```cpp
struct Coord
{
    double x;
    double y;
};
```

```cpp
struct Rectangle
{
    Coord point_A; // 第一个对角点。
    Coord point_B; // 第二个对角点。
};
```

```cpp
double rect_area(const Coord *c1, const Coord *c2);
```

```cpp
int main()
{
    Rectangle rect;

    cout << "Enter the x and y coords of the first point: ";
    cin >> rect.point_A.x >> rect.point_A.y;

    cout << "Enter the x and y coords of the second point: ";
    cin >> rect.point_B.x >> rect.point_B.y;

    cout << "Area:" << rect_area(&rect.point_A, &rect.point_B) << '\n';
    return 0;
}
```

```cpp
double rect_area(const Coord *c1, const Coord *c2)
{
    double base, height;

    if(c1->x > c2->x)
        base = c1->x - c2->x;
    else
        base = c2->x - c1->x;

```cpp
if(c1->y > c2->y)
    height = c1->y - c2->y;
else
    height = c2->y - c1->y;

  return base*height; // 返回面积。
}
```

C.13.7 对于复数，我们有 $z = a + bj$，其中 $j$ 是虚数单位，$a$ 是实部，$b$ 是虚部。定义结构类型 `Complex`，成员为浮点数 `re` 和 `im`，它们分别代表复数的实部和虚部。编写一个函数，参数为两个 `Complex` 类型的结构和一个字符，该字符表示数学运算的符号。该函数应执行数学运算并将结果作为 `Complex` 类型的结构返回。编写一个程序，使用结构 `Complex` 读取两个复数和一个数学符号（+, -, /），并使用函数显示数学运算的结果。如果 $z_1 = a + bj$ 且 $z_2 = c + dj$，我们有：

```
z = z1 + z2 = (a+c)+(b+d)j

z = z1 - z2 = (a-c)+(b-d)j

z = z1 × z2 = (ac-bd)+(ad+bc)j

z = \frac{z1}{z2} = (\frac{ac+bd}{c^2+d^2} + \frac{ad-bc}{c^2+d^2})j
```

```cpp
#include <iostream>
using std::cout;
using std::cin;
```

```cpp
struct Complex
{
    double re; // 复数的实部。
    double im; // 复数的虚部。
};
```

```cpp
Complex operation(Complex a1, Complex a2, char sign);
```

```cpp
int main()
{
    char sign;
    Complex z1, z2, z;
```

```cpp
cout << "Enter real and imaginary part of the first complex number: ";
cin >> z1.re >> z1.im;
cout << std::showpos << "z1 = " << z1.re << ' ' << z1.im << 'j' << '\n';
```

```cpp
cout << "Enter real and imaginary part of the second complex number: ";
cin >> z2.re >> z2.im;
cout << "z2 = " << z2.re << ' ' << z2.im << 'j' << '\n';
```

```cpp
cout << "Enter sign (+, -, *, /);";
cin >> sign;
if(sign == '+' || sign == '-' || sign == '*' || sign == '/')
{
    if(sign == '/' && z2.im == 0)
    {
        cout << "Division by zero is not allowed\n";
    }
    else
    {
        z = operation(z1, z2, sign);
        cout << "z = " << z1 << " sign " << "z2 = " << z.re << " << " << z.im << "\n";
    }
}
else
{
    cout << "Wrong sign\n";
    return 0;
}

Complex operation(Complex a1, Complex a2, char sign)
{
    double div;
    Complex a;
    switch(sign)
{
case '+':
    a.re = a1.re + a2.re;
    a.im = a1.im + a2.im;
    break;
case '-':
    a.re = a1.re - a2.re;
    a.im = a1.im - a2.im;
    break;
case '*':
    a.re = a1.re * a2.re - a1.im * a2.im;
    a.im = a1.re * a2.im + a1.im * a2.re;
    break;
case '/':
    div = (a2.re * a2.re + a2.im * a2.im);
    a.re = (a1.re * a2.re + a1.im * a2.im) / div;
    a.im = (a1.im * a2.re - a1.re * a2.im) / div;
    break;
}
    return a;
}
```

**注释：** 我们使用了在第 3 章讨论过的 `showpos` 操纵符，以便在正值前加上 +。我之所以没有向 `operation()` 传递结构的地址以避免创建拷贝，是为了向你展示一个带参数的函数示例。

**C.13.8** 定义结构类型，成员为：`name`、`code` 和 `grade`。编写一个程序使用该类型读取 100 名学生的数据并将其存储在结构数组中。如果用户在 `grade` 时输入 -1，则数据插入应终止。编写一个函数按升序排序结构，并编写另一个函数显示成绩高于所有学生平均分的学生数据。程序应调用这两个函数。

```cpp
#include <iostream>
#include <string>
using std::cout;
using std::cin;

const int SIZE = 100;

struct Student
{
    std::string name;
    int code;
    float grd;
};

void sort_by_grade(Student studs[], int num_studs);
void show_students(const Student studs[], int num_studs, float avg_grd);

int main()
{
    int i;
    float sum_grd;
    Student studs[SIZE];

    sum_grd = 0;
    for(i = 0; i < SIZE; i++) {
        cout << "\nGrade [0-10]: ";
        cin >> studs[i].grd;
        if(studs[i].grd == -1)
            break;

        sum_grd += studs[i].grd;
        cin.get();
    }

    cout << "Name: ";
    getline(cin, studs[i].name);

    cout << "Code: ";
    cin >> studs[i].code;

    if(i == 0)
        return 0;
    sort_by_grade(studs, i); /* 按成绩顺序排序结构。变量 i 指定了学生人数。 */
    show_students(studs, i, sum_grd/i); /* 最后一个参数是所有学生的平均分。 */
    return 0;
}

void sort_by_grade(Student studs[], int num_studs)
{
    int i, j;
    Student s;
    for(i = 0; i < num_studs-1; i++)
    {
        for(j = i+1; j < num_studs; j++)
        {
            /* 在每次迭代中比较成绩。如果较大，则交换结构。 */
            if(studs[i].grd > studs[j].grd)
            {
                s = studs[i];
                studs[i] = studs[j];
                studs[j] = s;
            }
        }
    }
}

void show_students(const Student studs[], int num_studs, float avg_grd)
{
    int i;
    for(i = 0; i < num_studs; i++)
        if(studs[i].grd > avg_grd)
            cout << "\nN:" << studs[i].name << " C:" << studs[i].code << " G:" << studs[i].grd << "\n";
}
```

# 13 • 结构与联合体 391

**C.13.9** 图像处理过程通常将图像旋转 90°。图像可以被视为二维数组，其元素代表图像的像素。例如，原始图像（例如 p[M][N]）的旋转会产生一个新的图像（例如 r[N][M]），所示：

| p_0,0 | p_0,1 | | p_0,N-2 | p_0,N-1 | | p_M-1,0 | p_M-2,0 | ... | p_1,0 | p_0,0 |
| p_1,0 | p_1,1 | | p_1,N-2 | p_1,N-1 | | p_M-1,1 | p_M-2,1 | ... | p_1,1 | p_0,1 |
| p = | | | | | r = | | | | |
| | | | | | | | | | |
| | | | | | | | | | |
| p_M-2,0 | p_M-2,1 | | p_M-2,N-2 | p_M-2,N-1 | | p_M-1,N-2 | p_M-1,N-1 | ... | p_1,N-2 | p_0,N-2 |
| p_M-1,0 | p_M-1,1 | | p_M-1,N-2 | p_M-1,N-1 | | | | | | |

特别地，原始图像的第一行变成新图像的最后一列，第二行变成倒数第二列，直到第一行变成第一列。例如，图像：

| 11 | 6 | 1 |
| 12 | 7 | 2 |
| 13 | 8 | 3 |
| p = 11 12 13 | 被转换为: r = |
| 14 | 9 | 4 |
| 15 | 10 | 5 |

每个像素的颜色遵循 RGB 色彩，通过混合红、绿、蓝三色来重现一系列颜色。颜色用 RGB 三元组 (r, g, b) 表示，其中每个分量值从 0 到 255 变化。

