
- (3) `<name-file>` 根据 ANSI 规范的形式在 (1) 或 (2) 中搜索。

30. 编译器可以将高级语言程序翻译成等效的低级语言程序。到目前，编译器产生的是机器级代码。我该如何配置编译器使其开始产生汇编级代码？

## 存储类与预处理器指令 10.43

```c
39. main()
{
    printf("Hello " "Readers!!");
}
```

```c
40. main()
{
    char *str="Hello";
    printf(str="Readers!!");
}
```

```c
41. #define PI=3.14
main()
{
    int rad=2;
    printf("Circumference of the circle is %f",2*PI*rad);
}
```

```c
42. #define PI 3.14
main()
{
    int rad=2;
    printf("Circumference of the circle is %f",2*PI*rad);
}
```

```c
43. #define PI 3.14;
main()
{
    int rad=2;
    printf("Circumference of the circle is %f",2*PI*rad);
}
```

```c
44. #define int char
main()
{
    int var;
    printf("The size of var is %d",sizeof(var));
}
```

```c
45. #define + - /
#define * /
main()
{
    int a;
    a=2+3*5;
    printf("The value of a is %d",a);
}
```

```c
46. #define clscr 200
main()
{
    printf("This will be printed\n");
    clrscr();
}
```

## 10.44 结构体与联合

```c
printf("The value is %d",clscr());
}
```

- 47. #define SQUARE(x) x*x

main()

{

printf("The square value of 2 is %d",SQUARE(2));

}

- 48. #define SQUARE(x) x*x

main()

{

printf("The square value of 2 is %d",SQUARE(2));

}

- 49. #define SQUARE(x) x*x

main()

{

int a=20,b;

b=SQUARE(2);

printf("The value of b is %d",b);

}

- 50. #define SQUARE(x) (x*x)

main()

{

int a=20,b;

b=SQUARE(2);

printf("The value of b is %d",b);

}

- 51. #define SQUARE(x) (x*x)

main()

{

int a=5,b;

b=SQUARE(a+2);

printf("The value of b is %d",b);

}

- 52. #define SQUARE(x) ((x)*(x))

main()

{

int a=5,b;

b=SQUARE(a+2);

printf("The value of b is %d",b);

}

- 53. #define SQUARE(x) ((x)*(x))

main()

{

int a=2,b;

b=SQUARE(++a);

printf("The value of b is %d",b);

}

## 存储类与预处理器指令 10.45

```c
55. #define SWAP(a,b) a^=b; b^=a; a^=b;
main()
{
    int a=20,b=10;
    printf("The values of a and b before swap are %d %d\n",a,b);
    SWAP(a,b);
    printf("The values of a and b after swap are %d %d\n",a,b);
}
```

```c
56. #define SWAP(a,b) a^=b; b^=a; a^=b;
main()
{
    int a=20,b=10;
    printf("Swap the values of a and b only if a is greater than b\n");
    if(a-b)
        SWAP(a,b);
    else
        printf("Values are not swapped\n");
    printf("Resultant values of a and b are %d %d\n",a,b);
}
```

```c
57. #define SWAP(a,b) a^=b; b^=a; a^=b;
main()
{
    int a=20,b=10;
    printf("Swap the values of a and b only if a is greater than b\n");
    if(a-b)
        SWAP(a,b);
    else
        printf("Values are not swapped\n");
    printf("Resultant values of a and b are %d %d\n",a,b);
}
```

```c
58. #define SWAP(a,b) a^=b; b^=a; a^=b;
main()
{
    int a=20,b=10;
    printf("Swap the values of a and b only if a is greater than b\n");
    if(a-b)
        SWAP(a,b);
    else
        printf("Values are not swapped\n");
}
```

## 10.46 结构体与联合

```c
printf("Resultant values of a and b are %d",a,b);
}
59. #define VALUE 100
main()
{
    int VALUE=100;
    printf("The VALUE is %d",VALUE);
}
```

```c
60. #define STR(x) #x
main()
{
    printf("Hello Readers!");
}
```

```c
61. #define STR(x) #x
main()
{
    printf("Hello Readers!");
}
```

```c
62. #define STR(x) #x
main()
{
    printf("Hello Readers!");
}
```

```c
63. #define STR(x) #x
main()
{
    printf("Hello Readers!");
}
```

```c
64. #define STR(x,y,z) #x#y#z
main()
{
    char str1[30]=STR(PROCESSOR);
    char str2[30]=STR(COMPILER);
    puts(str1);
    puts(str2);
}
```

```c
65. #define STR(x) #x
#include <stdio.h>
main()
{
    printf("Third form of include");
}
```

```c
66. #define PASTE(tk1,tk2) tk1##tk2
main()
{
    int var=100;
    printf("The value of var is %d",var);
}
```

## 存储类与预处理器指令 10.47

