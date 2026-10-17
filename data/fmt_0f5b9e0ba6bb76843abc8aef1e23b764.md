
```cpp
    char cArr[20]="abcd";

    ofstream file("first.dat");

    ofile<<cArr;

}
```

/*charFileOutput.cpp 的结束*/

5. 使用插入运算符向输出流插入对象：如果我们想使用插入运算符为特定类插入对象，我们需要对该类进行重载。运算符重载的概念、需要和用法将在下一章阐述。

### `put()` 函数

`put()` 函数是 `ostream` 类的成员。其原型为：
`ostream &put(char c);`

从原型可以看出，该函数可以相对于 `ostream` 类对象或任何派生自 `ostream` 类的对象被调用。这样一个对象是 `cout`。该函数将作为参数传递的字符复制到调用它的对象相关的输出文件中。让我们考虑列表 7.5 中的示例程序。

#### 列表 7.5 `put()` 函数

```cpp
/*put.cpp 的开始*/

#include<fstream.h>

void main()

{

    ofstream ofile("first.dat");

    ofile.put('a');

}

/*put.cpp 的结束*/
```

在列表 7.5 中，`put()` 函数相对于对象 `ofile` 调用。该对象与文件 `first.dat` 关联。因此，字符 'a' 被写入文件。正如前面提到的，`put()` 函数也可以配合 `cout` 对象使用（如列表 7.6所示）。

#### 列表 7.6 与 cout 对象使用 `put()` 函数

```cpp
/*coutPut.cpp 的开始*/

#include<iostream.h>

void main()

{

    cout.put('a');

}

/*coutPut.cpp 的结束*/
```

# 输出

a

列表 7.6 中 `put()` 函数的调用将在显示器上显示字符 'a'。
我们可能会想知道使用 `put()` 函数和插入运算符之间的区别。毕竟，我们可以使用插入运算符来代替调用 `put()` 函数，如下所示：

`cout<<'a';`

插入操作符（`<<`）与 `put()` 函数之间的区别在于，前者会根据设置的操符（manipulators）修改输出的格式，而后者会忽略操符的设置。格式化输出将在本章后面的章节中讨论。

## 7.5.2 文本输入

C++ 中通过以下方式实现文本输入：

- 提取操作符（`>>`）
- `get()` 函数
- `getline()` 函数

本章中的提取运算符，即提取运算符，可以用于从磁盘文件中输入值。提取运算符以文本模式进行输入。

提取运算符在 `istream` 类中被定义并重载。它的左侧接收一个 `istream` 类的对象或派生自 `istream` 类的对象。它的右侧接收一个基本数据类型的变量。它将与左侧对象关联的文件中在当前位置处找到的值复制到右侧的变量中。让我们研究它对不同类型数据的操作。必须记住，提取运算符对每种数据类型都进行了不同的重载，如下所示：

1. **使用提取运算符从输入流中提取字符：** 如果提取运算符的右侧是一个字符类型变量，它将从左侧对象关联的输入文件中读取一个字节，并将其写入变量中（列表 7.7）。

> 列表 7.7 使用提取运算符以文本模式输入字符

```cpp
/*Beginning of charFileInputText.cpp*/

#include<iostream.h>

#include<fstream.h>

void main() {

    ifstream ifile("first.dat"); //当前位置位于
    //文件的开头。
    // 假设文件中的第一个字节
    //包含 'A'。
    char Var;
    ifile>>Var;
    cout<<Var;

}

/*End of charFileInputText.cpp*/
```
输出
A

2. **使用提取运算符从输入流中提取整数：** 如果提取运算符的右侧是一个整数类型变量，它将从左侧对象关联的输入文件中读取字节，直到遇到空白符。它认为读取到的这组字节表示一个 10 进制格式的整数。因此，提取运算符将该值转换为 2 进制格式。最后，它将转换后的值写入变量中。

假设文件 `first.dat` 的内容如下：

11 22 33

我们必须注意，“11”后面有一个空格。文件的第一个字节具有字符‘1’的 ASCII 等效值。第二个字节也具有字符‘1’的 ASCII 等效值。第三个字节具有字符（空格）的 ASCII 等效值。第四个字节具有字符‘2’的 ASCII 等效值，依此类推。
现在让我们考虑列表 7.8。

# 列表 7.8 使用提取运算符以文本模式输入整数

```cpp
/*Beginning of intfileInputText.cpp*/

#include<iostream>

#include<fstream>

void main()

{

    ifstream ifile("first.dat");
    int iVar;
    ifile>>iVar;

}

/*End of intfileInputText.cpp*/
```
输出
11

