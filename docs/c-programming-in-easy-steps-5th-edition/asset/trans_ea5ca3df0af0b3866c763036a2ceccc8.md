

```cpp
string info = "\n\tThe Ballad of Reading Gaol" ;
info.append( "\n\t\tOscar Wilde 1898" );
// Add more statements here.
return 0 ;
}
```

- 3. 在主函数中，创建一个输出文件流对象——指定一种文件模式，该模式将追加到现有文本

```cpp
ofstream writer( "poem.txt" , ios::app );
```

- 4. 插入将字符串追加到文件或退出的语句，然后保存、编译并运行程序以查看结果

```cpp
if ( ! writer )
{
    cout << "Error opening file for output" << endl ;
    return -1 ;      // Signal an error then exit the program.
}
writer << info << endl ;      // Append output.
writer.close() ;              // Close filestream.
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_82_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_82_1.png)

文件必须允许程序拥有合适的读写权限。

## 读取字符与行

**ifstream** 文件流对象有一个 **get()** 函数，可以在循环中使用该函数读取文件，并依次将每个字符赋给作为其参数指定的 **char** 变量：

![](img/bf8dbdfb89042fadbaa73b4160c74bac_83_0.png)

- 1. 通过指定要包含的 C++ 库类和要使用的命名空间前缀，开始一个新程序

```cpp
#include <fstream>     // Include filestream support.
#include <iostream>
using namespace std ;
```

- 2. 添加一个包含最终 **return** 语句和两个变量声明的主函数——一个变量用于存储字符，另一个用于统计循环迭代次数

```cpp
int main()
{
  char letter ;
  int i ;
  // Add more statements here.
  return 0 ;
}
```

- 3. 在主函数中，创建一个输入文件流对象，以读取前面示例中的文本文件

```cpp
ifstream reader( "poem.txt" ) ;
```

- 4. 插入语句，如果文件流对象不存在则退出

```cpp
if ( ! reader )
{
  cout << "Error opening input file" << endl ;
  return -1 ;    // Signal an error then exit the program.
}
```

- 5. 接下来，插入一个循环读取文本文件，依次将每个字符赋给变量并输出其值

```cpp
else
for ( i = 0 ; ! reader.eof() ; i++ )
{
  reader.get( letter ) ;
  cout << letter ;
}
```

- 6. 最后，插入语句关闭文件流并输出循环迭代的总次数

```cpp
reader.close() ;
cout << "Iterations: " << i << endl ;
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_83_1.png)

请注意 ifstream 的 eof() 函数如何用于检查是否已到达“文件末尾”。

- 7. 保存、编译并运行程序，查看文本文件内容和循环次数显示在标准输出上

![](img/bf8dbdfb89042fadbaa73b4160c74bac_84_0.png)

这个程序运行得还算不错，但循环必须进行多次迭代才能输出文本文件的内容。可以通过在每次循环迭代中读取一行来提高效率：

- 8. 插入一个预处理指令，使 C++ string 库可被程序使用

```cpp
#include <string>
```

- 9. 将 `char` 变量声明替换为 `string` 变量声明

```cpp
string line ;
```

- 10. 替换 `for` 循环中的两条语句以读取行，然后再次保存、编译并运行程序

```cpp
getline( reader , line ) ;
cout << line << endl ;
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_84_1.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_84_2.png)

在每行输出后输出一个 **endl**——因为 **getline()** 在遇到 `\n` 换行符时会停止读取。

## 使用 getline 格式化

**getline()** 函数可以选择使用第三个参数来指定停止读取行的分隔符。这可用于分隔从数据文件中的制表列表读取的文本：

![](img/bf8dbdfb89042fadbaa73b4160c74bac_85_0.png)

format.cpp

- 1. 在纯文本编辑器中，创建一个包含 12 个数据项的文本文件，每行四个项目，每个项目之间用制表符分隔。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_85_1.png)

- 2. 通过指定要包含的 C++ 库类和要使用的命名空间前缀，开始一个新程序。

```cpp
#include <fstream>    // Include filestream support.
#include <string>
#include <iostream>
using namespace std;
```

- 3. 添加一个包含最终 **return** 语句和四个变量声明的主函数——一个固定数字、一个用于存储数据的 **string** 数组，以及两个设置为零的计数器变量。

```cpp
int main()
{
    const int RANGE = 12 ;
    string tab[RANGE] ;
    int i = 0, j = 0 ;
    // Add more statements here.
    return 0 ;
}
```

- 4. 插入一条语句以创建输入文件流对象。

```cpp
ifstream reader("records.txt");
```

- 5. 插入语句，如果文件流对象不存在则退出。

```cpp
if ( ! reader )
{
    cout << "Error opening input file" << endl ;
    return -1 ;
}
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_85_2.png)

