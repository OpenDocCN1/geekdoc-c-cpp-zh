
```cpp
#include <cstdlib>

#include <string>

using namespace std;

int main()

{

    int ch, key_ch;

    string fname;

    cout << "Enter input file: ";

    cin >> fname;

    ifstream fin(fname.c_str());

    if(fin.is_open() == false) {

        cout << "Error: Input file can't be loaded\n";

        exit(EXIT_FAILURE);

    }

    cout << "Enter output file: ";

    cin >> fname;

    ofstream fout(fname.c_str());

    if(fout.is_open() == false) {

        fin.close();

        cout << "Error: Output file can't be created\n";

        exit(EXIT_FAILURE);

    }

    cin.get();

    cout << "Enter key char: ";

    key_ch = cin.get();

    while (1)

    {

        ch = fin.get();

        if(!fin)

            break;

        fout << (char) (ch ^ key_ch);

    }

    fin.close();

    fout.close();

    return 0;

}
```

### C24.7 定义类 Country，包含私有成员：名称、首都和人口。假设 country.txt 文件的每行都包含相应国家的数据，格式如下：

name capital population

编写一个程序，读取文件并使用该类将国家数据存储在 `Country` 元素的 `vector` 中。程序应该读取一个数字并显示人口高于该数字的国家数据。在类中添加任何你函数。

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
#include <vector>
using namespace std;

class Country {
private:
    string name;
    string capital;
    int pop;
public:
    Country(const string& n = "", const string& c = "", int p = 0) : name(n), capital(c), pop(p) {}
    void set(const string& n, const string& c, int p);
    int get_pop() const { return pop; }
    void show() const;
};

void Country::set(const string& n, const string& c, int p) {
    name = n;
    capital = c;
    pop = p;
}

void Country::show() const {
    cout << name << '\t' << capital << '\t' << pop << '\n';
}

int main() {
    int i, pop;
    string name, capital;
    Country tmp;
    vector<Country> cntr;
    ifstream fin("country.txt");
    if(fin.is_open() == false) {
        cout << "Error: is_open() failed\n";
        exit(EXIT_FAILURE);
    }
    while (1) {
        if(!fin >> name >> capital >> pop) {
            break;
        }
        tmp.set(name, capital, pop);
        cntr.push_back(tmp);
    }
    cout << "Enter population: ";
    cin >> pop;
    for(i = 0; i < cntr.size(); i++)
        if(cntr[i].get_pop() >= pop)
            cntr[i].show();
    fin.close();
    return 0;
}
```

# 从二进制文件写入和读取数据

用于向二进制文件写入和从其读取数据的函数分别是 `write()` 和 `read()`。虽然它们主要用于二进制文件，但在谨慎的情况下，也可以用于文本文件。

# `write()` 函数

`write()` 函数对于一次性写入大块数据非常有用。它的原型定义为：

```cpp
ostream& write(const char *buf, streamsize count);
```

参数 `buf` 指向持有要写入文件数据的内存。`streamsize` 是某些整数类型的别名。`count` 参数指定要写入文件的字节数。例如，为了存储一个包含 1000 个整数的数组，我们这样写道：

```cpp
int arr[1000];
ofstream fout("test.dat", ios_base::out | ios_base::trunc | ios_base::binary);
fout.write((char*)arr, sizeof(arr));
```

要存储一个 `double` 数字数字，我们写入：

```cpp
double d = 1.2345;
fout.write((char*)&d, sizeof(double));
```

要存储 `Student` 类的对象，我们写入：

```cpp
Student s;
fout.write((char*)&s, sizeof(s));
```

注意，只有对象的数据被写入文件，而不是函数。如示例所示，我们应该将地址转换为 `char*`。最佳实践是使用 `sizeof` 运算符来指定大小，以使你的程序具有平台无关性。如果我们想验证没有发生错误，可以检查流的状态。例如：

```cpp
if(!fout)
    cout << "write error\n";
