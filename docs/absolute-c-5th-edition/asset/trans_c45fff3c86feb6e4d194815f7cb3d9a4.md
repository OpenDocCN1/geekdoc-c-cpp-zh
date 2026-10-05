

# 编程项目 511

在文件中。将实现放在单独的文件中。将命名空间定义分布在两个文件中。将演示程序放在第三个文件中。为了访问命名空间中的名称，你可以使用局部声明，例如：

```
using std::cout;
```

或者在块内部使用局部 using 指令，例如：

```
using namespace std;
```

或者使用命名空间名称来限定名称，例如 std::cout。你不能使用如下全局命名空间指令，因为它们不在块内，且适用于整个文件：

```
using namespace std;
```

- 3. 扩展第 10 章的编程项目 10.1。在该项目中，你实现实现了一个二维数组类，并将类定义和实现放在命名空间中，提供了对命名空间中名称的访问。测试你的代码。为了访问命名空间中的名称，你可以使用局部声明，例如：

```
using std::cout;
```

或者在块内部使用局部 using 指令，例如：

```
using namespace std;
```

或者使用命名空间名称来限定名称，例如 std::cout。你不能使用如下全局命名空间指令，因为它们不在块内，且适用于整个文件：

```
using namespace std;
```

- 4. 你想为你的系统验证用户的凭据。下面列出了名为 Security 的类，它用于验证用户和密码。（注意，此示例并不十分安全。通常，密码会被加密或存储在数据库中。）

```
class Security
{
    static int validate(string username, string password);
};
```

```
// 此子程序硬编码了有效用户，不
// 被认为是安全的做法。
// 如果凭据无效，返回 0，
// 如果是有效用户返回 1，
// 如果是有效管理员返回 2
```

```cpp
int Security::validate(string username, string password)
{
    if (username=="abbott") && (password=="monday") return 1;
    if (username=="costello") && (password=="tuesday") return 2;
    return 0;
}
```

# 第 11 章 分离编译与命名空间

将此类拆分为两个文件：一个头文件 Security.h 和一个实现文件 Security.cpp。

接下来，通过包含头文件创建另外两个使用 Security 类的类。第一个类应命名为 Administrator，包含一个名为 Login 的函数，如果给定的用户名和密码具有管理员权限，该函数返回 true。第二个类应命名为 User，包含一个名为 Login 的函数，如果给定的用户名和密码具有用户或管理员权限，该函数返回 true。

User 和 Administrator 类都应该拆分为用于头文件和实现的独立文件。

最后，编写一个 main 函数来调用 User 和 Administrator 类的 Login 函数，以测试它们是否正常工作。main 函数应该在一个单独的文件中。确保使用 #ifndef 指令以确保头文件不被包含多次。

- 5. 此项目探索了匿名命名空间（unnamed namespaces）是如何工作的。下面列出了用于执行用户名和密码输入验证的程序代码片段。输入和验证用户名的代码与输入和验证密码的代码位于不同的文件中。
头文件 user.cpp：

```
namespace Authenticate {
	void inputUsername() {
	do {
		cout << "Enter your username (8 letters only)" << endl;
		cin >> username;
	} while (!isValid());
	string getUsername() {
	return username;
}
}
```

在代码编译的匿名命名空间中定义 username 变量和 isValid() 函数。如果 username 正好包含八个字母，isValid() 函数应返回 true。为此代码生成一个适当的头文件。

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_541_0.png)

# 编程项目 513

对 password.cpp 重复相同的步骤，将密码变量和 isValid() 函数放在匿名命名空间。在这种情况下，如果输入至少包含八个字符且至少一个非字母，isValid() 函数应返回 true：
头文件 password.cpp：

```
namespace Authenticate {
    void inputPassword() {
        do {
            cout << "Enter your password (at least 8 characters) <<
            "and at least one non-letter" << endl;
            cin >> password;
        } while (!isValid());
    }
    string getPassword() {
        return password;
    }
}
```

