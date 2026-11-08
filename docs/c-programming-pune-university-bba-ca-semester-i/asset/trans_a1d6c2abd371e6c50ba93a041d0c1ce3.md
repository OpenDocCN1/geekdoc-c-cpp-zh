
**输出**

```text
Enter number of students
2
For student 1
Enter name
Sri
Enter marks
98
For student 2
Enter name
Kiran
Enter marks
96
Name Sri    Marks 98
Name Kiran Marks 96
```

## 77. 编写一个 C 程序，从用户处读取 n 名学生的姓名和成绩，并将它们存储到文件中。如果该文件已存在，则添加这 n 名学生的信息。

```c
#include <stdio.h>
int main()
{
    char name[50];
    int marks, i, num;

    printf("Enter number of students: ");
    scanf("%d", &num);

    FILE *fptr;
    fptr = (fopen("C:\\student.txt", "a"));
    if(fptr == NULL)
    {
        printf("Error!");
        exit(1);
    }

    for(i = 0; i < num; ++i)
    {
        printf("For student%d\nEnter name: ", i+1);
        scanf("%s", name);

        printf("Enter marks: ");
        scanf("%d", &marks);

        fprintf(fptr, "\nName: %s \nMarks=%d \n", name, marks);
    }

    fclose(fptr);
    return 0;
}
```

**输出**

```text
Enter number of students
1
For student 1
Enter name
Shrutikirti
Enter marks
94
Name Sri    Marks 98
Name Kiran  Marks 96
Name Shrutikirti Marks 94
```

## 78. 编写一个 C 程序，使用 fwrite() 将结构体数组的所有成员写入文件。从文件中读取该数组并显示在屏幕上。

```c
#include <stdio.h>
struct student
{
    char name[50];
    int height;
};

int main()
{
    struct student stud1[5], stud2[5];
    FILE *fptr;
    int i;
    fptr = fopen("file.txt", "wb");
    for(i = 0; i < 5; ++i)
    {
        fflush(stdin);
        printf("Enter name: ");
        gets(stud1[i].name);
        printf("Enter height: ");
        scanf("%d", &stud1[i].height);
    }
    fwrite(stud1, sizeof(stud1), 1, fptr);
    fclose(fptr);
    fptr = fopen("file.txt", "rb");
    fread(stud2, sizeof(stud2), 1, fptr);
    for(i = 0; i < 5; ++i)
    {
        printf("Name: %s\nHeight: %d", stud2[i].name, stud2[i].height);
    }
    fclose(fptr);
}
```

**输出**

```text
Enter name
Sri
Enter Height
5.6"
Enter name
Kiran
Enter Height
5.2"
Enter name
Shrutikirti
Enter Height
5.0"
Enter name
Chirag
Enter Height
5.7"
Enter name
Ravi
Enter Height
5.4"
```

## C 编程

### （选择题）

答案以粗体和下划线标出

1) C 语言包含 ________ 个关键字。

- A] **<u>32</u>**
- B] 40
- C] 24
- D] 56

2) 以下哪一项是用于存储类的关键字？

- A] Printf
- B] external
- C] **<u>auto</u>**
- D] scanf

3) 头文件中函数的原型是 _________

- A] Stdio.h
- B] stdLib.h
- C] **<u>conio.h</u>**
- D] io.h

4) 预处理指令用于 _________

- A] 宏展开
- B] 文件包含
- C] 条件编译
- D] **<u>以上全部</u>**

5) 哪个运算符的优先级最低？

- A] ++
- B] %
- C] +
- D] **<u>||</u>**

6) 类型转换运算符是

- A] **<u>(type)</u>**
- B] cast()
- C] //
- D] " "

7) C 中的文件操作函数在哪个头文件中可用？

- A] streams.h
- B] **<u>stdio.h</u>**
- C] stdlib.h
- D] files.h

8) 以下哪一对函数用于单字符 I/O？

- A] **<u>getchar() 和 putchar()</u>**
- B] scanf() 和 printf()
- C] input() 和 output()
- D] 以上都不是

9) 哪个函数用于在输入时读取字符？

- A] getchar()
- B] getch()
- C] getche()
- D] **<u>（B）和（C）两者都是</u>**

10) 该程序的输出是什么？

```c
void main()
{
    int a=b=c=10;
    a=b=c=50;
    printf("\n %d %d %d",a,b,c);
}
```

- A) 50 50 50
- B) **编译时错误**
- C) 10 10 10
- D) 三个垃圾值

11) 哪个格式说明符用于打印 double 类型变量的值

- A) %lf
- B) **%ld**
- C) %lu
- D) %f

12) 以下程序的输出将是什么？

```c
void main ( )
{
    double x=28;
    int r;
    r = x%5;
    printf ("\n r=%d", r);
}
```

- A) r= 3
- B) 运行时错误
- C) **编译时错误**
- D) 以上都不是

13) 以下函数调用是什么意思？

```c
Strcpy(s1 , s2);
```

