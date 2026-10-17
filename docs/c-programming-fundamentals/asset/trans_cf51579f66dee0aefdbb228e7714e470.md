

## 总结

- 在我们编写的C++程序中创建的文件有助于将数据存储到硬盘上，并保留在系统中以供日后使用。
- 在C++中，为了让用户输入并提供细节或数值，我们使用输入流。*流*指的是一组可以按顺序访问的字节。
- *输入流*用于接收来自用户的输入，例如键盘输入。
- *输出流*用于在显示器、文件或打印机上展示输出。
- 在C++代码中，你需要包含`iostream`头文件，它为程序提供了完整的类层次结构（多重继承），以便使用所有的I/O类。
- `iostream`类可以同时处理输入流和输出流，即使是用户随机按键的情况。
- `fstream`类可以处理与文件打开和关闭相关的输入和输出操作，例如读取。
- 在C++中，打开文件是文件管理的第一步。可以通过在创建对象时将文件名传递给构造函数，或者使用`open()`方法来完成。
- 向文件写入数据是通过`ofstream`或`fstream`类完成的，用于将数据写入已创建或已打开的文件。
- 从文件读取数据是通过`ifstream`或`fstream`类完成的，用于从已创建或已打开的文件中获取数据。
- 关闭文件是文件处理中最后一个重要步骤。
- 程序终止时，内存会自动释放。然而，为了不冒任何可能导致项目泄漏的风险，我们应该始终关闭文件。
- *随机文件访问*意味着默认情况下控制权并非交给文件的开头或结尾，而是文件中的任意位置。这是通过特殊的文件操作实现的，这些操作将文件指针指向我们希望访问的位置。

8. 编写一个C++程序，使用文件处理读取并显示文件。

9. 编写一个C++程序，使用文件处理将两个文件合并到第三个文件中。

10. 编写一个C++程序，使用文件处理对文件进行加密。

11. 编写一个C++程序，使用文件处理对文件进行解密。

12. 编写一个C++程序，使用文件处理通过对象读写值。

13. 编写一个C++程序，使用文件处理统计数字、字母和空格的数量。

14. 编写一个C++程序，使用文件处理统计单词数、行数和总大小。

15. 编写一个C++程序，使用文件处理读取一个文本文件并将其写入另一个文本文件。

16. 编写一个C++程序，使用文件处理统计某个单词出现的次数。

17. 编写一个C++程序，使用文件处理读写学生详细信息。

18. 编写一个C++程序，使用文件处理操作文件指针。

## 选择题

1. 默认情况下，所有文件以__________模式打开。
   - a. 二进制
   - b. 文本
   - c. 无法确定

2. 在`open()`方法中不能组合两种或多种文件打开模式。
   - a. 正确
   - b. 错误

3. 以下哪项不是文件打开模式？
   - a. `ios::ate`
   - b. `ios::nocreate`
   - c. `ios::noreplace`
   - d. `ios::truncate`

4. 由于`ios::trunc`模式，文件会被截断为零长度。
   - a. 正确
   - b. 错误

5. 如果我们有一个`ofstream`类的对象，那么打开文件的默认模式是__________。
   - a. `ios::in`
   - b. `ios::out`
   - c. `ios::in|ios::trunc`
   - d. `ios::out|ios::trunc`

6. __________是`open()`函数的返回类型。
   - a. `int`
   - b. `bool`
   - c. `float`
   - d. `char*`

7. 如果我们有一个`fstream`类的对象，那么打开文件的默认模式是什么？
   - a. `ios::in|ios::out`
   - b. `ios::in|ios::out|ios::trunc`
   - c. `ios::in|ios::trunc`
   - d. 默认模式取决于编译器

8. 要创建输出流，我们必须将流声明为__________类。
   - a. `ofstream`
   - b. `ifstream`
   - c. `iostream`
   - d. 以上都不是

