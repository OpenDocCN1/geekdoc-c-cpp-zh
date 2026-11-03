
正确。如果百分比低于75%，显示“Please ask your teacher for extra help.”，然后重置程序以便另一名学生尝试。如果百分比为75%或更高，显示“Congratulations, you are ready to go to the next level!”，然后重置程序以便另一名学生尝试。

## 5.53 (计算机辅助教学：难度等级)

Exercises 5.50 through Exercise 5.52 developed a computer-assisted instruction program to help teach an elementary-school student multiplication. Modify the program to allow the user to enter a difficulty level. At a difficulty level of 1, the program should use only single-digit numbers in the problems; at a difficulty level of 2, numbers as large as two digits, and so on.

## 5.54 (计算机辅助教学：变化的问题类型)

Modify the program of Exercise 5.53 to allow the user to pick a type of arithmetic problem to study. An option of 1 means addition problems only, 2 means subtraction problems only, 3 means multiplication problems only and 4 means a random mixture of all these types.

- 6.1 引言
- 6.2 数组
- 6.3 定义数组
- 6.4 数组示例
- 6.4.1 定义数组并使用循环设置数组元素值
- 6.4.2 在定义中使用初始化列表初始化数组
- 6.4.3 使用符号常量指定数组大小并通过计算初始化数组元素
- 6.4.4 求数组元素的和
- 6.4.5 使用数组汇总调查结果
- 6.4.6 使用直方图绘制数组元素值
- 6.4.7 掷骰子60,000,000次并在数组中汇总结果
- 6.5 使用字符数组存储和操作字符串
- 6.5.1 使用字符串初始化字符数组
- 6.5.2 使用字符初始化列表初始化字符数组
- 6.5.3 访问字符串中的字符
- 6.5.4 向字符数组输入
- 6.5.5 输出表示字符串的字符数组
- 6.5.6 演示字符数组
- 6.6 静态局部数组和自动局部数组
- 6.7 向函数传递数组
- 6.8 排序数组
- 6.9 案例研究：使用数组计算均值、中位数和众数
- 6.10 搜索数组
- 6.10.1 使用线性搜索搜索数组
- 6.10.2 使用二分搜索搜索数组
- 6.11 多维数组
- 6.11.1 说明双下标数组
- 6.11.2 初始化双下标数组
- 6.11.3 设置一行中的元素
- 6.11.4 求二维数组中元素的总和
- 6.11.5 二维数组操作
- 6.12 变长数组
- 6.13 安全的 C 编程

## 6.1 引言

This chapter introduces data structures. Arrays are data structures consisting of related data items of the same type. In Chapter 10, we discuss C’s notion of struct—a data structure consisting of related data items of possibly different types. Arrays and structs are “static” entities in that they remain the same size throughout program execution (they may, of course, be of automatic storage class and hence created and destroyed each time the blocks in which they’re defined are entered and exited).

## 6.2 数组

An array is a group of contiguous memory locations that all have the same type. To refer to a particular location or element in the array, we specify the array’s name and the position number of the particular element in the array.

Figure 6.1 shows an integer array called c, containing 12 elements. Any one of these elements may be referred to by giving the array’s name followed by the position number of the particular element in square brackets ([]). The first element in every array is the zeroth element (i.e., the one with position number 0). An array name, like other identifiers, can contain only letters, digits and underscores and cannot begin with a digit.

![](img/bf54db922e6fa8319cba11069e785521_242_0.png)

Fig. 6.1 | 12-element array.

The position number in square brackets is called the element's index or subscript. An index must be an integer or an integer expression. For example, the statement

```
c[2] = 1000;
```

assigns 1000 to array element c[2]. Similarly, if a = 5 and b = 6, then the statement

```
c[a + b] += 2;
```

adds 2 to array element c[11]. An indexed array name is an lvalue—it can be used on the left side of an assignment.

Let's examine array c (Fig. 6.1) more closely. The array's name is c. Its 12 elements are referred to as c[0], c[1], c[2], ..., c[10] and c[11]. The value stored in c[0] is -45, the value of c[1] is 6, c[2] is 0, c[7] is 62 and c[11] is 78. To print the sum of the values contained in the first three elements of array c, we'd write

```
printf("%d", c[0] + c[1] + c[2]);
```