- A) 将 s1 字符串复制到 s2
- B) 将 s2 字符串复制到 s1
- C) 复制 s1 和 s2
- D) **以上都不是**

14) 以下程序的输出将是什么？

```c
Void main( )
{
    Int x[] = {10,20,30,40,50};
    Printf (" \n %d %d %d %d %d ", x[4], 3[x], x[2], 1[x], x[0]);
}
```

- A) **错误**
- B) 10 20 30 40 50
- C) 50 40 30 20 10
- D) 以上都不是

15) 以下哪一项不是“C”的关键字？

- A) auto
- B) register
- C) int
- D) **function**

16) 输出将是什么？

```c
void main ( )
{
    char a[] = "INFO";
    a++;
    printf("\n %s", a);
}
```

- A] **错误**
- B] INFO
- C] NFO
- D] 以上都不是

17) 以下哪个运算符具有从右到左的结合性？

- A] &&
- B] //
- C] %
- D] **sizeof**

18) 输出将是什么？

```c
void main ( )
{
    int I;
    I = 0x10 + 010 + 10;
    printf("\nx=%x", i);
}
```

- A] x=34
- B] i=34
- C] I = 22
- D] **错误**

19) 显式类型转换称为

- A] 转换
- B] 析取
- C] 分离
- D] **<u>强制类型转换</u>**

20) C 变量不能以什么开头

- A] 数字
- B] 除下划线以外的特殊符号
- C] **以上两者**
- D] 字母

21) 默认情况下，函数返回的值的类型是

- A] int
- B] char
- C] **void**
- D] 以上都不是

22) C 最初是作为什么开发的

- A] **系统编程语言**
- B] 通用语言
- C] 数据处理语言
- D] 以上都不是

23) 在“C”中 sizeof 是什么？

- A] **运算符**
- B] 保留字
- C] （A）和（B）两者都是
- D] 函数

24) C 程序借助什么转换为机器语言

- A] 编辑器
- B] **编译器**
- C] 操作系统
- D] 以上都不是

25) 以下哪个不是“C”中的关键字？

- A] typedef
- B] const
- C] **near**
- D] 以上都不是

26) 以下哪一项不是有效的标识符？

- A] _examveda
- B] **examveda**
- C] exam_veda
- D] examveda1

27) C 语言是在 ________ 开发的？

- A] **美国 AT&T 贝尔实验室，1972 年**
- B] 美国 AT&T 贝尔实验室，1970 年
- C] Sun Microsystems，1973 年
- D] 剑桥大学，1972 年

28) 哪个函数是所有 C 程序都必须包含的唯一函数？

- A] start( )
- B] system( )
- C] **main( )**
- D] printf( )

29) 哪个是有效的字符串函数？

- A] strpbrk
- B] **strlen**
- C] strxfrm
- D] strcut

30) 以下哪一项不是正确的变量类型？

- A] float
- B] **real**
- C] int
- D] double

31) 我们可以通过使用什么在 C 程序中插入预先编写的代码

- A] #read
- B] #get
- C] **#include**
- D] #put

32) for 循环中的第一个表达式是

- A] 循环的步长值
- B] **计数器变量的值**
- C] 以上任意一个
- D] 以上都不是

33) break 语句用于

- A] 退出程序
- B] **退出当前迭代**
- C] 以上两者
- D] 以上都不是

34) continue 语句用于

- A] 继续执行下一行代码
- B] **停止当前迭代并从开头开始下一次迭代**
- C] 处理运行时错误
- D] 以上都不是

35) 在 C 中 \t 的用途是什么

- A] 用于插入垂直制表符
- B] **用于插入制表符**
- C] 将光标放在行尾
- D] 将光标放在行首

36) 以下程序的输出将是什么

```c
#include <stdio.h>
void main()
{
    char test = 'S';
    printf("\n%c", test);
}
```

- A] **S**
- B] 错误
- C] 垃圾值
- D] 以上都不是

37) 以下哪一项用作字符串终止字符？

- A] 0
- B] **\0**
- C] /0
- D] 以上都不是

38) 由于 C 中的变量作用域

- A] **在函数中创建的变量不能在另一个函数中使用**
- B] 在函数中创建的变量可以在另一个函数中使用
- C] 在函数中创建的变量只能在 main 函数中使用
- D] 以上都不是

39) 以下程序的输出将是什么

```c
#include <stdio.h>
main()
{
    int x, y = 10;
    x = y * NULL;
    printf("%d", x);
}
```

- A] 错误
- B] **0**
- C] 10
- D] 垃圾值

40) calloc() 和 malloc() 之间的区别

- A] calloc() 接受一个参数，而 malloc() 需要两个参数
- B] **malloc() 接受一个参数，而 calloc() 需要两个参数**
- C] malloc() 将分配的内存初始化为零
- D] calloc() 将分配的内存初始化为 NULL

41) 以下哪一项/哪些是有效的 C 关键字

- A] integer
- B] **int**
- C] null
- D] 以上都不是
