

# 8 • 指针 173

```cpp
a = *ptr; // ptr 未被初始化。
std::cout << a << '\n';
```

例如，如果在此之前添加语句 `ptr = &b;`，程序将成功执行；a 将等于 b 且程序输出 10。通常，在 [a] Unix/Linux 环境中，这种错误通过弹出的运行时消息 "Segmentation fault"（段错误）来指示。同样，在接下来的代码中，由于 ptr 未初始化，读取一个值并将其保存到 *ptr* 中是非常重要的。

```cpp
int *ptr, i;
cin >> *ptr;
```

如果我们在 `cin` 之前添加语句 `ptr = &i;`，代码就是正确的；输入的值被存储在 *ptr* 中，即 `i` 中。务必记住，在使用指针之前对其进行初始化，不要让它随风飘荡。听听 Bob Dylan 的《Blowing in the wind》来时刻牢记。* &* 放在一起使用时会相互抵消。例如，以下程序显示了 `i` 的地址：

```cpp
#include <iostream> // Example 8.5
int main() {
    int *ptr, i;
    ptr = &i;
    std::cout << &i << ' ' << *ptr << ' ' << &ptr << ' ' '\n';
}
```

因为 `/**` 标记了注释的开始，在如 `a = b*/ptr;` 的语句中，`/*` 之后的任何内容都被视为注释，会导致编译错误。在这种情况下，请留一个空格或使用括号。例如 `a = b/ptr;` 或 `a = b/(*ptr);`。
让我们看看，根据你目前学到的知识，你能找到以下程序的输出吗？

```cpp
#include <iostream> // Example 8.6
int main() {
    int *ptr1, i = 4;
    double *ptr2, j = 1.78;
    ptr1 = &i;
    ptr2 = &j;
    *ptr1 = i + *ptr2;
    std::cout << i << ' ' << sizeof(ptr1)*sizeof(ptr2) << ' ' << sizeof(ptr2) << ' ' '\n';
    return 0;
}
```

由于 `ptr1` 指向 `i` 的地址而 `ptr2` 指向 `j` 的地址，语句 `*ptr1 = i+*ptr2` 等同于 `i+j`。由于 `i` 是整数，它变成了 5。正如所说，无论指针指向的类型是什么，指针变量分配的大小是相同的。假设它是 4 个字节（octets）且 `ptr2` 是一个指向 double 的指针，程序显示：5 16 8

注意，因为 `sizeof` 不求值其操作数，因此指针不需要有一个有效值。例如，我们可以写：

```cpp
double *p;
cout << sizeof(*p) << '\n';
```

由于 `sizeof` 知道 `*p` 的类型是 `double`，它不需要解引用指针。

# 练习题

C.8.1 使用 `p1` 和 `p2` 指针并完成以下程序，先读取两个数字并交换它们所指向的值。然后使用相同的程序显示这些值之差的绝对值。变量 `i` 和 `j` 只能使用一次。

```cpp
#include <iostream>
using std::cout;
using std::cin;

int main()
{
    float *p1, *p2, i, j, tmp;
    ...
}
```

答案：

```cpp
#include <iostream>
using std::cout;
using std::cin;

int main()
{
    float *p1, *p2, i, j, tmp;
    /* 指针在用于存储输入值之前必须进行初始化。 */
    p1 = &i;
    p2 = &j;

    cout << "Enter values: ";
    cin >> *p1 >> *p2;

    tmp = *p2;
    *p2 = *p1;
    *p1 = tmp;

    if((*p1-*p2) > 0)
        cout << *p1-*p2 << '\n';
    else
        cout << -(p1-*p2) << '\n';
    return 0;
}
```

C.8.2 以下程序的输出是什么？

```cpp
#include <iostream>
int main() {
    int *ptr1, *ptr2, *ptr3, i = 0, j = 1, k = 2;

    ptr1 = &i;
    i = *ptr1 ? 3 : 4;

    ptr2 = &j;
    j = *ptr2 + *ptr1;

    ptr3 = &k;
    k = *ptr3 + *ptr2;
    std::cout << *ptr1 << ' ' << *ptr2 << ' ' << *ptr3 << '\n';
    return 0;
}
```

