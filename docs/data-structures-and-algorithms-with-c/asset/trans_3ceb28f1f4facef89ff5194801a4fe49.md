

字符串的字符被一对双引号括起来。编译器负责处理被一对双引号括起来的字符串。编译器负责将字符串中字符的 ASCII 码存储在内存中，并在末尾存储空终止符。

在初始化字符串时，维度可以是可选的（类似于数值数组），在这种情况下，如果未指定维度，编译器将根据初始化器的数量推断维度。例如，以下初始化是有效的。

```
char city[] = "Kolkata";
```

在这种情况下，编译器将假设字符串的大小为 8。

此外，大小可能大于初始化中的字符数；在这种情况下，剩余的内存单元将用空字符填充。例如，考虑以下内容：

```
char city[10] = "Kolkata";
```

因此，内存中的存储将如下：

| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |
|---|---|---|---|---|---|---|---|---|---|
| K | o | l | k | a | t | a | \0 | \0 | \0 |

图 3.17：字符串表示

但是，请记住，大小不能小于初始值中的字符数。

例如，初始化 char city[7] = "Kolkata"; 是无效的，这时编译器可能会产生编译时错误，或者不会有字符串终止符 (\0)，结果如果我们打印它，可能会得到一些不希望的结果。

## 读取字符串

通常，带有 %s 格式说明符的 scanf() 函数用于从终端读取字符字符串。

### 示例：

```
char city[15];
scanf ("%s", city);
```

scanf() 语句有一个缺点，即一旦发现空白字符（换行符、制表符、空格等），它就会终止语句。假设我们输入字符串 Hello India，则只会读取字符串 Hello，因为单词 Hello 后面有一个空格，它就会终止字符串。因此，通常情况下，无法使用 scanf() 读取一行文本。

### 示例：

```
char city [15];
scanf ("%[^\n]", city);
printf("\n %s", city);
```

> 注意：可以在变量名前不使用 & 符号来使用 scanf()。

此外，可以使用非格式化输入函数 gets 来读取字符串。函数 gets 的一般形式是 gets (string_name)；

该函数从终端读取字符到字符串中，直到遇到换行字符，最后在字符串末尾分配一个空字符。

### 示例：

```
char city[15];
gets(city);
```

## 写入字符串

带有格式说明符 %s 的 printf 语句可用于在屏幕上显示字符串。

### 示例：

```
printf("%s", string);
```

可用于显示数组字符串的全部内容。

另外，printf 函数可用于打印常量字符串，例如：

### 示例：

```
printf("Hello India");
```

我们还可以使用非格式化输出函数 puts() 在屏幕上显示字符串。

### 示例：

```
puts(string);
```

要显示常量字符串，我们可以这样使用 puts：

```
puts("Hello India");
```

由于 C 语言没有为字符串提供任何运算符，因此我们无法操作字符串。例如，我们不能直接将一个字符串赋值给另一个字符串。

### 示例：

```
char String1[30], String2[30];
String1 = "Hello"; /* Invalid */
String2 = "India"; /* Invalid */
String1 = String2; /* direct assignment not possible */
```

这些都无效。要将一个字符串中的字符复制到另一个字符串，我们可以逐个字符地复制。

同样，也无法通过关系运算符 (==) 直接比较两个字符串。

### 示例：

```
char String1[] = "Hello";
char String2[] = "India";
if(String1 == String2) /* direct comparison not possible */
printf("\n Strings are same");
else
printf("\n Strings are not same");
```

## 字符串数组

迄今为止，我们一直在讨论仅处理单个字符串，它是一个一维字符数组。但是，在许多应用程序中，需要处理一组字符串。在这种情况下，我们需要一个二维字符数组，称为字符串数组。一维字符数组的每个元素都是一个 ASCII 字符。但是，二维数组的每个元素都是一个字符串。

例如，考虑以下声明：

```
char os[5][10] = { "Unix",
                   "Linux",
                   "Windows",
                   "Macintosh",
                   "DOS"
                 };
```

上述字符串数组最多可容纳五个字符串。此外，每个字符串最多可容纳十个字符（包括空字符）。

在上述声明之后，内存中可能出现以下情况：

