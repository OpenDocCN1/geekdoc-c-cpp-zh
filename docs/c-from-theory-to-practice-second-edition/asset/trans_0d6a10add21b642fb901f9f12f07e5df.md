
显示成绩高于所有学生平均成绩的学生的数据。程序应调用这两个函数。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define SIZE 100

struct student
{
    char name[50];
    int code;
    float grd;
};

void sort_by_grade(struct student studs[], int num_studs);
void show_students(struct student studs[], int num_studs, float avg_grd);
int read_text(char str[], int size, int flag);

int main(void)
{
    int i;
    float sum_grd;
    struct student studs[SIZE];

    sum_grd = 0;
    for(i = 0; i < SIZE; i++)
    {
        printf("\nGrade [0-10]: ");
        scanf("%f", &studs[i].grd);
        if(studs[i].grd == -1)
            break;

        sum_grd += studs[i].grd;
        getchar();

        printf("Name: ");
        read_text(studs[i].name, sizeof(studs[i].name), 1);
        printf("Code: ");
        scanf("%d", &studs[i].code);
    }
    if(i == 0)
        return 0;
    sort_by_grade(studs, i); /* Sort the structures in grade ascending order. The variable i specifies the number of students. */
    show_students(studs, i, sum_grd/i); /* The last argument is the average grade of all students. */
    return 0;
}

void sort_by_grade(struct student studs[], int num_studs)
{
int i, j;
struct student temp;
for(i = 0; i < num_studs-1; i++)
{
    /* In each iteration, the grd member is compared with the others. If it is less, the structures are swapped. */
    for(j = i+1; j < num_studs; j++)
    {
        if(studs[i].grd > studs[j].grd)
        {
            temp = studs[i];
            studs[i] = studs[j];
            studs[j] = temp;
        }
    }
}
}

void show_students(struct student studs[], int num_studs, float avg_grd)
{
    int i;
    for(i = 0; i < num_studs; i++)
        if(studs[i].grd > avg_grd)
            printf("\n%s C: %d G: %f\n", studs[i].name, studs[i].code, studs[i].grd);
}
```

## C.13.10

图像编辑程序通常需要将图像旋转 90°。图像可以被视为一个二维数组，其元素代表图像的像素。例如，将原始图像（例如 p[M][N]）向右旋转会产生一个新图像（例如 r[M][N]），如下所示：

![](img/b8da5dcf9ba7f1fad5213c453d095246_455_0.png)

具体来说，原始图像的第一行变为新图像的最后一列，第二行变为倒数第二列，直到最后一行，它变为第一列。例如，图像：

p = ⎡1 2 3 4 5⎤
    ⎢6 7 8 9 10⎥
    ⎣11 12 13 14 15⎦ is transformed to r = ⎡11 6 1⎤
                                           ⎢12 7 2⎥
                                           ⎢13 8 3⎥
                                           ⎢14 9 4⎥
                                           ⎣15 10 5⎦

每个像素的颜色遵循 RGB 颜色模型，其中红色、绿色和蓝色混合在一起以再现广泛的颜色。颜色表示为 RGB 三元组 (r, g, b)，其中每个分量值在 0 到 255 之间变化。

定义结构类型 pixel，包含三个名为 red、green 和 blue 的整数成员。编写一个程序，创建一个二维图像（例如 3×5），其元素为 pixel 类型的结构。用 [0, 255] 范围内的随机值初始化每个结构的成员。然后，程序应显示原始图像，将图像向右旋转 90°，并显示旋转后的图像（例如 5×3）。

提示：使用第二个数组来存储旋转后的图像。

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define ROWS 3
#define COLS 5

struct pixel /* RGB format (Red-Green-Blue). */
{
    unsigned char red; /* Value in [0, 255]. */
    unsigned char green;
    unsigned char blue;
};

void rotate_right_90(struct pixel img[][COLS], struct pixel tmp[][ROWS]);

int main(void)
{
    int i, j;
    struct pixel img[ROWS][COLS], tmp[COLS][ROWS];

    srand(time(NULL));
    /* Create random colors. */
    for(i = 0; i < ROWS; i++)
    {
        for(j = 0; j < COLS; j++)
        {
            img[i][j].red = rand()%256;
            img[i][j].green = rand()%256;
            img[i][j].blue = rand()%256;
        }
    }
    printf("*** Original Image ***\n\n");
for(i = 0; i < ROWS; i++)
{
    for(j = 0; j < COLS; j++)
    {
        printf("(%%3d,%%3d,%%3d) ", img[i][j].red, img[i][j].green, img[i][j].blue);
    }
    printf("\n");
}
rotate_right_90(img, tmp);
printf("\n*** Rotated Image ***\n\n");
for(i = 0; i < COLS; i++)
{
    for(j = 0; j < ROWS; j++)
    {
        printf("(%%3d,%%3d,%%3d) ", tmp[i][j].red, tmp[i][j].green, tmp[i][j].blue);
    }
    printf("\n");
}
return 0;
}
void rotate_right_90(struct pixel img[][COLS], struct pixel tmp[][ROWS])
{
    int i, j, k = 0;
    for(i = ROWS-1; i >= 0; i--)
    {
        for(j = 0; j < COLS; j++)
        {
            tmp[j][i] = img[k][j];
        }
        k++;
    }
}
```

