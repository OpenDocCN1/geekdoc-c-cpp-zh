

## 13.2. 输入/输出流

```cpp
cin.clear();
```

重置你输入的流对象，那些无法赋值给给定变量的输入将留在键盘缓冲区输入中。

-   用户输入的字符可以被其纳，因此流对象不会移除剩余的按键值。清除流对象不会移除剩余的按键值。如果用户在不清除之前输入的错误字符的情况下进行重试，将导致相同的问题——流对象将重新进入错误状态，且错误字符仍留在键盘缓冲区中。解决方案是通过清除键盘缓冲区中自用户输入有效数据以来的所有字符来修复此问题。

```cpp
cin.ignore(numeric_limits<streamsize>::max(), '\n');
```

从缓冲区中删除所有字符，包括换行符 '\n' 在内的所有字符。

```cpp
numeric_limits<streamsize>::max()
```

返回缓冲区可以容纳的最大字符数，因此 ignore 方法会丢弃所有字符，直到读取换行符 '\n' 或到达缓冲区末尾（以先者为准）。

一旦流对象从错误状态被重置且键盘缓冲区为空，用户输入就可以像往常一样进行。

ostream 和 istream 还有许多其他方法，但我们在这里不考虑它们。

iostream 在从用户获取输入时使用空白字符（空格和制表符）作为分隔符。这意味着如果你的行包含嵌入的空格，你无法使用操作符>> 从键盘赋值一行文本。列表 13.4 (faultyreadline.cpp) 说明了这一点。

列表 13.4: faultyreadline.cpp

```cpp
#include <iostream>
#include <string>

using namespace std;

int main() {
    string line;
    cout << "Please enter a line of text: ";
    cin >> line;
    cout << "You entered: " << line << endl;
}
```

列表 13.4 (faultyreadline.cpp) 的示例运行显示：

```
Please enter a line of text: Mary had a little lamb.
You entered: "Mary"
```

如你所见，列表 13.4 (faultyreadline.cpp) 并没有将整行文本赋值给字符串 line。文本在输入中的第一个空格处被截断。

为了从键盘读取整行文本（包括可能存在的任何嵌入空格），请使用全局 getline 函数。如列表 13.5 (readline.cpp) 所示，getline 函数接受一个 istream 对象和一个用于赋值的 string 对象。

| 列表 13.5: readline.cpp |
| :--- |
| #include <iostream> |
| #include <string> |
| using namespace std; |
| int main() { |
| string line; |
| cout << "Please enter a line of text: "; |
| getline(cin, line); |
| cout << "You entered: " << line << endl; |
| } |

列表 13.5 (readline.cpp) 的示例运行产生：

## 13.3 文件流

许多应用程序允许用户创建和操作数据。真正实用的应用程序允许用户存储数据：例如，文字处理器可以保存和加载文档。

如果 vector 具有持久性，将会更有用。当数据在程序执行之间存在时，它就是持久的。在特定程序的某次执行期间，用户可以创建并填充 vector。用户将 vector 的内容保存到磁盘并退出程序。之后，用户可以运行程序从磁盘重新加载并恢复 vector。

C++ fstream 对象允许程序员在应用程序中构建持久性。列表 13.6 (numberlist.cpp) 是一个简单的程序示例，允许用户将 vector 的内容保存到文本文件并从文本文件中加载 vector。

| 列表 13.6: numberlist.cpp |
| :--- |
| // File_io.cpp |
| #include <iostream> |
| #include <fstream> |
| #include <string> |
| #include <vector> |
| using namespace std; |
| /* |
| # print_vector(v) |
| # 打印 vector v 的内容。 |
| */

## 13.3 文件流

```cpp
/* v 是一个持有整数的 vector。
 */
void print_vector(const vector<int>& vec) {
    cout << "[";
    int len = vec.size();
    if (len > 0) {
        for (int i = 0; i < len - 1; i++) {
            cout << vec[i] << ", "; // 元素间的逗号
        }
        cout << vec[len - 1]; // 最后一个元素后无逗号
    }
    cout << "]" << endl;
}
```

```cpp
/* save_vector(filename, v)
* 写入 vector v 的内容。
* filename 是创建的文本文件名。任何同名文件都会覆盖。
* v 是一个持有整数的 vector。函数不会改变 v。
 */
void save_vector(const string& filename, const vector<int>& vec) {
    ofstream out;
    out.open(filename);
    if (out.good()) { // 确保文件已正确打开
        int n = vec.size();
        for (int i = 0; i < n; i++) {
            out << vec[i] << " "; // 空格分隔
        }
        out << endl;
        out.close();
    } else
        cout << "Unable to save the file" << endl;
}
```

```cpp
/* load_vector(filename, v)
* 从文本文件读取 vector v 的内容。
* filename 是要读取的文件名。如果文件不存在则为空。
* v 是一个持有整数的 vector。函数会改变 v。
 */
void load_vector(const string& filename, vector<int>& vec) {
    ifstream in;
    in.open(filename);
    if (in.good()) { // 确保文件已正确打开
        vec.clear(); // 清空 vector
        int value;
        while (in >> value) { // 读取到文件末尾
            vec.push_back(value);
        }
    } else
        cout << "Unable to load the file" << endl;
}

int main() {
    vector<int> list;
    bool done = false;
    char command;
    while (!done) {
        cout << "Enter a command (i=add, s=save, l=load, q=quit): ";
        cin >> command;
        switch (command) {
            case 'i':
                int val;
                cout << "Enter an integer: ";
                cin >> val;
                list.push_back(val);
                break;
            case 's':
                save_vector("numbers.txt", list);
                break;
            case 'l':
                load_vector("numbers.txt", list);
                break;
            case 'q':
                done = true;
                break;
            default:
                cout << "Unknown command" << endl;
        }
        print_vector(list);
    }
}
```