答案：由于 `ptr1` 指向 `i` 的地址 `ptr2` 指向 `j` 的地址，语句 `*ptr1 ? 3 : 4` 等同于 `i ? 3 : 4`。由于 `i` 是 0，它变成了 4。由于 `ptr2` 指向 `j` 的地址，`*ptr2` 等于 `j`，即 1。因此 `j = *ptr2 + *ptr1 = 1+4 = 5`。同样，由于 `ptr3` 指向 `k` 的地址，`*ptr3` 等于 `k`，即 2。因此 `k = *ptr3 + *ptr2 = 2+5 = 7`。由于 `*ptr1`、`*ptr2` 和 `*ptr3` 的值分别等于 `i`、`j` 和 `k`，程序显示：4 5 7

C.8.3 使用指针和 `while` 循环完成以下程序显示 1 到 10 的整数。变量 `i` 只使用一次。

```cpp
#include <iostream>
int main() {
    int *p, i;
    ...
}
```

答案：

```cpp
#include <iostream>
int main() {
    int *p, i;

    p = &i;
    *p = 1;
    while(*p <= 10) {
        std::cout << *p << '\n';
        (*p)++; /* 如你所示，必须使用括号 */
    }
    return 0;
}
```

C.8.4 以下程序的输出是什么？

```cpp
#include <iostream>
int main()
{
    int *ptr1, *ptr2, i = 10, j = 20;

    ptr1 = &i;
    ptr2 = &j;

    ptr2 = *ptr1 + *ptr2;
    *ptr2 *= 2;
    std::cout << *ptr1 + *ptr2 << '\n';
    return 0;
}
```

答案：语句 `ptr2 = &ptr1` 意味着 `ptr2` 指向 `ptr1` 指向的地址，即 `i` 的地址。因此 `*ptr2` 等于 `i`。由于两个指针都指向 `i` 的地址，语句 `*ptr1+ptr2` 等于 `10+10=20`。同样，语句 `*ptr2 *= 2` 等于 `*ptr2=2*2=40`。结果是程序显示 `*ptr1+ptr2=40+40`，即 80。

C.8.5 使用 `p2` 指针完成以下程序，连续读取学生成绩，直到用户输入 -1。使用 `p1` 指针找到有多少学生成绩在 [5, 10] 之间，使用 `p3` 指针显示最高分。变量 `sum`、`max` 和 `grade` 只能使用一次。

```cpp
#include <iostream>
int main()
{
    int *p1, sum;
    float *p2, *p3, max;
    ...
}
```

答案：

```cpp
#include <iostream>
int main()
{
    int *p1, sum;
    float *p2, *p3, max, grade;

    p1 = &sum;
    *p1 = 0;

    p3 = &max;
    *p3 = 0;

    p2 = &grade;
    while(*p2 != -1) {
        std::cout << "Enter grade: ";
        std::cin >> *p2;
        if(*p2 == -1)
            break;
        if(*p2 >= 5 && *p2 <= 10) {
            (*p1)++;
            if(*p2 > *p3)
                *p3 = *p2;
        }
    }
    std::cout << *p1 << " students passed (max:" << *p3 << ")\n";
    return 0;
}
```

# VOID* 指针

有时我们可能需要存储或向函数传递指针，而我们不知道该变量内存地址的类型。在这种情况下，使用了 `void` 类型。`void*` 指针是一种通用指针，从意义上它可以指向任何类型的指针。`void*` 指针可以赋值给另一个 `void*` 指针。同样，非 `void*` 指针也可以赋值给另一个 `void*` 指针。例如：

```cpp
void *ptr1, *ptr2;
int i, j, *ptr3 = &i;
ptr1 = ptr3;
ptr2 = ...
```

注意，除了 `void*`，为了赋值另一种类型给指针，需要进行类型转换。例如：

```cpp
void *ptr1;
int *p2;
...
```

通常，`void*` 指针用于函数参数，以便传递不同类型的值而不丢失信息。我们在第 25 章将看到类型转换（如 `reinterpret_cast`）以访问变量。例如：

```cpp
#include <iostream> // Example 8.47
int main()
{
  void *ptr;
  char s[] = "abcd";
  int i = 10;

  ptr = &i;
  *ptr += 20; // 错误，需要转换
  *(int*)ptr += 20; // 现在可以了
  std::cout << i << '\n';
}
```

```cpp
ptr = s+2;
*(char*)ptr++;
std::cout << ptr << '\n';
```

