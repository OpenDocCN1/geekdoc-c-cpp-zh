```
```c
/* array_of_pointers.c: Prints array1 using array2 which contains
   pointers to elements of array1. */
#include <stdio.h>
#define SIZE 6
int main(void)
{
    short n, arr[] = {11, 33, 55, 77, 99, 22};
    short *p_arr[SIZE];                /* Array of pointers */
    for (n = 0; n < SIZE; n++) {
        p_arr[n] = &arr[n];
        printf("%hd ", *p_arr[n]);
    }
    return 0;
}

/* PROGRAM 12.11: array_of_pointers.c */

11 33 55 77 99 22

/* PROGRAM OUTPUT: array_of_pointers.c */
```
```

arr 的两种视图使用 p_arr 以及一个直接显示元素的视图。整个练习由四个简单的 for 循环和一个嵌套循环处理。

第一个循环填充两个数组（arr 和 p_arr），同时保持输入项数量的计数。第二个循环解引用指针以显示 arr 的元素。嵌套循环使用与程序 10.7 相同的逻辑框架，不同之处在于当前练习重新排列存储在 p_arr 中的指针。请注意，关系运算符已从 > 更改为 <，因为这个程序反转数组。最后，最后两个循环使用指针呈现 arr 的排序视图，同时也确定 arr 没有以任何方式改变。

我们使用表达式 *p_arr[i] 来求值 arr[i]，但理论告诉我们 p_arr[i] 与 *(p_arr + i) 相同。毕竟，p_arr 表示 &p_arr[0]，而 &p_arr[0] 本身包含一个指针。所以 p_arr[i] 等价于 *(p_arr + i)。** 在 C 中有意义吗？将 *p_arr[i] 替换为 **(p_arr + i) 在第二个 for 循环中，并说服自己确实如此。第 12.15 节讨论了指向指针的指针。

# ## 12.15 POINTER TO A POINTER

正如第 12.14 节的最后一段让我们相信的那样，C 支持指向另一个指针的指针。这个指针反过来可以指向另一个指针，以此类推。在最简单的层面上，指向指针的指针是这样声明的：

```
```c
int **q;
```
```

这个指针目前不指向任何地方。在 (i) 将 q 指向一个指针变量（比如 p），并且 (ii) 将 p 指向另一个对象（比如简单变量 x）之后，它可以被完全解引用。那么，如果 p = &x 且 q = &p，那么 x 的值可以使用双重间接求值：

```
```c
**q                     Same as x and *p
```
```