```

# `read()` 函数

与 `write()` 类似，`read()` 对于一次性读取大块数据非常有用。它的原型定义为：

```cpp
istream& read(char *buf, streamsize count);
```

参数 `buf` 指向存储读取数据的内存。`count` 参数指定从文件中读取多少字节。

> 因为两个系统之间存在差异（例如，类型的大小），因此无法保证使用 `write()` 函数写入的文件在另一个系统中通过 `read()` 函数正确读取。

在接下来的示例中，一个 `double` 数字被读取并存储在 `d` 中：

```cpp
double d;
ifstream fin("test.dat", ios_base::in | ios_base::binary);
fin.read((char*)&d, sizeof(d));
```

在下一个示例中，1000 个整数被读取并存储在 `arr` 中：

```cpp
int arr[1000];
fin.read((char*)arr, sizeof(arr));
```

> 使用二进制文件而非文本文件使用 `write()` 和 `read()` 更安全，因为换行符的潜在转换可能会导致意外的结果。

例如，假设我们使用 `write()` 在文本文件中写入一个 50 个字符的字符串，并将 `count` 的值为 50。如果程序在 Windows 上运行且字符串包含换行字符，则与 `\r\n` 对的替换将使其大小超过 50；因此，`write()` 不写入整个字符串。

正如我们在接下来的示例中看到的，`write()` 和 `read()` 经常用于占用相同内存的对象。正如我们所说的，当我们将对象存储在文件中时，只存储数据成员。然而，对于使用虚函数的类要小心。（注：此处原文似乎存在大量重复的错误文本，翻译已按逻辑处理）

## 练习题

- **24.8** 编写一个程序，声明一个 10 个整数的数组并将其写入用户选择的二进制文件中。然后，程序应该读取文件并显示。
- **22..** 编写一个程序，读取标题的大小，将其写入用户选择的二进制文件中。然后，程序应该读取文件并显示内容。
- **24.9** 编写一个程序，读取标题的大小，然后将其写入用户选择的二进制文件中。然后，程序应该读取文件并显示它是否包含。

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
#include <cstring>
using namespace std;

int main()
{
    bool found;
    int i, len;
    char title[100], str[100];
    string fname;
    cout << "Enter file name: ";
    cin >> fname;
    fstream fstr(fname.c_str(), ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    if(fstr.is_open() == false) {
        cout << "Error: is_open() failed\n";
        exit(EXIT_FAILURE);
    }
    cin.get();
    for(i = 0; i < 10; i++)
    {
        cout << "Enter title: ";
        cin.getline(title, sizeof(title));
        len = strlen(title);
        fstr.write((char*)&len, sizeof(int));
        fstr.write(title, len);
    }
    cout << "Enter title to search: ";
    cin.getline(str, sizeof(str));
    found = 0;
    fstr.seekg(0);
    while (1)
    {
        if (!fstr.read((char*)&len, sizeof(int)))
            break;
        fstr.read(title, len);
        if (!fstr)
        {
            break;
        }
        title[len] = '\0';
        if(strcmp(title, str) == 0)
        {
            found = 1;
            break;
        }
    }
    if(found == 0)
        cout << "\nTitle not found\n";
    else
        cout << "\nTitle found\n";
    fstr.close();
    return 0;
}
```

24 Files 797

C.24 假设 `test.bin` 二进制文件包含学生的成绩。成绩数量在文件开头声明。编写一个程序从二进制文件读取成绩（使用 `float` 类型）并存储在动态分配的内存中。然后，程序应该读取一个数字并显示大于该数字的成绩。

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
using namespace std;
```

# 798 C++ 简介

```cpp
int main() {
    int i, grd_num;
    float *grd_num, grd;
    ifstream fin("test.bin", ios_base::in | ios_base::binary);
    if(fin.is_open() == false) {
        cout << "Error: is_open() failed\n";
        exit(EXIT_FAILURE);
    }
    fin.read((char*)&grd_num, sizeof(int));
    if(!fin) {
        fin.close();
        cout << "Error: read() failed\n";
        exit(EXIT_FAILURE);
    }
    grd_arr = new float[grd_num]; /* 分配内存存储成绩。 */
    fin.read((char*)grd_arr, grd_num * sizeof(float)); /* 读取所有成绩并检查是否读取成功。 */
    if(fin) {
        cout << "Enter grade: ";
        cin >> grd;
        for(i = 0; i < grd_num; i++)
            if(grd_arr[i] > grd)
                cout << grd_arr[i] << '\n';
    }
    else {
        cout << "Error: read(0) failed to read grades\n";
    }
    delete[] grd_arr;
    fin.close();
    return 0;
}
```

**C.24.11** 杀毒软件识别病毒的一种常用方法是基于特征的检测。特征是一段字节序列（例如 F3 BA 20 63 7A 1B），用于识别特定的病毒。当对文件进行扫描时，杀毒软件会在文件中搜索用于标识病毒存在的特征码。编写一个程序，读取病毒特征码（例如五个整数），并检查它是否包含在二进制文件 test.dat 中。

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
#include <cstring>
using namespace std;

int main() {
    const int SIZE = 5;
    bool found;
    int i, len, back, buf[SIZE], sign[SIZE];
    ifstream fin("test.dat", ios_base::in | ios_base::binary);
    if(fin.is_open() == false)
    {
        cout << "Error: is_open failed\n";
        exit(EXIT_FAILURE);
    }
    cout << "Enter virus signature " << SIZE << " integers\n";
    for(i = 0; i < SIZE; i++)
    {
        cout << "Enter number: ";
        cin >> sign[i];
    }
    len = sizeof(sign);
    found = 0;
    back = len - sizeof(int);
    while (1) {
        fin.read((char*)buf, SIZE * sizeof(int));
        if(!fin) {
            break;
        }
        if(memcmp(buf, sign, len) == 0) { 
            found = 1;
            break;
        } else {
            fin.seekg(-back, ios_base::cur); /* 回到此处检查下一组五个。 */
        }
    }
    if(found == 1)
        cout << "SOS: Virus found\n";
    else
        cout << "That virus signature isn't found\n";
    fin.close();
    return 0;
}
```