string 数组必须具有足够数量的元素来存储每个数据项——如果需要处理更多记录，则需要扩大数组。

- 6. 接下来，插入一个循环，将每一行读取到 **string** 数组中——对于前三项，读取到 **\t** 制表符为止；对于每行的第四项，读取到 **\n** 换行符为止。

```cpp
while ( ! reader.eof() )
{
    if ( (i + 1) % 4 == 0 )
        getline( reader, tab[i++], '\n' );
    else
        getline(reader, tab[i++], '\t');
}
```

- 7. 现在，关闭文件流并重置计数器

```cpp
reader.close();
i = 0;
```

- 8. 插入第二个循环，输出存储在每个数组元素中的数据，并使用描述和换行符进行格式化

```cpp
while (i < RANGE)
{
    cout << endl << "Record Number: " << ++i << endl ;
    cout << "Forename: " << tab[i++] << endl ;
    cout << "Surname: " << tab[i++] << endl ;
    cout << "Department: " << tab[i++] << endl ;
    cout << "Telephone: " << tab[i++] << endl ;
}
```

- 9. 保存、编译并运行程序，查看文本文件的格式化输出

![](img/bf8dbdfb89042fadbaa73b4160c74bac_86_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_86_1.png)

if 语句测试项目编号（元素编号加 1）是否能被四整除，以确定读取到换行符还是制表符。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_86_2.png)

记录计数器必须使用前缀递增运算符，以便在输出变量值之前先递增变量。

## 操作输入与输出

输入和输出流的行为可以通过使用“插入运算符”配合 **cout** 和 **cin** 函数来修改。为其 **width()** 函数指定一个整数参数可设置流的字符宽度。当内容未填满整个流宽度时，可指定一个填充字符作为其 **fill()** 函数的参数来表示空白部分。类似地，浮点数默认的六位小数精度可以通过为其 **precision()** 函数指定一个整数来改变。使用插入运算符修改流的语句应位于使用 `<<` 或 `>>` 运算符的语句之前。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_87_0.png)

插入运算符只修改一个流对象——后续的流对象使用默认值，除非它们也先被插入运算符修改。

`<iostream>` 库提供了下表中列出的“操纵器”，它们使用 `<<` 或 `>>` 运算符修改流。

| 操纵器： | 显示： |
|---|---|
| noboolalpha* | 布尔值显示为 1 或 0 |
| boolalpha | 布尔值显示为 "true" 或 "false" |
| dec* | 整数以十进制（基数为 10）显示 |
| hex | 整数以十六进制（基数为 16）显示 |
| oct | 整数以八进制（基数为 8）显示 |
| right* | 文本在输出宽度中右对齐 |
| left | 文本在输出宽度中左对齐 |
| internal | 符号左对齐，数字右对齐 |
| noshowbase* | 不显示表示数字进制的前缀 |
| showbase | 显示表示数字进制的前缀 |
| noshowpoint* | 当小数为零时仅显示整数部分 |
| showpoint | 所有浮点数都显示小数点 |
| noshowpos* | 正数前不加 + 前缀 |
| showpos | 正数前加上 + 前缀 |
| noskipws* | 对 >> 输入不跳过空白字符 |
| skipws | 对 >> 输入跳过空白字符 |
| fixed* | 浮点数保留六位小数 |
| scientific | 以科学计数法显示浮点数 |
| nouppercase* | 科学计数法用 e，十六进制数用 ff |
| uppercase | 科学计数法用 E，十六进制数用 FF |

