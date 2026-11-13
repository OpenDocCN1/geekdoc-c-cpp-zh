

```cpp
{
 int i;
 if(size==0)
 {
 cout<<"array is underflow\n";
 return;
 }
 cout<<"the elements are\n";
 for(i=1;i<=size;i++)
 cout<<a[i]<<" ";
 cout<<"\n";
 }
 void main()
 {
 int ch,n;
 clrscr();
 cout<<"enter the size of the array\n";
 cin>>n;
 array<float> a(n);
 while(1)
 {
 cout<<"menu\n";
 cout<<"1.add\n";
 cout<<"2.delete\n";
 cout<<"3.display\n";
 cout<<"4.exit\n";
 cout<<"enter your choice\n";
 cin>>ch;
 switch(ch)
 {
 case 1:
 a.insert();
 break;
 case 2:
 a.deletee();
 break;
 case 3:
 a.display();
 break;
 case 4:
 exit(0);
 break;
 default:
 cout<<"invalid option\n";
 break;
 }
 }
 }
```

### 输出

enter the size of the array
10
menu
1.add
2.delete
3.display
4.exit
enter your choice
1
enter the element
2
menu
1.add
2.delete
3.display
4.exit
enter your choice
1
enter the element
3
menu
1.add
2.delete
3.display
4.exit
enter your choice
3
the elements are
2 3
menu
1.add
2.delete
3.display
4.exit
enter your choice
2
the deleted element is 3
menu
1.add
2.delete
3.display
4.exit
enter your choice
4

### 4.7 数组作为参数

数组可以作为参数传递给函数。在 C++ 中，不可能将完整的内存块按值作为参数传递给函数，但允许传递其地址。在实践中，这几乎具有相同的效果，并且速度更快，是一种更高效的操作。

要接受数组作为参数，在声明函数时只需指定数组作为其参数的类型和名称，即一个标识符和一对方括号[]。例如，以下函数：

```cpp
void procedure(int arg[])
```

接受一个类型为 int、名为 arg 的数组参数。要向此函数传递数组，数组声明如下：

```cpp
int myarray[40];
```

编写如下调用即可：

```cpp
procedure(myarray);
```

### 程序 4.2

```cpp
/*arrays as parameters*/
#include<iostream>
using namespace std;
void printarray(int arg[], int length)
{
  for (int n=0;n<length;n++)
    cout<<arg[n]<< " ";
  cout<<endl;
}
int main ()
{
  int firstarray[]={5, 10, 15};
  int secondarray[]={2, 4, 6, 8, 10};
  printarray (firstarray,3);
  printarray (secondarray,5);
  return 0;
}
```

### 输出

5 10 15
2 4 6 8 10

在程序 4.2 中，第一个参数 (int arg[]) 接受任何元素类型为 int 的数组：长度任意。因此，一个指定每个数组长度的第二个参数与第一个参数一起传递给函数。这允许打印数组的 for 循环知道传递数组中的迭代范围，而不会越界。

在函数声明中，也可以包含多维数组。三维数组参数的格式如下：

```cpp
base_type[][depth][depth]
```

以多维数组作为参数的函数可以是：

```cpp
void procedure(int myarray[][3][4])
```

请注意，第一组方括号 [ ] 留空，而另外两组带有值。这是因为编译器必须能够确定函数中每个额外维度的深度。

### 4.8 字符序列

C++ 标准库拥有一个功能强大的 string 类，用于处理和操作字符串非常有用。然而，因为字符串实际上是字符序列，可以表示为 char 元素的数组。数组 char C[20] 可存储最多 20 个 char 类型的元素。它可以如图 4.13 所示表示。

![](img/45784b9f0334626143002ec0d63692fd_144_0.png)

图 4.13 字符数组

此数组可存储最多 20 个字符长的字符序列。但它也可以存储更短的序列。例如，在程序的某个时刻，char 数组 C 可以存储序列 "Hello" 或序列 "Merry Christmas"，因为两者都短于 20 个字符。由于字符数组可以存储比其总长度更短的序列，因此使用一个特殊字符来指示有效序列的结束，即空字符，其字面常量可写为 '\0'（反斜杠，零）。一个包含 20 个 char 类型元素的数组 C，可以通过存储字符序列 "Hello" 和 "Merry Christmas" 来表示，如图 4.14 所示。

