
## 例题 6.4

图6.4所示的程序试验了多种用于读取整数的输入格式选项。

```c
Program

main()
{
    int a,b,c,x,y,z;
    int p,q,r;
    printf("Enter three integer numbers\n");
    scanf("%d %*d %d",&a,&b,&c);
    printf("%d %d %d \n\n",a,b,c);
    printf("Enter two 4-digit numbers\n");
    scanf("%2d %4d",&x,&y);
    printf("%d %d\n\n", x,y);
    printf("Enter two integers\n");
    scanf("%d %d", &a,&x);
    printf("%d %d \n\n",a,x);
    printf("Enter a nine digit number\n");
    scanf("%3d %4d %3d",&p,&q,&r);
    printf("%d %d %d \n\n",p,q,r);
    printf("Enter two three digit numbers\n");
    scanf("%d %d",&x,&y);
    printf("%d %d",x,y);
}

Output

Enter three integer numbers
1 2 3
1 3 -3577
Enter two 4-digit numbers
6789 4321
67 89
Enter two integers
44 66
4321 44
Enter a nine-digit number
123456789
66 1234 567
Enter two three-digit numbers
123 456
89 123
```

*图6.4 使用 scanf 读取整数*

```c
printf("\n\np = %.12f\nq = %.12e", p,q);
}

Output
Values of x and y:12.3456 17.5e-2
x = 12.345600
y = 0.175000
Values of p and q:4.142857142857 18.5678901234567890
p = 4.142857142857
q = 1.856789012346e+001
```

*图6.5 实数的读取*

### 6.4.3 输入字符串

我们已经看到如何使用 **getchar** 函数从终端读取单个字符。使用 **scanf** 函数也可以实现同样的功能。此外，**scanf** 函数可以输入包含多个字符的字符串。以下是读取字符串的格式规范：

`%ws or %wc`

对应的参数应是指向字符数组的指针。不过，当参数是指向 **char** 变量的指针时，%c 可用于读取单个字符。

## 例题 6.6

图6.6说明了使用 **%wc** 和 **%ws** 读取字符串的方法。

图6.6中的程序说明了用于读取字符串的各种字段规范的用法。当我们使用 **%wc** 读取字符串时，系统会等到输入第 w<sup>th</sup> 个字符为止。

**注意**，**%s** 规范在遇到空白字符时终止读取。因此，**name2** 只读取了 "New York" 的第一部分，而第二部分被自动赋给 **name3**。然而，在第二次运行中，字符串 "New-York" 被正确地赋给 **name2**。

```c
Program

main()
{
    int no;
    char name1[15], name2[15], name3[15];
    printf("Enter serial number and name one\n");
    scanf("%d %15c", &no, name1);
    printf("%d %15s\n\n", no, name1);
    printf("Enter serial number and name two\n");
    scanf("%d %s", &no, name2);
    printf("%d %15s\n\n", no, name2);
    printf("Enter serial number and name three\n");
    scanf("%d %15s", &no, name3);
    printf("%d %15s\n", no, name3);
}

Output

Enter serial number and name one
1 123456789012345
1 123456789012345r
Enter serial number and name two
2 New York
2 New
Enter serial number and name three
2 York
Enter serial number and name one
1 123456789012
1 123456789012r
Enter serial number and name two
2 New-York
2 New-York
Enter serial number and name three
3 London
3 London
```

*图6.6 字符串的读取*

某些版本的 `scanf` 支持以下用于字符串的转换规范：

```text
%[characters]
%[^characters]
```

`%[characters]` 规范意味着输入字符串中只允许出现括号内指定的字符。如果输入字符串包含任何其他字符，则字符串将在第一次遇到此类字符时终止。`%[^characters]` 规范则完全相反。也就是说，脱字符（^）之后指定的字符不允许出现在输入字符串中。读取字符串时，一旦遇到这些字符之一就会终止。

## 例题 6.7

图6.7中的程序说明了 `%[ ]` 规范的功能。

```c
Program-A

        main()
        {
                char address[80];
                printf("Enter address\n");
                scanf("%[a-z]", address);
                printf("%-80s\n", address);
        }

Output

    Enter address
    new delhi 110002
    new delhi

Program-B

    main()
    {
        char address[80];
        printf("Enter address\n");
        scanf("%[^\n]", address);
        printf("%-80s", address);
    }

Output

    Enter address
    New Delhi 110 002
    New Delhi 110 002
```

*图6.7 字符串转换规范 %[ ] 的说明*

### 读取空白字符