9. 将要同时执行输入和输出操作的流必须声明为__________类。
   - a. `iostream`
   - b. `fstream`
   - c. `stdiostream`
   - d. `Stdiostream`

10. 要执行文件I/O操作，我们必须使用__________头文件。
    - a. `<ifstream>`
    - b. `<ofstream>`
    - c. `<fstream>`
    - d. 以上任意一个

11. 以下哪项不用于定位文件指针？
    - a. `ios::cur`
    - b. `ios::set`
    - c. `ios::end`
    - d. `ios::beg`

12. 以下哪项用于将文件指针移动到文件开头？
    - a. `ios::cur`
    - b. `ios::start`
    - c. `ios::first`
    - d. `ios::beg`

13. 以下哪项不用作文件打开模式？
    - a. `ios::trunc`
    - b. `ios::binary`
    - c. `ios::in`
    - d. `ios::ate`

14. 哪个流类只向文件写入？
    - a. `ofstream`
    - b. `ifstream`
    - c. `fstream`
    - d. `iostream`

15. 关于`eof()`，以下哪个说法是正确的？
    - a. 如果为读取而打开的文件已到达下一个字符，则返回true。
    - b. 如果为读取而打开的文件已到达下一个单词，则返回true。
    - c. 如果为读取而打开的文件已到达末尾，则返回true。
    - d. 如果为读取而打开的文件已到达中间，则返回true。

16. 关于`FILE *fp`，以下哪项是正确的？
    - a. `FILE`是一个结构体，fp是指向`FILE`类型结构体的指针。
    - b. `FILE`是一种缓冲流。
    - c. `FILE`是C++中表示文件的关键字，`fp`是`FILE`类型的变量。
    - d. `FILE`是一种流。

17. 在文件处理中，可以使用以下哪种方法打开文件？
    - a. 使用`open()`
    - b. 构造函数方法
    - c. 析构函数方法
    - d. A和B都可以

18. 哪个运算符用于向文件插入数据？
    - a. `>>`
    - b. `<<`
    - c. <
    - d. 以上都不是

19. 哪个语法是正确的？
    - a. `myfile:open ("example.bin", ios::out);`
    - b. `myfile.open ("example.bin", ios::out);`
    - c. `myfile::open ("example.bin", ios::out);`
    - d. `myfile.open ("example.bin", ios:out);`

20. 这个程序的输出是什么？

    > **注意** *包含所有必需的头文件*

    ```cpp
    using namespace std;
    int main ()
    {
        int l;
        char * b;
        ifstream i;
        i.open ("find.txt", ios::binary);
        i.seekg (0, ios::end);
        l = i.tellg();
        i.seekg (0, ios::beg);
        b = new char [l];
        i.read (b, l);
        i.close();
        cout.write (b, l);
        delete[] b;
        return 0;
    }
    ```

    - a. 错误
    - b. find
    - c. This is find
    - d. 运行时错误

21. 这个程序的输出是什么？

    > **注意** *包含所有必需的头文件*

    ```cpp
    using namespace std;
    int main ()
    {
        char fine, course;
        cout << "Enter a word: ";
        fine = cin.get();
        cin.sync();
        course = cin.get();
        cout << fine << endl;
        cout << course << endl;
        return 0;
    }
    ```

    - a. course
    - b. fine
    - c. 返回“fine”以及从输入的单词中得到的两个字母或数字
    - d. 以上均不是

22. `ios::trunc`有什么用途？
    - a. 如果文件是为输出操作而打开且已存在，则不执行任何操作。
    - b. 如果文件是为输出操作而打开且已存在，则会创建一个新副本。
    - c. 如果文件是为输出操作而打开且已存在，则其先前内容会被删除并由新内容替换。
    - d. 以上都不是

23. 以下程序的输出是什么？

    > **注意** *包含所有必需的头文件*

    ```cpp
    using namespace std;
    int main()
    {
        ofstream ofile;
        ofile.open ("find.txt");
    ```

