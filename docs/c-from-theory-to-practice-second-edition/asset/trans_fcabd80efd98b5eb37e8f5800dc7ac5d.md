
由于 *(s+1) 等价于 s[1]，字符串变为 "%d\n"，程序会显示 '%' 字符的 ASCII 值。

数组参数也可以声明为指针。例如，声明：

```
void test(int arr[]);  and  void test(int *arr);
```

两者是等价的。编译器对两者处理相同，并将指针传递给函数。因此，第二种声明更准确，因为它明确指出只传递了一个指针，而不是数组的拷贝。然而，我们更倾向于第一种，以明确显示传递数组的意图。第二种声明是模糊的；读者无法判断函数是接受多个值还是指向单个变量的指针。

另外，我们也可以使用指针算术来访问数组元素。例如：

```
void test(int arr[])
{
    *arr = 0; /* Equivalent to arr[0] = 0. */
    arr++;
    *arr = 0;
}
```

真正有趣的是语句 arr++。我们能改变数组的值吗？当然不能，你现在已经知道，当数组名用作指针时，它是一个 const 指针。那么，为什么编译器允许这个语句呢？因为，正如所说，虽然 arr 声明为数组，但实际上它是一个指针。因此，它可以被赋予新值。再举一个例子，下面的代码能否编译，如果能，输出是什么？

```
void test(int arr[])
{
    int i = 20, b[10];
    arr = b;
    *arr = 10;
    arr = &i;
    *arr = 30;
    printf("%d %d", b[0], i);
}
```

当然能编译；arr 被当作普通指针处理。该函数输出 10 和 30。

![](img/b8da5dcf9ba7f1fad5213c453d095246_352_0.png)

> 为了防止函数改变数组元素的值，将参数声明为 const。

例如，使用声明：

```
void test(const int arr[]);
```

test() 不能修改任何 arr 元素的值。注意，这并不意味着原始数组需要声明为常量。它只是表示 test() 可以将 arr 当作只读数据处理。

在向函数传递数组时，我们可以传递它的一部分。例如：

```c
#include <stdio.h>

void test(int ptr[]);

int main(void)
{
    int i, arr[6] = {1, 2, 3, 4, 5, 6};

    test(arr+3); /* Alternatively, test(&arr[3]) ... */
    for(i = 0; i < 6; i++)
        printf("%d ", arr[i]);
    return 0;
}

void test(int ptr[])
{
    int i, tmp[3] = {10, 20, 30};

    for(i = 0; i < 3; i++)
        ptr[i] = tmp[i];

    *ptr = *(ptr-1);
}
```

当 test() 被调用时，我们有 ptr = arr+3，也就是说，从第四个元素开始的 arr 部分被传递。由于我们将 ptr 用作数组，ptr[0] 对应 arr[3]，ptr[2] 对应 arr[5]。因此，循环使 arr[3]、arr[4] 和 arr[5] 的值分别等于 10、20 和 30。由于 ptr 指向 arr[3]，语句 *ptr = *(ptr-1); 等价于 arr[3] = arr[2]。因此，程序显示 1 2 3 3 20 30

让我们出一个 tricky 的问题。我们能否写下面的代码？

```c
void test(int ptr[])
{
    printf("%d ", ptr[-1]);
    ...
}
```

听起来可能很奇怪，但答案是肯定的。正如你在第 8 章已经知道的，ptr[-1] 等价于 *(ptr-1)，而由于 ptr 等于 arr+3，它等价于 *(arr+3-1)，也就是 arr[2]。如果可以确定向后方向的元素确实存在，那么使用负索引访问它们是安全的。当然，如果有人选择这种语法，我们也无话可说，只能献上 New York Dolls 的《Personality Crisis》。

![](img/b8da5dcf9ba7f1fad5213c453d095246_353_0.png)

虽然我们可以使用 sizeof 运算符来查找数组变量的大小，但在函数中无法用它来查找数组参数的大小。

例如，考虑下面的程序：

```
#include <stdio.h>

void test(int arr[]);

int main(void)
{
    int a[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    test(a);
    printf("Array = %u bytes\n", sizeof(a));
    return 0;
}

void test(int arr[])
{
    printf("Ptr = %u bytes\n", sizeof(arr));
}
```

由于数组参数被当作指针处理，sizeof 运算符计算的是指针变量的大小，而不是数组实际的大小。因此，程序输出指针为 4，数组为 40。

