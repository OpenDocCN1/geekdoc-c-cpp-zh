
```cpp
#include <fstream.h>
using namespace std;
void main()
{
  ofstream outfile("EXAMPLE.txt");
  int i = 0;
  while (i != 999)
  {
    cout<<"Please input an integer:";
    cin>>i;
    outfile.write((char *) &i, sizeof(i));
  }
}
```

在前面的代码片段中，类型转换是必要的，因为 read() 和 write() 函数的语法如下：

```cpp
write(char * addr, int size);
read(char * addr, int size);
```

前面的语法意味着编译器假定缓冲区是字符类型。因此，对象的地址应强制转换为字符指针。现在，考虑以下程序。

```cpp
#include <fstream>
using namespace std;
int main ()
{
  char * buffer;
  long size;
  ifstream infile ("EXAMPLE.txt",ifstream::binary);
  ofstream outfile ("new.txt",ofstream::binary);

  // get size of file
  infile.seekg(0,ifstream::end);
  size=infile.tellg();
  infile.seekg(0);

  // allocate memory for file content
  buffer = new char [size];

  // read content of infile
  infile.read (buffer,size);

  // write to outfile
  outfile.write (buffer,size);

  // release dynamically-allocated memory
  delete[] buffer;
  outfile.close();
  infile.close();
  return 0;
}
```

> **注意**
>
> *当操作的不是定义为字符数组的缓冲区时，调用 read() 和 write() 内部的类型转换是必需的。由于 C++ 的强类型检查，一种类型的指针不能自动转换为另一种类型的指针。*

接下来，我们学习显式打开和关闭文件。

## 显式打开和关闭文件

显式地，可以使用 **open()** 和 **close()** 函数打开文件。这两个函数的用法可以通过以下代码来说明：

```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main ()
{
   ofstream file1;
   file1.open ("SAMPLE.txt");
   file1<<"Example of open and close function.\n";
   file1.close();
   return 0;
}
```

前面的代码创建一个名为 SAMPLE.txt 的文件，并向该文件写入一句话。

要打开一个具有流对象的文件，我们需要按如下方式使用 open() 函数：

```
open (filename, mode);
```

在前面的语法中，filename 是 **const char *** 类型的以空字符结尾的字符序列，表示要打开的文件的名称；mode 是一个可选参数，由以下标志组合而成：

| 标志 | 描述 |
|---|---|
| ios::in | 用于为输入操作而打开的流。 |
| ios::out | 用于为输出操作而打开的流。 |
| ios::binary | 用于以二进制模式打开的流。 |
| ios::app | 用于以仅输出方式打开的流。所有输出操作都在文件末尾执行，将内容追加到文件的当前内容之后。 |
| ios::ate | 用于将初始位置设置在文件末尾。如果未将此标志设置为任何值，则初始位置为文件开头。 |
| ios::trunc | 如果文件以输出操作方式打开且文件已存在，则用于删除文件内容并用新内容替换。 |

每个流都包含一系列与其操作符相关联的位或标志。这些位定义在 **ios** 类中。其中一些位用于格式化输入和输出，而另一些用于错误处理。借助继承，这些位在 **fstream** 类中可用。其中一些位也与文件的打开操作相关。每个流都关联一系列称为打开模式位的位。这些打开模式位表示文件打开时所采用的模式。总体而言，这些位说明了文件将要打开的模式。例如，考虑以下语句：

```cpp
fstream file("IOFILE",ios::in|ios::out);
```

当程序遇到前面的语句时，会为该流设置语句中的两个位。因此，该文件可用于输入和输出。表15.1列出了打开模式及其说明：

表15.1：打开模式

