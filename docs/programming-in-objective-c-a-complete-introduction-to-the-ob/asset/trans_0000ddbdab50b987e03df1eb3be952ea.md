
如果 `valuesPtr` 指向 `values` 数组的最后一个元素之后，则结果为 TRUE（非零），否则为 FALSE（零）。根据我们之前的讨论，你可以将之前的表达式替换为等效表达式：

```
valuesPtr > values + 99
```

这是可以的，因为不带下标的 `values` 是指向数组开头的指针。（记住，这等同于编写 `&values[0]`）。程序 13.15 展示了指向数组的指针。`arraySum` 函数计算整数数组包含元素的和。

## 程序 13.15

```
// 计算整数数组元素和的函数
#import <Foundation/Foundation.h>

int arraySum(int array[], int n)
{
    int sum = 0, *ptr;
    int *arrayEnd = array + n;

    for ( ptr = array; ptr < arrayEnd; ++ptr )
        sum += *ptr;

    return (sum);
}

int main(int argc, char *argv[])
{
    NSAutleasePool *pool = [[NSAutleasePool alloc] init];
    int arraySum(int array[], int n);
    int values[10] = { 3, 7, -9, 3, 6, -1, 7, 9, 1, -5 };

    NSLog("Sum is %i", arraySum(values, 10));
    [pool release]
}
```

## 程序 13.15 输出

The sum is 21

在 `arraySum` 函数内部，定义了整数指针 `arrayEnd`，并将其设置在 `array` 的最后一个元素之后。随后设置了一个 `for` 循环来顺序处理 `array` 的元素；然后将 `ptr` 的值设置为指向进入循环时的起始位置。每次循环中，`ptr` 指向的 `array` 元素被加到 `sum` 中。`for` 循环增加 `ptr` 的值，使其指向数组中的下一个元素。当 `ptr` 指过数组末尾时，退出 `for` 循环并将 `sum` 的值返回给调用者。

## 第 13 章 C 语言底层特性

### 它是数组，还是指针？

要将数组传递给函数，你只需要指定数组名称，就像你之前调用 `arraySum` 函数时所做的那样。我们在本节提到，为了产生数组的指针，只需要指定数组名称。这意味着在调用 `arraySum` 函数时，传递给函数的是指向 `values` 数组的指针。情况确实如此，这解释了为什么你可以在函数内部更改数组的元素。

但如果传递给函数的是数组指针，函数内部声明为指针的形式参数又是哪个？换句话说，在 `arraySum` 函数中 `array` 的声明中，为什么没有这样声明：

```
*array;
```

函数内部对数组的所有引用不都应该使用指针变量来实现吗？

为了回答这些问题，我们必须重申之前关于指针和数组的话。我们提到过，如果 `valuesPtr` 指向与名为 `values` 的数组中相同类型的元素，那么表达式 `*(valuesPtr + i)` 等同于表达式 `values[i]`，假设 `valuesPtr` 已设置为 `values` 的开头。由此得出，你可以使用表达式 `*(values - i)` 来引用 `values` 数组的第 `i` 个元素——通常情况下，如果 `x` 是任何类型的数组，表达式 `x[i]` 始终可以在 Objective-C 中等价表示为 `*(x - i)`。

如你所示，指针和数组在 Objective-C 中紧密相关，这就是为什么你可以在 `arraySum` 函数内部将 `array` 声明为“int 数组”或“int 指针”。在前面的程序中，两种声明均有效——尝试一下看看。

如果你将使用索引来引用数组元素，请将相应的形式参数声明为 `array`。这更准确地反映了函数对数组的使用。同样，如果你将参数作为数组的指针，请将其声明为指针类型。

## 字符字符串指针

使用数组指针最常见的应用之一是作为字符字符串指针。原因出于便利性和效率。为了展示如何方便地使用字符串指针，让我们写一个 `copyString` 函数将一个字符串拷贝到另一个字符串。如果你使用普通的数组索引方法编写此函数，你可能会这样编写代码：

```
void copyString(char to[], char from[]) {
  int i;

  for ( i = 0; from[i] != '\0'; ++i )
    to[i] = from[i];
}
```

## 指针 285

`for` 循环在空字符拷贝到 `to` 数组之前就退出，因此解释了函数最后一条语句的必要性。

如果你使用指针编写 `copy`，就不再需要索引变量 `i`。程序 13.16 展示了指针版本。

## 程序 13.16

```
#import <Foundation/Foundation.h>
void copyString(char *to, char *from)
{
    for (; ; *from != '\0'; ++from, ++to)
        *to = *from;

    *to = '\0';
}

int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [NSAutoreleasePool alloc];
    void copyString(char *to, char *from);
    char string1[] = "A string to be copied.";
    char string2[50];

    copyString(string2, string1);
    NSLog("%@s", string2);

    copyString(string2, "So is this.");
    [pool drain];
    return 0;
}
```

## 程序 13.16 输出

A string to be copied.
So is this.

> `copyString` 函数将两个形式参数 `to` 和 `from` 定义为指针，而不是数组，正如之前的 `copyString` 版本中所做的那样。这反映了函数使用这两个变量的需求。
进入一个循环（无初始条件），将 `from` 指向的字符串拷贝到 `to` 指向的字符串中。每次循环，`from` 和 `to` 指针各递增 1。这使得 `from` 指针指向要从源字符串拷贝的下一个字符，并使得 `to` 指针指向目标字符串中存储下一个字符的位置。
当 `from` 指针指向空字符时，退出 `for` 循环。函数随后将空字符放在目标字符串的末尾。

## 第 13 章 C 语言底层特性

在 `main` 例程中，调用了两次 `copyString` 函数——第一次是将 `string1` 的内容拷贝到 `string2`，第二次是将常量字符串 "So is this." 的内容拷贝到 `string2`。

## 常量字符串与指针

在之前的程序中，调用

```
copyString(string2, "So is this.");
```

能够工作意味着，当常量字符串作为参数传递给函数时，该字符实际上被传递给了一个指针。这不仅在这种情况下是真的，而且可以概括为：每当在 Objective-C 中使用常量字符串，就会产生指向该字符字符串的指针。

这一点现在听起来可能有点困惑，但正如我们在第 4 章中简要提到的，我们在这里提到的常量字符字符串是 C 风格字符串。它们不是对象。如你所知，常量字符串对象是通过在字符串前加上 @ 符号创建的，例如 `@"This is okay."`。你不能相互替换。

如果 `textPtr` 被声明为字符指针，如下所示

```
char *textPtr;
```

那么语句

```
textPtr = "A character string.";
```

将 `textPtr` 分配为指向常量字符字符串 "A character string." 的指针。注意区分字符指针和字符数组，因为之前的赋值类型对于字符数组是无效的。例如，如果 `text` 被定义为字符数组，语句如下：

```
char text[80];
```

你不能编写这样的语句：

```
text = "This is not valid.";
```

只有在初始化字符数组时，Objective-C 才允许你对数组执行此类类型的赋值：

```
char text[80] = "This is okay.";
```