我们之前已经看到，%s 说明符不能用于读取包含空白字符的字符串。但是，借助 %[ ] 规范可以做到这一点。空白字符可以包含在方括号内，从而使 *scanf* 能够读取带空格的字符串。请记住，小写字母和大写字母是不同的。参见图6.7。

### 6.4.4 读取混合数据类型

可以使用一条 *scanf* 语句输入包含混合模式数据的数据行。在这种情况下，应注意确保输入数据项在*顺序和类型*上与控制规范匹配。当尝试读取与预期类型不匹配的数据项时，*scanf* 函数不会继续读取，并立即返回已读取的值。语句

```c
scanf ("%d %c %f %s", &count, &code, &ratio, name);
```

将正确读取数据

```text
15 p 1.575 coffee
```

并将这些值按它们出现的顺序赋给变量。某些系统接受用整数代替实数，反之亦然，并且输入数据会被转换为控制字符串中指定的类型。

> *注意* 格式字符串中 %c 规范之前的空格是必需的，用于跳过 p 之前的空白字符。

### 6.4.5 输入错误检测

当 *scanf* 函数完成读取其列表时，它会返回成功读取的数据项数量。该值可用于测试读取输入时是否发生任何错误。例如，语句

```c
scanf("%d %f %s", &a, &b, name);
```

如果输入以下数据，将返回值 3：

`20 150.25 motor`

如果输入以下行，将返回值 1：

`20 motor 150.25`

这是因为该函数在期望浮点值时遇到了字符串，因此会在读取第一个值后终止扫描。

## 例题 6.8

图6.8中给出的程序说明了如何测试 **scanf** 函数读取数据的正确性。

**scanf** 函数预期读取三个数据项，因此，当所有三个变量的值都被正确读取时，程序会打印出它们的值。在第三次运行中，第二个数据项与变量类型不匹配，因此读取被终止，并打印错误消息。第四次运行的情况相同。

在最后一次运行中，尽管数据项与变量不匹配，但没有打印错误消息。当我们尝试为 **int** 变量读取一个实数时，整数部分被赋给该变量，而被截断的小数部分被赋给下一个变量。

> **注意** 字符 '2' 被赋给字符变量 c。

```c
Program

main()
{
  int a;
  float b;
  char c;
  printf("Enter values of a, b and c\n");
  if (scanf("%d %f %c", &a, &b, &c) == 3)
    printf("a = %d b = %f c = %c\n", a, b, c);
  else
    printf("Error in input.\n");
}

Output

Enter values of a, b and c
12 3.45 A
a = 12    b = 3.450000    c = A
Enter values of a, b and c
23 78 9
a = 23    b = 78.000000   c = 9
Enter values of a, b and c
8 A 5.25
Error in input.
Enter values of a, b and c
Y 12 67
Error in input.
Enter values of a, b and c
15.75 23 X
a = 15      b = 0.750000      c = 2
```

**图6.8** *scanf 输入中的错误检测*

常用的 **scanf** 格式代码见表6.2。

**表6.2** *常用的 scanf 格式代码*

| 代码 | 含义 |
|---|---|
| %c | 读取单个字符 |
| %d | 读取十进制整数 |
| %e | 读取浮点值 |
| %f | 读取浮点值 |
| %g | 读取浮点值 |
| %h | 读取短整数 |
| %i | 读取十进制、十六进制或八进制整数 |
| %o | 读取八进制整数 |
| %s | 读取字符串 |
| %u | 读取无符号十进制整数 |
| %x | 读取十六进制整数 |
| %[...] | 读取由单词组成的字符串 |

以下字母可用作某些转换字符的前缀。

- h 表示短整数
- l 表示长整数或 double
- L 表示 long double

> **注意** C99 增加了一些格式代码。参见附录“C99 特性”。

### 6.4.6 使用 scanf 时的注意事项

如果不仔细规划，使用 **scanf** 时可能会发生一些“疯狂”的事情。由于 I/O 例程不是 C 语言的一部分，它们要么作为 C 库的独立模块提供，要么作为操作系统（如 UNIX）的一部分提供。随着系统新版本的发布，这些例程会不时添加新特性。在使用这些例程之前，我们应该查阅系统参考手册。以下是编写 **scanf** 语句时需要牢记的一些通用要点。

- 1. 除控制字符串外，所有函数参数*必须*是指向变量的指针。
- 2. 控制字符串中包含的格式规范应按顺序与参数匹配。
- 3. 输入数据项必须用空格分隔，并且必须按相同顺序与接收输入的变量匹配。