| 模式 | 说明 |
|---|---|
| app | 所有写出的数据都会追加到流中。 |
| ate | 文件指针从流的末尾开始，也就是说，它使文件定位到末尾。I/O 操作仍可在文件中的任意位置进行。 |
| in | 流以输入方式打开。 |
| out | 流以输出方式打开。 |
| binary | 二进制文件；如果不存在，则默认以美国信息交换标准代码（ASCII）文件打开。 |
| trunc | 如果文件存在，则在写入或读取之前将其截断并擦除所有数据。 |
| nocreate | 如果要打开的文件尚不存在，则操作失败。 |
| noreplace | 如果文件已存在，则以输出方式打开时操作失败，除非设置了 app 或 ate 模式。 |

在下一节中，我们将详细讨论磁盘 I/O。

### 使用成员函数进行磁盘 I/O

让我们借助一个示例 C++ 程序来理解这个概念。考虑如下定义的 Medicine 类：

```cpp
class Medicine
{
    private:
        char MedicineCode[5];
        unsigned int BatchNo;
        char Category;
        char units;
        float producedQty;

    public:
        void getdata()
        {
            cout<< "Enter the BatchNo:";
            cin>> BatchNo;
            cout<< "Enter the Medicine Code:";
            cin>> MedicineCode;
            cout<< "Enter Category:";
            cin>> Category;
            cout<< "Enter the unit of measurement:";
            cin>> units;
            cout<< "Enter the quantity produced:";
            cin>> producedQty;
        }
        void showdata()
        {
            cout<< "Displaying the desired Data:";
            cout<< "The Batch Number is:" << BatchNo;
            cout<< "The Medicine Code is:" << MedicineCode;
            cout<< "The Category is:" << Category;
            cout<< "the unit of measurement is:" << units;
            cout<< "The quantity produced is:" << producedQty;
        }
};
```

前面代码片段的目的是将磁盘 I/O 操作纳入类定义中。然而，可以看出，如果我们在类中包含 I/O 操作，可能会在一定程度上损害类的可重用性，因为该类将与磁盘文件相关联。为了保留可变的磁盘文件名，我们可以将文件名作为类的一个属性包含进来。然而，在这种情况下，文件名并不是 Medicine 类的属性。此外，如果我们想重用 Medicine 类来创建 Medicine 列表，则无法这样做，因为文件 I/O 不是通用 Medicine 类的属性。现在，考虑 Medicine_File 类的代码：

```cpp
class Medicine_File
{
   private:
      Medicine buffer;
   public:
      void diskout(void);
      void diskin(void);
};
```

为了将文件 I/O 与通用 Medicine 类分离，我们声明了一个名为 **Medicine_File** 的单独类，该类会生成一个与此类关联的名为 MEDICINE.TXT 的输出文件。这个类唯一的属性是一个名为 buffer 的 Medicine 类型包含对象；可以先将值写入其中，然后刷新到磁盘文件，或者从文件读取一个对象到该对象中。这个类还包含两个公共函数：一个用于将记录写入文件，另一个用于从文件读取记录。该类的成员函数如下：

- **diskout()**——从用户处获取数据并将记录写入文件
- **diskin()**——从文件读取记录并将其显示在屏幕上

现在，考虑以下代码：

```cpp
void Medicine_File::diskout(void)
{
   ofstream ofile("MEDICINE.TXT", ios::app);
   char loop;
   do
   {
      buffer.getdata();
      ofile.write((char *) &buffer, sizeof(buffer));
      cout<<"Any more records (y/N)?";
      cin>>loop;
   } while (loop == 'y');
}
void Medicine_File::diskin(void)
{
   ifstream ifile("MEDICINE.TXT");
   ifile.read((char *) &buffer, sizeof(buffer));
   while (ifile)
   {
      buffer.showdata();
      ifile.read((char *) &buffer, sizeof(buffer));
   }
}
```

我们有一个名为 Medicine_File 的用于文件 I/O 的自包含类；因此，我们可以用非常简单的方式实现 main() 函数，如下所示：

```cpp
void main()
{
   Medicine_File fileobj;
   fileobj.diskout();
   fileobj.diskin();
}
```
