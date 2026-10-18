
正如初始化列表中所列。对于初始化，变量和常量对象都可以使用。否则，如果提供了`__num`但初始化列表中的值不够，剩余的值将设置为默认值；对于内置类型，这意味着将它们设置为`0`。另一方面，如果初始化值的数量多于`elems_num`中声明的数量，则会发出编译错误。然而，该语言足够灵活，允许我们跳过初始化，如图A.1b所示。当运行时优化是主要问题时，此选项可用于大型数组。在这种情况下，数组值应在后续代码行中使用之前设置。

数组的元素可以通过下标运算符`[i]`访问，如下面代码片段中的第[4–5]行所示。在这种情况下，请记住：

- 允许的索引*i*的范围是从0到*N*−1，其中*N*是数组中的元素个数。在我们的示例中，元素个数已定义为`kTabSize`

```cpp
/* Set new values to tab */
for ( int i = 0; i < kTabSize; ++ i )
    tab[ i ] = i;
```

- 指向数组第一个元素的*常量指针*

因此，在我们的示例中，`tab`的类型是`int * const`，它指向索引为0的元素。这意味着`tab`本身不能被修改，而它所指向的元素可以被修改（这是一个普通的`int`，而不是`const int`）。

如果记住以下两个事实，通过指针操作指针和数组就会更简单（参见3.12节）：

- 解引用指针的类型是它所指向对象的类型
- 向指针加上*n*个值，使其指向其类型的第*n*个对象

下面代码片段演示了使用指针访问数组元素的示例：

```cpp
/* arr is a const pointer to its first element, */
/* so we can also write this */
for( int i = 0; i < kTabSize; ++ i )
    *( tab + i ) = i;
```

在第[9]行，指针`tab`增加了索引*i*。由于指针的算术缩放，`( tab + i )`精确地指向`tab`数组的第*i*个元素。剩下要做的就是解引用该指针并给它赋值。请注意，对指针的加法会*按比例缩放*，使得访问的是数组的下一个元素，而不是下一个字节。

在第三个版本中，数组的元素通过指针`tab_ptr`访问，该指针最初设置为指向`tab`数组中的第一个对象。但这一次，`tab_ptr`会被更新，逐个指向数组的元素。

```cpp
/* Array access via the pointer */
int * tab_ptr = tab;    /* tab is constant, tab_ptr is variable */
for( int i = 0; i < kTabSize; ++ i )
    * tab_ptr ++ = i;
```

前面的操作如图A.2所示。

[第596页]

内置数组可以包含其他内置数组作为其元素。这样，我们可以创建多维数组，如下例所示：

```
/* Multidimensional arrays */
enum Dims { kRows = 2, kCols = 2 };
/* kRows is external, kCols internal index */
double affineMatrix[ kRows ][ kCols ] = { 0.0 }; /* initialize all elements to 0.0 */
```

可以使用下标访问其元素，如下例所示：

```
/* Set all off-diagonal elements to -1 */
for( int r = 0; r < kRows; ++ r )
for( int c = 0; c < kCols; ++ c )
if( r != c )
affineMatrix[ r ][ c ] = -1.0;
```

多维结构也可以通过指针访问。下面的示例执行相同的操作，只是第[10]行和第[15]行之间有一处不同：

```
/* The same with pointers */
for( int r = 0; r < kRows; ++ r )
for( int c = 0; c < kCols; ++ c )
if( r != c )
* ( * ( affineMatrix + r ) + c ) = -1.0;
```

为了识别此表达式中的关键步骤，我们首先确定`affineMatrix`的类型。这是一个指向第一个元素的指针，而第一个元素恰好是一个单独的行：一个类型为`double [ kCol ]`的一维数组。因此，`affineMatrix`遵循指针缩放，单次递增会前进

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_596_0.png)

[第597页]

其值的大小等于一整行元素的大小，这些元素共有`kCol`个`double`类型对象。换句话说，`affineMatrix`指向第一行，`affineMatrix + 1`指向第二行，依此类推。另一方面，每一行都是一个一维数组，因此指针移动1就会移动到该行中的下一个`double`对象，依此类推。现在我们可以按如下方式解释第[15]行：

- `affineMatrix + r` 指向数组中的第r行，该行是一个包含kCol个`double`类型元素的数组
- `* (affineMatrix + r)` 表示该行，因此是指向该行第一个`double`类型对象的指针
- `(affineMatrix + r) + c` 是指向第r行中第c个`double`对象的指针
- `* ( * (affineMatrix + r) + c )` 通过指针为我们带来这个`double`对象，即`affineMatrix`中索引为(r,c)的元素。通过这种间接访问，可以将该对象的值设置为-1.0，如上一代码片段的最后一行所示

表3.15列出了基于指针操作复制内存的`BackwardMemCopy`函数。此外，`MiniMatrix`类示例说明了基于指针访问矩阵元素的使用。

# A.2.2 将数组传递给函数 – 主函数

`main`函数是为我们的程序调用的第一个函数。然而，`main`并不是程序启动后执行的第一段代码，因为还有一些内务处理任务需要完成，例如静态和全局变量初始化等。程序中应该只有一个`main`函数，它应定义为以下两个版本之一：

+   1. 无输入参数：

```
int main()
{
    /* body of main */
}
```

+   2. 带调用参数：

```
int main( int argc, char ** argv )
{
    /* body of main */
}
```

第二个版本的含义在图A.3中解释，图中显示了示例`CPro.exe`在终端窗口中的一次调用，带有两个参数`2019`和`bin`。系统将控制权连同这两个参数一起传递给`main`函数。参数`argc`传递了由第二个参数`argv`指向的C风格字符串数组中的元素个数。因此，`argv`表示一个元素为C风格字符串（即以0哨兵结尾的`char`表）的表。该表的第一个字符串保存了所调用应用程序的完整路径。下一个字符串包含命令行中传入的连续参数，依此类推。数值需要从C风格字符串转换而来。

因此，在`main`中收到`argc`后，我们应该只使用`argv[0]`到`argv[argc-1]`，尽管`argv[argc]`也保证为0（即nullptr）。

`main`的两个参数展示了一种C风格的方式将数组传递给函数：一个是指向其第一个元素的指针，另一个是数组中的元素总数。由于该数组存储的是`char *`类型的C风格文本，因此指向其第一个元素的指针类型为`char **`。

[第598页]

清单A.1包含了CPro.exe的完整C实现。程序首先从命令行读取一个十进制值和转换基数，然后以所请求的基数输出转换后的值。第[1-2]行包含了两个标准C头文件，其中包含常用数学函数和输入/输出函数的声明。第[7]行包含了`ToBinConvert`函数的声明，该函数在`main`中被调用来将十进制值转换为其二进制表示。它的完整定义放在`main`之后。在C语言中编写注释时，我们使用`/* */`符号。C++继承了这种风格，并引入了`//`类型的单行注释。

# ## 清单A.1 用于转换十进制值的C程序。参数作为实参传递给main函数（在CPro的main.c中）。

```
#include <stdlib.h>
#include <stdio.h>

/\* Function declaration. \*/
void ToBinConvert( int val );

/\* The CProg converts a decimal value into an equivalent in one of the bases: oct, bin, hex.
Param no. 1 is a decimal integer value.
An optional param no. 2 is the output base "oct", "bin", "hex"
If not provided, then the same value is displayed. \*/
/\* C program starts with the main function \*/
int main( int argc, char ** argv )
{
    printf( "Value converter. Calling format: \\nCPro.exe dec_val [bin,oct,hex] \\n" );
}
```
