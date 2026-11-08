
对象；严格地将值用于长字符串并不明智。那么你该怎么做？C++17 中新的 string_view 就是解决方案。

string_view（以及相应的 wstring_view 等）是一个指向字符串的只读对象。只要函数和方法是只读的，该类就提供相同的函数和方法。因此，你可以用 begin() 和 end() 进行迭代，用 find() 查找，用 compare() 或 == 进行比较，用 starts_with() 检查开头，以及更多操作——并在算法中使用它们。

但是，你可以进行某些修改。例如，你可以从开头和结尾裁掉一些内容。使用 remove_prefix() 和 remove_suffix()，你可以从前面或后面缩短 string_view 若干个字符。

string_view 需要的资源极少——确切地说，只需要一个指向现有字符串的指针及其长度。最重要的是，绝对不需要堆内存。因此，string_view 特别适合作为函数参数。这里有用的一点是，借助自动类型转换，可以轻松地从字符串生成 string_view。

```cpp
// https://godbolt.org/z/izof7Pcs
#include <iostream>
#include <string>
#include <string_view>
void show_middle(std::string_view msg) {      // string_view is a good parameter
    auto middle = msg.substr(2, msg.size()-4); // substr returns string_view
    std::cout << middle << "\n";
}
int main() {
    using namespace std::literals;
    const std::string aaa = "##Some text##"s;
    show_middle(aaa);                          // conversion to string_view
    auto bbb = "++More text++"sv;              // string_view as literal
    show_middle(bbb);
}
```

**清单 6.2** 可以轻松地从字符串创建 string_view。

使用 show_middle(aaa) 时，编译器会自动将名为 aaa 的字符串转换为 string_view。几乎不可能以更少的资源将字符串作为参数传递。正如你从 msg.substr 中看到的，string_view 也具有与 string 相同的方法。返回值 middle 是一个新的 string_view。

值得注意的是，你可以使用后缀 ""sv 直接将 string_view 生成为字面量。因此，bbb 指向源代码（或编译后程序的静态部分），并且几乎不占用自身的内存。

有时也可以将 `string_view` 用作返回值。然而，正如指针和引用一样，你必须确保 `string_view` 所基于的原始字符串仍然存在。

## 6.2 流

你已经在示例中多次看到流，但很少出现它们的类型，因为我们使用了标准库预定义的流：

- 类型为 `std::ostream` 的 `std::cout` 用于*标准输出*，通常输出到控制台——也就是屏幕。或者你可以将输出重定向到文件。
- 类型为 `std::istream` 的 `std::cin` 用于*标准输入*，通常来自键盘或重定向的文件。
- `std::cerr` 和 `std::clog` 也是类型为 `std::ostream` 的输出数据流，通常最终显示在屏幕上，但你可以将它们与 `std::cout` 分开重定向到文件。

对于正常程序流程的输入和输出，你通常使用 `std::cin` 和 `std::cout`。每次输出都要花费时间，而且调用有开销，因此 `std::cout` 是带缓冲的：输出有时不会立即出现，而是先被收集起来。

`std::cerr` 则不是这样，它的输出应当立即出现。请将此流用于错误输出。如果 `std::cout` 已被重定向到文件，此输出仍会显示在控制台上，如[清单 6.3](#listing-63)所示。

```cpp
// https://godbolt.org/z/P1fn5q8z8
// Call this program with "prog.exe > file.txt", for example.
#include <iostream>  // cout, cerr
int main() {
    std::cout << "Output to cout\n";       // is output after file.txt
    std::cerr << "Error message!\n";       // still appears on the console
    std::cout << "Normal output again\n";  // back into the file
}
```

**清单 6.3** 错误流与标准输出分离。

### 6.2.1 输入和输出运算符

如你经常看到的，你可以使用 `<<` 运算符将数据输出到 `cout`。所有内置数据类型都可以用这种方式输出。你不必担心格式——但也可以自行控制格式，稍后你会看到 *操纵符* 的用法。这一点值得提及，因为与 C 函数 `printf()` 中不同，编译器会为你选择正确的格式——即全局 `operator<<` 的正确重载。你也可以为自己的数据类型添加重载（见第 12 章第 12.11 节）。

你可以连续串联多个 `<<` 调用；只需先写出输出流。每个 `<<` 调用都会将流作为结果返回，以便它可以再次接收输出。

通过 `>>` 进行输入也是如此：内置数据类型总是读取到下一个空白字符（例如空格或换行）为止。

让我们用一些额外的输入和输出来扩展清单 6.1。

```cpp
// https://godbolt.org/z/xYvPxbjr5
#include <iostream>                 // cin, cout for input and output
#include <string>
#include <array>
using std::cin; using std::cout;     // abbreviations cin and cout
void input(
    std::string &name,
    unsigned &birthDay,
    unsigned &birthMonth,
    unsigned &birthYear,
    long long &socialSecurity,
    std::array<int,12> &monthIncomes)  // array is a container
{
    /* input still without good error handling... */
    cout << "Name: ";
    std::getline(cin, name);          // getline takes input stream and string
    if(name.length() == 0) {
        cout << "You have entered an empty name.\n";
        exit(1);
    }
    cout << "birth day: "; cin >> birthDay;
    cout << "birth month: "; cin >> birthMonth;
    cout << "birth year: "; cin >> birthYear;
    cout << "social security: "; cin >> socialSecurity;
    for(int m=0; m<12; ++m) {
        cout << "income month " << m+1 << ": "; // multiple outputs
        cin >> monthIncomes[m];                      // read in with operator
    }
    cout << std::endl;
}
int main() {
    std::string name{};
    unsigned day = 0;
    unsigned month = 0;
    unsigned year = 0;
    long long ssid = 0;
    std::array<int,12> incomes{};
    input(name, day, month, year, ssid, incomes);
    // ... calculations ...
}
```

**清单 6.4** 一个带输入和输出的函数。

在这里，你可以看到通过 `std::cout <<...` 进行的大量输出。无论它是像 “Birthday: ” 这样的字符串，还是像 `m+1` 这样的数字，你始终只需使用 `<<`。通过 `cout << "income month "...`，你还可以看到多个输出如何串联在一起。

从键盘输入同样简单：`>>` 运算符后面跟上你想读入的变量，就允许用户输入一个值。不过这里需要稍加注意：输入项应始终通过按 **Enter** 键来完成。对于内置数据类型，下一个空白字符——例如 **Space** 或 **Enter**——会结束该变量的输入。如果用户输入中出现空格，那么其后的所有内容都会被保留下来，供下一次通过 `>>` 的操作使用，于是所有内容都会乱套。

### 6.2.2 “getline”

这也是为什么在 `std::getline(cin, name);` 中，我不对 name 使用 `>>`，而是改用 `getline()`。此函数不仅读取到下一个空白字符，而且读取到下一个行尾——因此也允许名字中包含空格。

### 6.2.3 用于输入和输出的文件

当你调用程序时，可以使用 `>` file 将 cout“重定向”到文件。以下程序将参数转换为大写并输出它们：

```cpp
// https://godbolt.org/z/a6qqbWKMs
#include <cstdlib>
#include <iostream>

int main(int argc, char* argv[]) {
    for(int i=1; i<argc; ++i) {              // start at 1
        for(char* p=argv[i]; *p!='\0'; ++p) {
            char c = toupper(*p);
            std::cout << c;
        }
        std::cout << ' ';
    }
    std::cout << '\n';
}
```

带 `i` 的循环遍历你传给程序的所有参数，带 `p` 的循环遍历各个参数的所有字符。每个参数都以 `\0` 结束。这个