| | [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |
|---|---|---|---|---|---|---|---|---|---|---|
| os[0] | U | n | i | x | \0 | | | | | |
| os[1] | L | i | n | u | x | \0 | | | | |
| os[2] | W | i | n | d | o | w | s | \0 | | |
| os[3] | M | a | c | i | n | t | o | s | h | \0 |
| os[4] | D | O | S | \0 | | | | | | |

图 3.18：字符串数组

这里，os[0] 表示字符串“Unix”，os[1] 表示字符串“Linux”，os[2] 表示“Windows”，os[3] 表示“Macintosh”，os[4] 表示“DOS”。

## 对字符串执行的操作

需要对字符串执行不同种类的操作。

表 3.2：字符串操作

| 操作 | 描述 |
|---|---|
| 查找长度 | 查找字符串的长度。 |
| 复制 | 将一个字符串复制到另一个字符串。 |
| 连接 | 将一个字符串追加到另一个字符串的末尾。 |
| 比较 | 比较两个字符串以查找它们是否相同。 |
| 反转 | 反转字符串。 |
| 大写 | 将字符串中的小写字母（如果有）转换为大写。 |
| 小写 | 将字符串中的大写字母（如果有）转换为小写。 |
| 排序 | 将所有字符串按字典顺序排列。 |
| 字符串匹配 | 在字符串中搜索模式。 |

## 字符串长度

字符串的长度返回字符串的字符总数，这不一定等于其存储容量。空字符串的长度为零。

### 查找字符串长度的算法

- 算法：STRING_LENGTH (S)
- [S 是给定字符串]
- 1. 设置 N = 0
- 2. 当 S[N] != Null 时重复步骤 3
- 3. N = N + 1
  - [循环结束]
- 4. 返回 N

在 C 语言中，strlen() 函数计算并返回字符串中的字符数。长度不包括空字符，但包括空格。strlen() 函数的一般形式是

```
n = strlen (string);
```

这里 n 是一个整数变量，用于接收给定字符串长度的值。

### 程序 3.2：使用 strlen() 函数查找字符串的长度

```
#include<stdio.h>
#include<string.h>
main()
{
 char str[100];
 int length;
 printf("Enter the string:");
 gets(str);
 length = strlen(str);
 printf("\\nNumber of characters in the string=%d",length);
}
输出：
Enter the string:Hello world
Number of characters in the string=11
```

## 字符串复制

将字符串的当前值复制到另一个具有与原始字符串相同值的字符串中。不能使用赋值运算符复制字符串。

### 将字符串复制到另一个字符串的算法

- 算法：STRING_COPY (T, S)
- [S 是源字符串，T 是目标字符串]
- 1. 设置 I = 0
- 2. 当 S[I] != Null 时重复步骤 3
- 3. T[I] = S[I]
- 4. I = I + 1
  - [循环结束]
- 5. 设置 T[I] = Null
- 6. 返回

在 C 语言中，strcpy() 函数用于复制字符串。该函数的语法如下所示：

```
strcpy( string1, string2 );
```

strcpy 函数将 string2 的内容赋值给 string1，其中 string2 可以是字符数组变量或字符串常量。但是，string1 应该足够大，以容纳要复制到其中的字符串。

### 程序 3.3：使用 strlen() 函数将一个字符串的内容复制到另一个字符串

```
#include<stdio.h>
#include<string.h>
main()
{
    char string1[30];
    char string2[] = "Hello World";
    printf("\nSecond string was %s",string2);
    strcpy(string1, string2);
    printf("\n Now first strings is:%s",string1);
}
输出：
Second string was: Hello World
Now first strings is: Hello World
```

## 两个字符串的连接

当组合两个字符串时，即将一个字符串的内容追加到另一个字符串的末尾。此操作称为连接。

### 连接两个字符串的算法

- 算法：STRING_CONCAT (T, S)
- {字符串 S 追加到字符串 T 的末尾}
- 1. 设置 I = 0, J = 0
- 2. 当 T[I] != Null 时重复步骤 3
- 3. I = I + 1
  - [循环结束]
- 4. 当 S[J] != Null 时重复步骤 5 到 7
- 5. T[I] = S[J]
- 6. I = I + 1
- 7. J = J + 1
  - [循环结束]
- 8. 设置 T[I] = Null
- 9. 返回

在 C 语言中，strcat() 函数将两个字符串连接在一起。strcat() 函数的一般形式是：