To divide the value of element 6 of array c by 2 and assign the result to the variable x, write

```
x = c[6] / 2;
```

The brackets used to enclose an array's index are actually considered to be an operator in C. They have the same level of precedence as the function call operator (i.e., the parentheses that are placed after a function name to call that function). Figure 6.2 shows the precedence and associativity of the operators introduced to this point in the text.

| Operators | Associativity | Type |
|---|---|---|
| [ ] ( ) ++ (postfix) -- (postfix) | left to right | highest |
| + - ! ++ (prefix) -- (prefix) (type) | right to left | unary |

Fig. 6.2 | Operator precedence and associativity. (Part 1 of 2.)

| Operators | Associativity | Type |
|---|---|---|
| * / % | left to right | multiplicative |
| + - | left to right | additive |
| < <= > >= | left to right | relational |
| == != | left to right | equality |
| && | left to right | logical AND |
| || | left to right | logical OR |
| ?: | right to left | conditional |
| = += -= *= /= %= | right to left | assignment |
| , | left to right | comma |

Fig. 6.2 | Operator precedence and associativity. (Part 2 of 2.)

## 6.3 定义数组

Arrays occupy space in memory. You specify the type of each element and the number of elements each array requires so that the computer may reserve the appropriate amount of memory. The following definition reserves 12 elements for integer array c, which has indices in the range 0–11.

```
int c[12];
```

The definition

```
int b[100], x[27];
```

reserves 100 elements for integer array b and 27 elements for integer array x. These arrays have indices in the ranges 0–99 and 0–26, respectively. Though you can define multiple arrays at once, defining only one per line is preferred, so you can add a comment explaining each array's purpose.

Arrays may contain other data types. For example, an array of type char can store a character string. Character strings and their similarity to arrays are discussed in Chapter 8. The relationship between pointers and arrays is discussed in Chapter 7.

## 6.4 数组示例

This section presents several examples that demonstrate how to define and initialize arrays, and how to perform many common array manipulations.

### 6.4.1 定义数组并使用循环设置数组元素值

Like any other variables, uninitialized array elements contain garbage values. Figure 6.3 uses for statements to set the elements of a five-element integer array n to zeros (lines 11–13) and print the array in tabular format (lines 18–20). The first printf statement (line 15) displays the column heads for the two columns printed in the subsequent for statement.

```c
1   // Fig. 6.3: fig06_03.c
2   // Initializing the elements of an array to zeros.
3   #include <stdio.h>
4
5   // function main begins program execution
6   int main(void)
7   {
8       int n[5]; // n is an array of five integers
9
10      // set elements of array n to 0
11      for (size_t i = 0; i < 5; ++i) {
12          n[i] = 0; // set element at location i to 0
13      }
14
15      printf("%s%13s\n", "Element", "Value");
16
17      // output contents of array n in tabular format
18      for (size_t i = 0; i < 5; ++i) {
19          printf("%7u%13d\n", i, n[i]);
20      }
21  }
```

| 元素 | 值 |
|---|---|
| 0 | 0 |
| 1 | 0 |
| 2 | 0 |
| 3 | 0 |
| 4 | 0 |

**Fig. 6.3** | Initializing the elements of an array to zeros.

Notice that the counter-control variable `i` is declared to be of type `size_t` in each `for` statement (lines 11 and 18), which according to the C standard represents an unsigned integral type.¹ This type is recommended for any variable that represents an array's size or indices. Type `size_t` is defined in header `<stddef.h>`, which is often included by other headers (such as `<stdio.h>`). [Note: If you attempt to compile Fig. 6.3 and receive errors, simply include `<stddef.h>` in your program.]

### 6.4.2 在定义中使用初始化列表初始化数组

The elements of an array can also be initialized when the array is defined by following the definition with an equals sign and braces, `{ }`, containing a comma-separated list of array initializers. Figure 6.4 initializes an integer array with five values (line 9) and prints the array in tabular format.

1. On some compilers, `size_t` represents `unsigned int` and on others it represents `unsigned long`. Compilers that use `unsigned long` typically generate a warning on line 19 of Fig. 6.3, because `%u` is for displaying unsigned ints, not unsigned longs. To eliminate this warning, replace the format specification `%u` with `%lu`.
