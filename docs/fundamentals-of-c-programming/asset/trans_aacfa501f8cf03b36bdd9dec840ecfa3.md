

```cpp
/*
 * save_vector(filename, v)
 * Writes the contents of vector v.
 * filename is name of text file created.  Any file
 * by that name is overwritten.
 * v is a vector holding integers.  v is unchanged by the
 * function.
 */
void save_vector(const std::string& filename, const std::vector<int>& vec) {
    // Open a text file for writing
    std::ofstream out(filename);
    if (out.good()) {    // Make sure the file was opened properly
        int n = vec.size();
        for (int i = 0; i < n; i++)
            out << vec[i] << " ";  // Space delimited
        out << '\n';
    }
    else
        std::cout << "Unable to save the file\n";
}

/*
 * load_vector(filename, v)
 * Reads the contents of vector v from text file
 * filename.  v's contents are replaced by the file's
 * contents.  If the file cannot be found, the vector v
 * is empty.
 * v is a vector holding integers.
 */
void load_vector(const std::string& filename, std::vector<int>& vec) {
    // Open a text file for reading
    std::ifstream in(filename);
    if (in.good()) {    // Make sure the file was opened properly
        vec.clear();    // Start with empty vector
        int value;
        while (in >> value)    // Read until end of file
            vec.push_back(value);
    }
    else
        std::cout << "Unable to load in the file\n";
}

int main() {
    std::vector<int> list;
    bool done = false;
    char command;
    while (!done) {
        std::cout << "I)nsert <item> P)rint "
                  << "S)ave <filename> L)oad <filename> "
                  << "E)rase Q)uit: ";
        std::cin >> command;
        int value;
        std::string filename;
        switch (command) {
        case 'I':
        case 'i':
            std::cin >> value;
            list.push_back(value);
            break;
        case 'P':
        case 'p':
            print_vector(list);
            break;
        case 'S':
        case 's':
            std::cin >> filename;
            save_vector(filename, list);
            break;
        case 'L':
        case 'l':
            std::cin >> filename;
            load_vector(filename, list);
            break;
        case 'E':
        case 'e':
            list.clear();
            break;
        case 'Q':
        case 'q':
            done = true;
            break;
        }
    }
}
```

清单 13.6 (numberlist.cpp) 是命令驱动的，带有菜单，当用户键入 S data1.txt 时，程序将向量的当前内容保存到名为 data1.txt 的文件中。用户可以擦除向量的内容：

```
I)nsert <item> P)rint S)ave <filename> L)oad <filename> E)rase Q)uit: E
```

然后可以使用加载命令恢复内容：

```
I)nsert <item> P)rint S)ave <filename> L)oad <filename> E)rase Q)uit: L data1.txt
```

用户也可以退出程序，稍后重新运行程序并加载先前保存的数字列表。用户可以使用不同的文件名将不同的数字列表保存到不同的文件中。

请注意，在 save_vector 和 load_vector 函数中，我们将 std::string 参数作为 const 引用传递。我们这样做的原因与对 std::vector 对象所做的相同（参见第 11.14 节）——这种技术避免了为传递给函数而复制字符串。这些函数可以通过引用“看到”调用者的实际字符串，而不是使用字符串对象的副本。const 说明符防止函数修改传递的字符串。复制字符串需要时间（尤其是长字符串），副本还会占用额外内存。在这种情况下，复制确实没有必要，因此按 const 引用传递是理想的方法。

std::ofstream 对象将数据写入文件。语句

```cpp
std::ofstream out(filename);
```

将名为 out 的对象与名为 filename 的文本文件关联。这在声明点处打开文件。我们也可以将文件流对象的声明与打开分开，如

```cpp
std::ofstream out;
out.open(filename);
```

清单 13.6 (numberlist.cpp) 中的 save_vector 函数传递一个 std::string 对象来打开文件，但文件名也可以是字符串字面量（带引号的字符串）。请考虑以下代码片段：

```cpp
std::ofstream fout("myfile.dat");
int x = 10;
if (fout.good()) // Make sure the file was opened properly
    fout << "x = " << x << '\n';
else
    std::cout << "Unable to write to the file \"myfile.dat\"\n";
```

打开文件后，程序员应通过调用文件流对象的 good 方法来验证该方法是否正确打开了文件。输出文件流可能因各种原因失败，包括磁盘已满或没有足够的权限在给定文件夹中创建文件。

一旦关联的文件打开，我们就可以像使用 std::cout 输出流对象一样使用 std::ofstream 对象，只不过数据被记录在文本文件中，而不是打印到屏幕上。与 std::cout 一样，你可以使用 << 运算符并向 std::ofstream 对象发送流操纵符，如 std::setw。std::cout 对象和 std::ofstream 类的对象属于同一类家族，并通过称为继承的概念相关联。我们将在第 17 章更详细地探讨继承。就目前的目的而言，这种关系意味着我们可以用 std::cout 对象做的任何事情，都可以用 std::ofstream 对象做。当然，区别在于，std::cout 的效果出现在控制台窗口中，而 std::ofstream 对象的效果被写入文本文件。