如所述，提取运算符从文件中读取内容，直到遇到空白符。由于第三个字节包含空白符，因此它只读取了前两个字节。这两个字节表示 10 进制格式的数字十一。提取运算符将其转换为 2 进制。结果值占用四个字节。它将其写入变量 `iVar`。

3. **使用提取运算符从输入流中提取浮点数和双精度浮点数：** `float` 和 `double` 类型变量值的提取方式与整数类型变量相同。

4. **使用提取运算符从输入流中提取字符串：** 与整数的情况类似，提取运算符在读取字符数组的值时，会从文件中读取内容直到遇到空白符。

假设文件 `first.dat` 的内容如下：

abc def ghi

我们必须注意，“c”后面有一个空格。参见列表 7.9。

# 列表 7.9 使用提取运算符输入字符数组

```cpp
/*Beginning of charArrayInputText.cpp*/

#include<iostream>

#include<fstream>

void main()

{

    ifstream ifile("first.dat");
    char cArr[20];
    ifile>>cArr;
    cout<<cArr;

}

/*End of charFileInputText.cpp*/
```
输出
abc

显然，提取运算符读取到空白符为止，并将读取到的值存储在字符数组中。

5. **使用提取运算符从输入流中提取对象：** 如果我们想使用提取运算符从输入流中提取特定类的对象，我们必须对其进行重载。运算符重载的概念、必要性及其用法将在后面的章节中阐述。

## `get()` 函数

`get()` 函数在 `istream` 类中已定义。它从输入文件中读取一个字节，并存储在作为参数传递给它的变量中（列表 7.10）。`get()` 函数的原型如下：

`istream & :: get(char &);`

假设文件 `first.dat` 的内容如下：

abcd

列表 7.10 使用 `get()` 函数输入字符

```cpp
/*Beginning of charFileInputText.cpp*/

#include<iostream.h>

#include<fstream.h>

void main() {

  ifstream ifile("first.dat");
  char cVar;
  ifile.get(cVar);
  cout<<cVar;

}

/*End of charFileInputText.cpp*/
```
输出
a

## get() 函数

`get()` 函数在 `istream` 类中已定义。它从输入文件中读取一个字节，并存储在作为参数传递给它的变量中（列表 7.10）。`get()` 函数的原型如下：

`istream & :: get(char &);`

假设文件 `first.dat` 的内容如下：

abcd

列表 7.10 使用 `get()` 函数输入

```cpp
/*Beginning of charFileInputText.cpp*/

#include<iostream.h>

#include<fstream.h>

void main() {

  ifstream ifile("first.dat");
  char cVar;
  ifile.get(cVar);
  cout<<cVar;

}

/*End of charFileInputText.cpp*/
```
输出
a

（注：原文后续部分存在大量重复内容，已按要求不再重复输出）

列表 7.14 展示了如何使用 `write()` 函数将字符类型变量的值输出到显示器。

## **列表 7.14** 使用 `write()` 函数将字符类型值输出到显示器

```cpp
/*Beginning of writeCharConsole.cpp*/

#include <iostream>

using namespace std;

void main()

{

    char cVar;
    cVar = 'a';
    cout.write(&cVar,sizeof(char));

}

/*End of writeCharConsole.cpp*/
```

# 输出
a

显而易见，以文本模式（插入运算符、`put()` 函数）和二进制模式（`write()` 函数）输出字符类型值没有区别。在两种情况下都没有发生任何转换。

2. 使用 `write()` 函数向输出流中插入整数：列表 7.15 展示了如何使用 `write()` 函数将整数类型变量的值输出到磁盘文件。

## **列表 7.15** 使用 `write()` 函数将整数类型值输出到磁盘文件

正如我们已经讨论过的，被 ‘iVar’ 占据的四个字节中所包含的值将不经过任何转换直接复制到指定的输出文件中。列表 7.16 展示了如何使用 `write()` 函数将整数类型变量的值输出到显示器。

## **列表 7.16** 使用 `write()` 函数将整数类型值输出到显示器

```cpp
/*Beginning of writeIntConsole.cpp*/

#include <iostream.h>

void main()

{

    int iVar;
    iVar = 65;
    cout.write((char *)&iVar,sizeof(int));

// Stream and File Handling

}

/*End of writeIntConsole.cpp*/
```

# 输出

理解列表 7.16 的输出是有意思的。由于 `main()` 函数第二个语句的作用，被 ‘iVar’ 占据的四个字节中的第一个字节的八位被设置为表示数字‘65’的二进制等效值。其余三个字节中的位被设置为零。正如我们所知，显示器显示传递给它的每个字节的 ASCII 等效值。“65”的 ASCII 等效值是 ‘A’。因此，我们得到了这个输出。