```c
67. #define PASTE(tk1,tk2) tk1##tk2
main()
{
    int var1=100,var2=200,var3=300;
    int i;
    for(i=0;i<3;i++)
        printf("The value of var is %d",i);
}
```

```c
68. #define PASTE(tk1,tk2) tk1##tk2
main()
{
    int var[]={100,200,300};
    int i;
    for(i=0;i<3;i++)
        printf("The value of var is %d",i);
}
```

```c
69. #define p(x,y,z) x##y##z
main()
{
    int arr[]={p(2,3,4), p(5,6), p(6,7), p(8,9), p(10,11)};
    int i;
    for(i=0;i<6;i++)
        printf("%d",arr[i]);
}
```

```c
70. #define CONST
main()
{
    printf("The value of CONST is %d",CONST);
}
```

```c
71. #define CONST
main()
{
    printf("The value of CONST is %d",CONST);
}
```

```c
72. #define CONST
main()
{
    printf("The value of CONST is %d",CONST);
}
```

```c
73. #define CONST
main()
{
    printf("The value of CONST is %d",CONST);
}
```

## 10.48 结构体与联合

```c
74. #define CONST
main()
{
    printf("The value of CONST is %d",CONST);
}
```

```c
75. #define VER I
main()
{
    #ifdef VER
        printf("Place code corresponding to version I");
    #else
        printf("Place code corresponding to version other than I");
    #endif
}
```

```c
76. #define VER I
main()
{
    #ifdef VER
        printf("Place code corresponding to version I");
    #else
        WILL IT BE COMPILATION ERROR??
    #endif
}
```

```c
77. #define VER=I
main()
{
    #if VER=I
        printf("Place code corresponding to version I");
    #else
        printf("Place code corresponding to version other than I");
    #endif
}
```

```c
78. #define VER=I
main()
{
    #if VER=I
        printf("Place code corresponding to version I");
    #else
        printf("Place code corresponding to version other than I");
    #endif
}
```

```c
79. #define VER I
main()
{
    int a=I;
    #if a==VER
        printf("Place code corresponding to version I");
    #else
    printf("Place code corresponding to version other than I");
    #endif
}
```

## 存储类与预处理器指令 10.49

```c
80. #define VER 1
main()
{
    const int a=1;
    #if a==VER
        printf("Place code corresponding to version I");
    #else
        printf("Place code corresponding to version other than I");
    #endif
}
```

```c
81. main()
{
    #ifdef WINDOWS
        PLACE CODE FOR WINDOWS OPERATING SYSTEM
    #elif defined(LINUX)
        PLACE CODE FOR LINUX OPERATING SYSTEM
    #else
        #error OPERATING SYSTEM IS NOT KNOWN
    #endif
}
```

```c
82. main()
{
    /* The C PREPROCESSOR */
    /* THERE ARE VARIOUS DIRECTIVES */
    PRAGMA IS ONE OF THEM */
    printf("THE PREPROCESSOR");
}
```

```c
83. #pragma option -C
main()
{
    /* The C PREPROCESSOR */
    /* THERE ARE VARIOUS DIRECTIVES */
    PRAGMA IS ONE OF THEM */
    printf("THE PREPROCESSOR");
}
```

```c
84. int req_var_value;
func()
{
    printf("This sets up the prerequisites of function main\n");
    req_var_value=200;
}
#pragma startup
main()
{
    printf("This is main\n");
    printf("The requisite value of variable is %d",req_var_value);
}
```

## 10.50 结构体与联合

```c
85. #define size_of(data)((char *)(Gdata+i))char *)(Gdata))
main()
{
    int INT;
    char CHAR;
    float FLOAT;
    double DOUBLE;
    printf("Size of int: %d\n",size_of(INT));
    printf("Size of char: %d\n",size_of(CHAR));
    printf("Size of float: %d\n",size_of(FLOAT));
    printf("Size of double: %d\n",size_of(DOUBLE));
}
```

## 选择题

- 86. A translator that converts a program written in a high-level language into an equivalent written in some other high-level language is

    a. Interpreter c. Assembler

    b. Compiler d. Preprocessor

- 87. Preprocessing is a phase of translation, which occurs

    a. Before compilation c. After compilation but before linking

    b. After compilation d. None of these

- 88. Which of the following are replaced within string literals?

    a. Macro names c. Trigraph sequences

    b. Digraph sequences d. None of these

- 89. Among function-like macro call and function call, which one is efficient time-wise?

    a. Function-like macro call c. Both take equal time

    b. Function call d. None of these

- 90. The following piece of code on execution leads to:

    main(){puts("Hello", "Readers!!");}

    a. Compilation error c. Readers!!

    b. Hello d. None of these

- 91. The following piece of code on execution leads to:

    #define puts printf

    main(){puts("Hello", "Readers!!");}