此时，你应该有两个名为 isValid() 的函数，分别位于不同的匿名命名空间。在适当的位置放置以下 main 函数。程序应该可以编译并运行。

```cpp
int main() {
    inputUserName();
    inputPassword();
    cout << "Your username is " << getUsername() <<
    " and your password is: " <<
    getPassword() << endl;
    return 0;
}
```

使用多个无效的用户名和密码测试程序。

流与文件 I/O 12

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_544_0)

12.1 I/O 流

- 文件 I/O 217
- 陷阱：流变量的限制 222
- 追加文件 222
- 提示：打开文件的另一种语法 224
- 提示：检查文件是否成功打开 226
- 字符 I/O 228
- 检查文件末尾 229

12.3 流层次：继承的概述 547

- 流类之间的继承 547
- 示例：getline 函数 549
- 使用 stringstream 解析 553

12.4 随机访问文件 556

12.2 流 I/O 的工具 533

- 文件名 533
- 使用流函数格式化输出 534
- 操纵符 538
- 保存标志 539
- 更多输出流函数 540
- 示例：清理文件 542
- 示例：编辑文本文件 544

流与文件 I/O

鱼说，它们有流和池塘；
还有其他的吗？

> RUPERT BROOKE, Heaven (1913)

正如叶子被流携带，无论流流向湖泊还是大海，程序的输出也被流携带，而无论流是流向屏幕还是文件。

洗手间 计算机系墙 (1995)

# 引言

文件 I/O 涉及到少量但至关重要的继承，这直到第 14 章才会介绍。然而，我们将本章放在继承章节之前，程序员通常希望尽早开始文件 I/O。因此，本章包含了对文件 I/O 所需细分细节的简单介绍。

你可以在涵盖第 1 到 4 章和第 6 到 9 章内容的任何时候学习本章；也就是说，你可以在第 5、10 和 11 章之前学习本章。虽然第 2 章给出了简单的文件输入，但为了连续性，重复了这些概念。文件 I/O 的基本元素可以在阅读第 1 到 4 章、第 6 章以及第 9 章“成员函数和 put”小节后的任何时候学习。

12.1 I/O 流

> 天哪！四十年来，我一直在不知情的情况下说散文。

MOLIÈRE, Le Bourgeois Genthomme

流是字符（或其他类型的数据）的流动。如果流流程序，流被称为输出流。如果流进入程序，流被称为输入流。如果输入流来自键盘，你的程序将从键盘获取输入。同样，输出流可以流向文件。

尽管你可能没有意识到，你已经在程序中使用流了。你已经使用的 `cin` 是连接到键盘的输入流，而 `cout` 是连接到屏幕的。只要你的程序有 `<iostream>` 头文件的包含指令以及对 `std` 命名空间的 using 指令，这两个流对你的程序都是自动可用的。你可以定义来自文件或指向文件的流；你可以像定义 `cin` 和 `cout` 一样在程序中使用它们。例如，假设你的程序定义了一个来自某些文件的流 `inStream`。（稍后我们将告诉你如何定义它。）然后使用以下代码用该文件中的数字填充名为 `theNumber` 的 int 变量：

```cpp
int theNumber;
inStream >> theNumber;
```

同样，如果你的程序定义了一个指向另一个文件的输出流 `outStream`，你可以将 `theNumber` 的值输出到文件中。以下内容会将字符串 "theNumber is " 以及 `theNumber` 的内容输出到连接到流 `outStream` 的输出端：

```cpp
outStream << "theNumber is " << theNumber << endl;
```

# 文件 I/O

在本章用于 I/O 文件是文本文件；它们与你的 C++ 程序是相同的文件。当你的程序从文件获取输入时，被称为从文件读取；当你的程序将输出发送到文件时，被称为写入文件。还有其他从文件读取输入的方法，但本节讨论的方法是从文件开始到末尾（或程序在……之前）读取文件。