执行中的程序将所有数据写入文件后，当 std::ofstream 对象超出作用域时，文件对象会自动关闭文件，确保程序写入文件的所有数据都已完全保存到磁盘。std::ofstream 类还提供 close 方法，允许程序员手动关闭文件。当使用同一文件对象重新创建同一文件时，这有时很有用，如清单 13.7 (endltest.cpp) 所示。

在清单 13.6 (numberlist.cpp) 中，std::ifstream 对象从文件读取数据。语句

```cpp
std::ifstream in(filename);
```

将名为 in 的对象与名为 filename 的文本文件关联。这在声明点处打开文件。我们也可以将文件流对象的声明与打开分开，如

```cpp
std::ifstream in;
in.open(filename);
```

与 std::ofstream 对象一样，filename 是标识要读取的文件的字符串文件名。

打开文件后，程序应调用 good 以确保文件已成功打开。输入流对象通常无法正确打开，是因为文件不存在；可能是文件名拼写错误，或者文件路径不正确。输入流也可能因权限不足或磁盘上的坏扇区而失败。

一旦打开关联的文件，输入文件流对象的行为就像 std::cin 对象一样，只不过其数据来自文本文件而不是键盘。这意味着熟悉的 >> 运算符和 getline 函数与 std::ifstream 对象完全兼容。std::cin 对象和 std::ifstream 对象通过继承相关联，其方式类似于 std::cout 对象和 std::ofstream 对象的关联方式。

与输出流对象一样，std::ifstream 对象在超出作用域时会自动关闭其关联的文件。

输入和输出流使用一种称为缓冲的技术。缓冲依赖于两个事实：

- 将数据写入内存比写入磁盘更快。
- 将 n 个字节的数据一次性写入磁盘，比使用 n 次操作一次写入一个字节来写入 n 个字节的数据更快。

缓冲区是内存中用于保存待写入磁盘数据的特殊位置。程序写入缓冲区的速度比直接写入磁盘快得多。当缓冲区满时，程序（通过操作系统）可以将缓冲区的完整内容写入磁盘。

要理解缓冲的概念，请考虑用砖块砌墙的任务。估计表明，这堵墙大约需要 1,350 块砖。一旦我们准备好开始砌墙，就可以开车去建材商店购买一块砖。然后我们可以开车到工地，根据需要用砂浆将砖块放置在合适的位置。现在我们准备好放置下一块砖，因此必须开车回商店取下一块砖。然后我们开车回工地，安放砖块。我们重复这个过程大约 1,350 次。

如果这看起来非常低效，那确实如此。更好的做法是第一次行程尽可能多地将砖块装入车辆，然后根据需要再次前往商店获取更多砖块，直到墙壁完成。

在这个类比中，运输车辆就是缓冲区。输出流对象使用内存中称为缓冲区的特殊位置。就像用于运输砖块的车辆一样，内存缓冲区具有固定容量。程序写入缓冲区的速度比直接写入磁盘快得多。<< 运算符将要保存的各个值写入缓冲区，当缓冲区满时，输出流会以一次请求向操作系统发送缓冲区中的所有数据到磁盘。与砖块一样，这比一次只向显示器发送一个字符更高效。这种缓冲过程可以显著加快程序的输入和输出操作。

std::ofstream 对象将所有数据写入其缓冲区并在其生命周期结束后，即使缓冲区未满，也会将缓冲区中剩余的数据刷新到磁盘。缓冲区大小固定，因此数据的最后部分可能无法完全填满缓冲区。这类似于砌墙所需的最后一批砖块，可能无法构成满载。即使车辆未完全装载，我们仍需将这些剩余砖块运送到几乎完工的墙上。

在某些情况下，有必要确保在缓冲区满之前和完全关闭文件之前刷新缓冲区。对于任何写入文本的输出流对象，我们可以使用 std::endl 流对象在不关闭文件的情况下刷新缓冲区。我们在第 3.1 节简要提及了 std::endl。我们可以将 std::endl 与 '\n' 互换使用，以表示控制台打印中的换行。由于缓冲为文件输入和输出提供了性能优势，因此 std::endl 和 '\n' 的选择会对文件处理产生很大影响。清单 13.7 (endltest.cpp) 比较了 std::endl 和 '\n' 在各种情况下的性能。

```cpp
Listing 13.7: endltest.cpp
#include <iostream>
#include <fstream>
#include <ctime>
```