因为实际传递给函数的是指针，所以在方括号内写数组长度没有任何效果。编译器会忽略它；它不会检查数组是否真的具有指定的长度。事实上，传递的指针是指向未知长度数组第一个元素的指针。这就是为什么我们把方括号留空；我们不想制造出传递了特定数量元素的假象。让函数知道数组长度的一种简单方法是将其作为额外参数传递。例如，我们可以这样声明 test()：

```
void test(int arr[], int size);
```

并写成 test(a, 10); 来调用它。

另外，我们也可以定义一个常量，例如 #define SIZE 10，并在需要的地方使用该常量，而不是传递额外参数。另一种方法是使用特殊值来表示数组的结束，前提是当然该值不会出现在数组中。例如，如果数组包含一个字符串，就不需要传递其长度，因为空字符指示了它的结束。

在结束之前有一个简单的问题，以检验你是否完全理解了这一非常重要部分。下面的程序输出的值是否相同？如果是，为什么？

```
#include <stdio.h>

void test(int arr[]);

int main(void)
{
    int a[10];

    printf("Addr: %p\n", a);
    test(a);
    return 0;
}
void test(int arr[])
{
    printf("Addr: %p\n", &arr);
}
```

不要急着看下一页的答案，好好思考一下。

不仅你回答了是，而且你还为答案提供了理由？我们又一次骗了你……注意接下来出现的陷阱。不要生气，听一听 Oasis 的《Don't Look Back in Anger》，再检查一下程序。

第一个 printf() 输出的是 a 变量的地址。test() 输出的是 arr 变量的地址。它们相同吗？当然不；它们位于不同的内存位置。然而，arr 的值等于 a；也就是说，如果去掉 &，输出值就会相同。

## 练习

### C.11.15 编写一个函数，以包含学生考试成绩的数组和两个成绩（例如 a 和 b）作为参数，并返回 [a, b] 范围内的成绩平均值。编写一个程序，读取 50 名学生的成绩以及两个成绩 a 和 b，并使用该函数显示平均值。程序应强制用户输入 a 的值小于或等于 b。

```
#include <stdio.h>

#define SIZE 50

float avg_arr(float arr[], float min, float max);

int main(void)
{
    int i;
    float a, b, k, arr[SIZE];

    for(i = 0; i < SIZE; i++)
    {
        printf("Enter grade: ");
        scanf("%f", &arr[i]);
    }
    do
    {
        printf("Enter min and max grades: ");
        scanf("%f%f", &a, &b);
    } while(a > b);

    k = avg_arr(arr, a, b);
    if(k == -1)
        printf("None grade in [%f, %f]\n", a, b);
    else
        printf("Avg = %.2f\n", k);
    return 0;
}

float avg_arr(float arr[], float min, float max)
{
    int i, cnt = 0;
    float sum = 0;
    for(i = 0; i < SIZE; i++)
    {
        if(arr[i] >= min && arr[i] <= max)
        {
            cnt++;
            sum += arr[i];
        }
    }
    if(cnt == 0)
        return -1;
    else
        return sum/cnt;
}
```

### C.11.16 编写一个函数，以字符串作为参数并返回其长度。不要使用 strlen()。

```
unsigned int str_len(const char *str)
{
    unsigned int i = 0;
    while(str[i] != '\0') /* Count the characters up to the null character. */
        i++;
    return i;
}
```

注释：str_len() 是 strlen() 库函数的实现示例。

### C.11.17 下列函数的作用是什么？

```
unsigned int test(const char *str)
{
    const char *ptr = str;
    while(*str++) /* Equivalent to while(*str++ != '\0') */
        ;
    return str-ptr-1;
}
```

答案：很难，不要害怕。

在每次迭代中，循环将 *str 的值与 0 比较，等价于 '\0'，然后 str 被递增，以指向下一个数组元素。例如，在第一次迭代中，*str 等于 str[0]，然后它变为 str[1]，以此类推。一旦 *str 等于空字符，循环终止。

回顾第 8 章和指针算术，指向同一数组的两个指针相减的结果是元素个数，因此，在本例中是它们之间的字符数。ptr 指向第一个元素，而 str 在最后一次递增后指向空字符之后的下一个位置。这就是为什么我们要减去 1，以减去这个位置。