![](img/45784b9f0334626143002ec0d63692fd_144_1.png)

图 4.14 字符串末尾的空字符

请注意，在有效内容之后包含了一个空字符 ('\0') 以指示序列的结束。灰色面板表示值未确定的 char 元素。

### 以空字符结尾的字符序列的初始化：

因为字符数组是普通数组，所以遵循相同的规则。例如，要用某个预定义的字符序列初始化字符数组，可以像其他数组一样进行：

```cpp
char myword[]={'H', 'e', 'l', 'l', 'o', '\0'};
```

在此情况下，声明了一个包含 6 个 char 类型元素的数组，用组成单词 "Hello" 的字符以及末尾的空字符 '\0' 进行初始化。但是 char 元素数组有一种使用字符串字面量初始化其值的附加方法。

在表达式中，通过将文本放在双引号 (") 之间来指定整个字符串，使其成为字符串字面量。例如，

```cpp
"the result is."
```

是一个常量字符串字面量。

带双引号的字符串 (") 是字面常量，其类型实际上是以空字符结尾的字符数组。因此，用双引号括起来的字符串字面量始终会在末尾自动追加一个空字符 ('\0')。

因此，名为 myword 的 char 元素数组通过以下两种方法之一，用以空字符结尾的字符序列进行初始化。

```cpp
char myword[]={'H', 'e', 'l', 'l', 'o', '\0'};
```

```cpp
char myword[]="Hello";
```

在两种情况下，字符数组 myword 都声明为包含 6 个 char 类型元素：组成单词 "Hello" 的 5 个字符加上一个最终的空字符 ('\0')，它指定序列的结束，而在第二种情况下，使用双引号 (") 时会自动追加它。

假设 mystext 是一个 char[] 变量，源代码中的如下表达式

```cpp
mystext = "Hello";
```

```cpp
mystext [] = "Hello";
```

都是无效的。同样，以下也是无效的：

```cpp
mystext={'H', 'e', 'l', 'l', 'o', '\0'};
```

了解更多关于指针的知识后，这可能更容易理解。因此，将澄清数组实际上是一个指向内存块的常量指针。

使用以空字符结尾的字符序列：以空字符结尾的字符序列是在 C++ 中处理字符串的自然方式。例如，cin 和 cout 支持以空字符结尾的序列作为字符序列的有效容器。因此，可以直接用它们从 cin 提取字符串或将字符串插入到 cout 中。

### 程序 4.3

```cpp
/* null-terminated sequences of characters*/
#include <iostream>
using namespace std;
int main ()
{
  char question[]="Please, enter your first name:";
  char greeting[]="Hello, ";
  char yourname[80];
  cout<<question;
  cin>>yourname;
  cout<<greeting<<yourname<<"!";
  return 0;
}
```

### 输出

Please, enter your first name:John
Hello, John!

在程序 4.3 中，声明了三个 char 类型的数组。前两个用字符串字面量常量初始化，而第三个未初始化。大小由它们初始化所用的字面量常量的长度隐式定义。而对于 yourname，则明确指定其大小为 80 个字符。最后，存储在 char 数组中的字符序列可以通过使用赋值运算符轻松转换为 string 对象。

```cpp
string mystring;
char myncts []="some text";
mystring=myncts;
```

### 4.9 应用

数组有广泛的应用。其中一些在此列出，并详细介绍了稀疏矩阵应用。

- 矩阵
- 稀疏矩阵
- 记录
- 有序列表

稀疏矩阵：矩阵是按行和列表示元素的方式。稀疏矩阵是零项比例较高的矩阵。图 4.15 说明了矩阵和稀疏矩阵。

![](img/45784b9f0334626143002ec0d63692fd_146_0.png)

图 4.15 矩阵和稀疏矩阵示例

图 4.16 显示了各种应用中最常用的 n 阶方稀疏矩阵。