显而易见，以文本模式（插入运算符、`put()`）和二进制模式（`write()` 函数）输出整数值之间存在重要区别。在前一种情况下，从内存读取的值的表示从从 2 转换为十 进制，然后复制到输出文件中。在后一种情况下没有这种转换。

- 3. 使用 `write()` 向输出流中插入浮点数和双精度浮点数：浮点和双类型值在二进制模式下的输出方式与整数类型值相同。

- 4. 使用 `write()` 向输出流中插入字符串：列表 7.17 展示了如何使用 `write()` 函数将字符数组的值输出到磁盘文件。

## 列表 7.17 使用 `write()` 函数将字符串输出到磁盘文件

```cpp
/*Beginning of writeCharArrDisk.cpp*/

#include<fstream>

void main()

{

    ofstream ofile("first.dat");
    char cArr[10]="abcdefgh";
    ofile.write(cArr,sizeof(cArr));

}

/*Beginning of writeCharArrDisk.cpp*/
```

作为 `write()` 函数第一个参数传递的数组代表其起始地址。第二个参数表示要写入输出文件的内存块的大小。

传递给列表 7.17 中 `write()` 函数的第二个参数评估为 ‘10’（数组的大小）。为此，10 个字节的条被逐字复制到指定文件中。这包括字符串本身（八个字符）、字符串后的分隔符 NULL 字符（所有位都设置为零的单字节）以及末尾的一个带有垃圾值的字节。

如果将 ‘5’ 作为第二个参数传递，则只有字符数组的前五个字节被写入文件。

列表 7.18 展示了如何使用 `write()` 函数将字符数组的值输出到显示器。

## 列表 7.18 使用 `write()` 函数将字符串输出到显示器

```cpp
/*Beginning of writeCharArrConsole.cpp*/

#include<iostream.h>

void main()

{

    char cArr[10] = "abcdefgh";
    cout.write(cArr,strlen(cArr));

}

/*End of writeCharArrConsole.cpp*/
```

# 输出
abdefgh

5. 使用 `write()` 函数向输出流中插入对象：列表 7.19 展示了以二进制模式向输出流插入类对象的方法之一。在这种方法中，类对象占据的内存块中的值被复制到指定的输出文件中。

- 列表 7.19 使用 `write()` 函数将对象输出到磁盘文件

```cpp
/*Beginning of writeObjectDisk.cpp*/

#include<fstream.h>

class A

{

    /*

    definition of class A

    */

};

void main()

{

    ofstream ofile("first.dat");
    ofile.write((char *)&A,sizeof(A));

}

/*End of writeObjectDisk.cpp*/
```

当然，我们注意到注意到类对象占据的内存块中的值被复制到指定的输出文件中。然而，如果对象包含指针，则只有地址会被复制，而不是指针所指向的数据。这导致了当对象被读回另一个程序时出现一个问题：指针将指向一个无效的内存位置。这就是为什么复杂对象应该实现自己的输入和输出函数。

# 列表 7.21 使用 read() 函数从磁盘文件输入字符类型值

```cpp
/*Beginning of readCharDisk.cpp*/

#include<iostream>

#include<fstream>

void main()

{

    ifstream ifile("first.dat");
    char cVar;
    ifile.read(&cVar,sizeof(char));
    cout<<cVar;

}

/*/End of readCharDisk.cpp*/
```

# 输出

x

列表 7.22 展示了如何使用 `read()` 函数通过从键盘读取来输入字符类型变量的值。

# 列表 7.22 使用 read() 函数从键盘输入字符类型值

```cpp
/*Beginning of readCharConsole.cpp*/

#include<iostream>

void main()

{

    char cVar;
    cout << "Enter a character: ";
    cin.read(&cVar,sizeof(char));
    cout<<cVar;

}

/*/End of readCharConsole.cpp*/
```

# 输出

Enter a character: a<enter>

a

显而易见，在文本模式（提取运算符、`get()` 函数）下输入字符类型值与在二进制模式（`read()` 函数）下输入没有区别。在这两种情况下，都不会发生任何转换。

2. 使用 `read()` 函数从输入流中提取整数：列表 7.23 展示了如何使用 `read()` 函数通过从磁盘文件读取将值输入到整数类型变量。

假设磁盘文件 `first.dat` 的前四个字节包含了 64 的二进制等效值。

```
01000000
00000000
00000000
00000000
...
```

# 列表 7.23 使用 read() 函数从磁盘文件输入整数类型值

```cpp
/*Beginning of readIntDisk.cpp*/

#include<iostream.h>

#include<fstream>

void main()

{

    if (isfile("first.dat"))
    {

        int iVar;
        file.read((char*)&iVar,sizeof(iVar));
        cout<<iVar<<endl;
    }
}/*End of readIntDisk.cpp*/
```