## Unions

与结构类似，联合体包含一个或多个成员，这些成员可能具有不同的类型。联合体的属性几乎与结构的属性相同；允许在结构上执行的操作也允许在联合体上执行。它们的区别在于，结构的成员存储在不同的地址，而联合体的成员存储在同一地址。

### Union Declaration

联合体类型的声明类似于结构的声明，只是使用 union 关键字代替 struct。当声明一个联合体变量时，编译器只分配足够存储其最大成员的空间。因此，其成员都存储在同一

内存中，相互重叠。例如，在以下程序中，s 变量分配 8 个字节，因为其最大成员的类型为 double：

```c
#include <stdio.h>

union sample
{
    char ch;
    int i;
    double d;
};

int main(void)
{
    union sample s;
    printf("Size: %lu\n", sizeof(s));
    return 0;
}
```

由于编译器不会为每个联合体成员分配内存，联合体的主要用途是节省内存空间。例如，我们经常在内存有限的嵌入式系统中使用联合体。

![](img/b8da5dcf9ba7f1fad5213c453d095246_458_0.png)

与结构类似，要计算联合体变量的内存大小，请使用 sizeof 运算符。

由于所有联合体成员共享同一内存，因此在声明时只能初始化联合体变量的第一个成员。例如，编译器会允许我们写：

```
union sample s = {'x'};
```

but not: union sample s = {'x', 10, 1.23};

### Access Union Members

联合体的成员与结构的成员访问方式相同。然而，由于它们都存储在同一内存中，只有最后赋值的成员才具有有意义的值。例如，以下程序向 s 成员赋值并显示其他成员：

```c
#include <stdio.h>

union sample
{
    char ch;
    int i;
    double d;
};

int main(void)
{
    union sample s;
s.ch = 'a';
printf("%c %d %f\n", s.ch, s.i, s.d);

s.i = 64;
printf("%c %d %f\n", s.ch, s.i, s.d);

s.d = 12.48;
printf("%c %d %f\n", s.ch, s.i, s.d);
return 0;
}
```

首先，程序输出 a 以及 s.i 和 s.d 成员的无意义值。接下来，值 64 被赋给 i。由于该值存储在公共空间中，s.ch 的值被覆盖。因此，程序显示 64 以及 s.ch 和 s.d 的无意义值。接下来，值 12.48 被赋给 d。s.i 的值被覆盖，程序输出 12.48 以及 s.ch 和 s.i 的无意义值。

![](img/b8da5dcf9ba7f1fad5213c453d095246_459_0.png)

> 当联合体成员被赋值为某个值时，先前存储在最后赋值的成员中的任何值都会被覆盖。

让我们做一个测试。以下程序的输出是什么？

```c
#include <stdio.h>

union test
{
    int a, b, c;
};

int main(void)
{
    union test t;
    t.a = 100;
    t.b = 200;
    t.c = 300;
    printf("%d %d %d\n", t.a, t.b, t.c);
    printf("%d %d %d\n", &t.a, &t.b, &t.c);
    return 0;
}
```

由于成员类型相同且它们都存储在同一内存中，一旦 c 变为 300，其他成员的值也将是 300。因此，第一个 printf() 三次显示 300。第二个 printf() 三次显示公共内存地址。

联合体的典型用途是在数据可以以两种或多种形式存储但永远不会同时存在时节省内存。例如，假设我们想在一个包含 100 个结构的数组中存储男性和女性的偏好。男性的偏好涉及最喜欢的
