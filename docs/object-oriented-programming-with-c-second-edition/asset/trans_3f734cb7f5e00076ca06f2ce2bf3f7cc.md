

## 流处理与文件处理

文件指针可以通过作为流处理类成员提供的某些函数进行显式操作。以下是对这些函数的解释。

### 7.9.1 seekp() 函数

该函数用于显式地将输出指针（put pointer）指向打开文件中的指定位置。需要注意的是，默认情况下，如果是新打开用于写入的文件，输出指针位于文件开头。如果打开已存在的文件进行追加操作，则输出指针默认指向文件末尾。此外，每次写操作都会根据写入的字节数推移输出指针。

`seekp()` 函数定义在 `stream` 类中。它有两个版本：

```cpp
ostream & ostream :: seekp(streampos pos);
ostream & ostream :: seekp(streamoff off,
                               ios::seek_dir dir);
```

在第一个版本中，`seekp()` 函数只接受一个参数——相对于文件开头的绝对位置。`streampos` 类型使用 `long` 作为源数据类型。我们必须记住，位置编号是从零开始的。在这个示例中，输出指针指向文件的第二个字节：

```cpp
ofile.seekp(1); //ofile 是 ostream 类的一个对象
```

在第一个版本中，输出指针的新位置只能相对于文件开头进行指定。但在第二个版本中，`seekp()` 函数接受两个参数——第一个参数是偏移量（offset），第二个参数是打开文件中用于指定该偏移量的参考基准位置。`streamoff` 类型使用 `long` 作为源数据类型。`ios::seek_dir` 类型是一个枚举类型，具有以下值：

```cpp
ios::beg—偏移量从文件开始计算
ios::cur—偏移量从文件中的当前位置计算
ios::end—偏移量从文件末尾计算
```

在接下来的示例中，输出指针指向文件的最后一个字节。我们必须记住 EOF 字符（文件结束符）是文件的最后一个字节。因此，在接下来的示例中，输出指针将指向写入文件中的最后一个字节，即是 EOF 字符的前一个字节。

```cpp
ofile.seekp(-1,ios::end); //ofile 是 fstream
//类的一个对象
```

后面是更多示例：

```cpp
ofile.seekp(0,ios::beg); //将输出指针带到
//文件的开头
of.seekp(2,ios::beg); //将输出指针带到
//文件开头的第三个字节
of.seekp(-2,ios::cur); //将输出指针从其
//文件中的当前位置向左移动
//两个字节
of.seekp(2,ios::cur); //将输出指针带到字节
```

```cpp
//到其文件中的当前
//位置的右侧
//将输出指针带到文件
//末尾（越过
//最后一个字节）
ofile.seekp(0,ios::end);
```

```cpp
ofile.seekp(-1,ios::end);
//将输出指针带到文件的
//最后一个字节
```

现在让我们来理解 `ios::app` 和 `ios::ate` 标志之间的区别。这两者都会以追加模式打开文件，并默认使输出指针指向文件末尾（现有最后一个字节之后）。两者都不会溢出现有文件。它们之间的区别在于：`ios::ate` 允许你重回输出指针并修改文件的现有内容，而 `ios::app` 不允许这样做。换句话说，如果文件使用了 `ios::app` 标志，尝试使用 `seekp()` 函数重回输出指针将失败。输出指针将继续指向文件末尾。正如提到的，随着字节追加到文件中，输出指针会向前移动。因此，如果文件使用了 `ios::app` 标志，就无法重回。

### 7.9.2 tellp() 函数

`tellp()` 返回输出指针的当前位置。它定义在 `ostream` 类中。

```cpp
ostream::tellp();
```

在接下来的示例中，确定了输出指针的当前位置并存储在程序变量中。

```cpp
long pos = ofile.tellp(); //ofile 是 ostream
//类的对象
```

### 7.9.3 seekg() 函数

该函数用于显式地将输入指针（get pointer）指向打开文件中的指定位置。需要注意的是，默认情况下，输入指针指向用于读取的文件开头。每次读操作都会根据字节数向前推移输入指针。
`seekg()` 函数定义在 `istream` 类中。它有两个版本。

```cpp
istream & istream :: seekg(streampos pos);
istream & istream :: seekg(streamoff off,
ios::seek_dir dir);
```

这两个 `seekg()` 函数版本的解释与相应 `seekp()` 函数版本的解释类似。

### 7.9.4 tellg() 函数

`tellg()` 函数与 `tellp()` 函数一样，返回输入指针的当前位置。它定义在 `istream` 类中。

```cpp
istream::tellg();
```

在接下来的示例中，确定了输入指针的当前位置并存储在程序变量中。

```cpp
long pos = ifile.tellg(); //ifile 是 istream
//对象
```

### 7.10 随机访问

在随机访问中，不需要通过顺序遍历记录就可以直接访问文件的中间记录。我们已经学习了随机访问文件所需的工具：`seek()` 和 `seekg()` 函数。
假设我们将整数类型的值输出到文件中并想要直接访问第 n 个记录。可以通过使用从第一个记录开始的循环来实现，循环每次读取后增加计数器，直到计数器指示到 n-1 个记录。更直接的方法是使用 `seekp()` 函数或 `seekg()` 函数，如：

```cpp
ofile.seekg((n-1)*sizeof(int), ios::beg); //ofile 是
                                              fstream
```

该语句导致指针指向第 n 个记录。此时，如果进行操作，第 n 个记录将被修改。注意，该技术仅当记录大小相等时有效。

### 7.12 对象输出成员函数

我们意识到类拥有从外部帮助输出和输入的指针。客户端程序不应承担了解类数据如何组织的责任。

让我们为 `String` 类（到目前为止我们的示例）提供写入数据和从磁盘读取的功能。参见列表 7.27。

#### 列表 7.27 通过成员函数输入输出

```cpp
#include<iostream>
class String
{
  explicit String(const char * p = NULL);
  const char * getString();
  void diskOut(ostream&);
  void diskIn(istream&);
};
```

```cpp
/*
String类的*/
String::String(const char * p)
{
  if(p==NULL) //如果传递了默认值...
    cStr=NULL; //置空
    len=0;
  } else //否则...
    len=strlen(p);
    cStr=new char[len+1]; //动态分配一个//独立的内存块//并拷贝进去
    strcpy(cStr,p);
  }
const char * String::getString()
{
  return cStr;
}
void String::diskOut(ostream& fout)
{
  fout.write((char*)&len, sizeof(int));
  for(int i = 0;i<len;i++)
    fout.put(cStr[i]);
}
void String::diskIn(istream& fin)
{
  String temp;
  fin.read((char*)&temp.len, sizeof(int));
  temp.cStr= new char[temp.len+1];
  int i;
  for(i=0;i<temp.len;i++)
    fin.get(temp.cStr[i]);
  temp.cStr[i]='\0';
  *this = temp;
}
```

