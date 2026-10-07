
```cpp
readIntegerField(fileName, myInts);
} catch (const invalid_argument& e) {
cerr << e.what() << endl;
return 1;
}
}
```
```cpp
} catch (const runtime_error& e) {
cerr << e.what() << endl;
return 1;
} catch (int x) {
cerr << "Caught " << x << endl;
set_unexpected(old_handler);
// Remainder of function omitted
}
```

现在 `main()` 通过将来自 `readIntegerField()` 的任何异常转换为 `runtime_error` 来处理它们。然而，使用 `set_terminate()` 时，建议谨慎地使用此功能。
`unexpected()`、`set_unexpected()` 和 `bad_exception` 均在 `<exception>` 头文件中声明。

# 在重写的方法中更改抛列表（Throw List）

当你在派类中重写虚方法时，你可以更改抛列表，只要该列表比基类中的抛列表更严格。以下更改符合更严格的定义：

- 从列表中移除异常
- 添加基类抛列表中已出现的异常类
- 将其设为 `noexcept` 方法

以下更改不符合更严格的定义：

- 向列表中添加并非基类抛列表中异常的派生类的异常
- 完全移除抛列表

> 警告：当你在重写方法时更改抛列表，请记住任何调用基类方法版本的代码都能够调用派生类版本。因此，你不能添加异常。

例如，假设你有如下基类：

```cpp
class Base {
public:
virtual ~Base() {}
virtual void func() throw(exception) { cout << "Base\n"; }
};
```

你可以写一个派生类来重写 `func()`，并指定它不抛出任何异常。

```cpp
class Derived : public Base {
public:
virtual void func() noexcept { cout << "Derived\n"; }
};
```

你可以重写 `func()`，使其既抛出 `runtime_error` 也抛出 `exception`，因为 `runtime_error` 是 `exception` 的派生类。

```cpp
class Derived : public Base {
public:
virtual void func() throw(exception, runtime_error) {
cout << "Derived\n"; }
};
```

然而，你不能完全移除抛列表，因为这意味着 `func()` 可能会抛出任何异常。
作为第二个例子，假设 `Base` 看起来如下：

```cpp
class Base {
public:
virtual ~Base() {}
virtual void func() throw(runtime_error) { cout << "Base\n"; }
};
```

那么你不能在 `Derived` 中用如下抛列表来重写 `func()`：

```cpp
class Derived : public Base {
public:
virtual void func() throw(exception) // 错误！
cout << "Derived\n"; }
};
```

`exception` 是 `runtime_error` 的类，所以你不能用 `exception` 替换 `runtime_error`。

# 抛列表有用吗？

来自特定函数的异常是其接口的重要部分，应该尽可能地进行记录。在过去，你可以考虑通过抛列表来记录它们。大多数 C++ 代码（包括标准库）都没有使用抛列表。这使得在你在使用这些代码时，很难确定可能会抛出哪些异常。此外，无法指定模板函数和方法的异常特性。当你甚至不知道将使用什么类型来实例化模板时，你无法确定这些类型的方法可以抛出哪些异常。

自 C++11 以来，决策变得简单：永远不要使用抛列表，因为它们现在已被弃用，`noexcept` 除外。相反，请在代码文档中记录函数可能抛出的异常。

# 异常与多态

如前述描述的，你实际上可以抛出任何类型的异常。然而，类是最有用的异常类型。事实上，异常类通常写在层次结构中，以便你在捕获异常时可以使用多态性。

# 标准异常层次结构

你已经看到了 C++ 标准异常层次结构中的几种异常：`runtime_error` 和 `invalid_argument`。图 13-3 显示了完整的层次结构：

![](img/5dda262a2e4cfd8040434fe81f2b4e78_434_0.png)

图 13-3

C++ 标准库抛出的所有异常都是该层次结构中类的对象。层次结构中的每个类都支持一个 `what()` 方法，该方法返回一个描述异常的 `const char*` 字符串。你可以在错误消息中使用这个字符串。

除了需要在构造函数中设置的基异常外，所有异常都需要设置 `what()` 返回的字符串。这就是为什么你需要在 `runtime_error` 和 `invalid_argument` 的构造函数中指定一个字符串。在本章的示例中已经完成了。这里是另一个 `readIntegerFile()` 的版本，它在错误消息中包含了文件名。

```cpp
void readIntegerFile(const string& fileName, vector<int>& dest) {
istream instr;
int temp;
instr.open(fileName.c_str());
if (instr.fail()) {
// 打开文件失败：抛出一个异常。
string error = "Unable to open file " + fileName;
throw invalid_argument(error);
}
// 逐个读取整数并将它们添加到 vector。
while (instr >> temp) {
dest.push_back(temp);
}
if (instr.eof()) {
// 我们没有到达文件末尾。
// 这意味着在读取文件时发生了错误。
// 抛出一个异常。
string error = "Unable to read file " + fileName;
throw runtime_error(error);
}
}
int main() {
try {
readIntegerFile("test.txt", dest);
} catch (const invalid_argument& e) {
cerr << e.what() << endl;
return 1;
} catch (const runtime_error& e) {
cerr << e.what() << endl;
return 1;
}
return 0;
}
```
*(注：原文提供的 `readIntegerFile` 示例代码在结尾处似乎不完整，根据上下文在翻译中进行了逻辑补全以保持一致性)*

# 在类层次结构中捕获异常

如之前所述，你实际上可以捕获任何类型的异常。类层次结构的一个特点是你可以以多态的方式来捕获异常。例如，如果你查看 `main()` 函数中调用 `readIntegerFile()` 后的两个捕获语句，你会发现它们除了处理的异常外完全相同。方便的是，`invalid_argument` 和 `runtime_error` 都是 `exception` 的派生类，所以你可以用一个异常异常捕获语句替换那两个：

```cpp
try {
readIntegerFile("test.txt", dest);
} catch (const exception& e) {
cerr << e.what() << endl;
return 1;
}
```

`exception` 捕获语句匹配 `exception` 的派生类。注意，在异常层次结构中捕获的位置越高，你的错误处理就越不具体。你应该尽可能在具体的级别捕获异常。

> 警告：当你以多态方式捕获异常时，请确保通过引用捕获。如果你按值捕获异常，可能会遇到切片问题。详情请参见第 9 章。

当使用多个捕获语句时，捕获语句按照它们在代码中的出现顺序进行匹配；匹配者获胜。如果一个捕获语句比另一个更具包含性，它将匹配，而更严格的将永远不会执行。例如，如果你想显式捕获来自 `readFile()` 的 `invalid_argument`，但让通用的 `exception` 匹配其他异常。正确的方法如下：

```cpp
try {
readIntegerFile("test.txt", dest);
} catch (invalid_argument& e) { // 先列出派生类
// 对无效文件名进行特殊处理。
} catch (exception& e) { // 现在列出异常
cerr << e.what() << endl;
return 1;
}
```

第一个捕获语句捕获 `invalid_argument` 异常，第二个捕获其他类型的 `exception` 异常。然而，如果你反转了捕获语句的顺序，就得不到结果：

```cpp
try {
readIntegerFile("test.txt", dest);
} catch (exception& e) { // Bug：先捕获了基类！
cerr << e.what() << endl;
return 1;
} catch (invalid_argument& e) {
// 对无效文件名进行特殊处理。
}
```

在这种情况下，任何派自 `exception` 类的异常都会被第一个捕获语句捕获，第二个永远不会被到达。某些编译器在这种情况下会发出，但你不应该依赖此。

# 编写你自己的异常类

编写自己的异常类有两个优点。

- 1. C++ 标准库中的异常数量是有限的。与其使用具有通用名称的异常（如 `runtime_error`），你不如创建一个对你程序中特定错误更具意义的类名。
- 2. 你可以向这些异常添加你自己的信息。标准层级结构中的异常仅允许你设置一个错误字符串。你可能希望在异常中传递不同的信息。

建议所有的异常类都直接或间接继承自标准异常基类 `exception`。如果项目中的每一个人都遵循这一规则，你就知道程序中的每个异常都派生自 `exception`（假设你没有使用违反此规则的第三方库）。这一准则使得不使用多态的异常处理变得简单得多。

例如，`invalid_argument` 和 `runtime_error` 无法很好地捕捉 `readOpenFile()` 中的文件打开和读取错误。你可以为文件错误定义自己的错误层次结构，从一个通用的 `FileError` 类开始：

```cpp
class FileError : public exception
{
public:
FileError(const string& fileIn) : mFile(fileIn) {}
virtual const char* what() const override { return mMsg.c_str(); }
const string& getFileName() const { return mFile; }
protected:
void setMessage(const string& message) { mMsg = message; }
private:
string mFile, mMsg;
};
```

通用的 `FileError` 类还包含一个文件名、一个用于文件名的公共访问器以及一个派生类可以设置的保护设置器。

`readOpenFile()` 中的第一个情况发生在文件无法打开时。因此，你可能从 `FileError` 派生出一个 `FileOpenError`：

```cpp
class FileOpenError : public FileError
{
public:
FileOpenError(const string& fileNameIn);
};
FileError::FileOpenError(const string& fileName) : FileError(fileName)
{
setErrorMessage("Unable to open " + fileName);
}
```

`FileOpenError` 改变 `mMsg` 字符串以表示文件打开错误。

`readIntegerFile()` 中的第二个异常情况发生在文件无法被正确读取时。该异常包含错误所在的行号，以及 `what()` 返回的错误消息字符串中的文件名，可能会很有用。这里有一个派生自 `FileError` 的 `FileReadError`：

```cpp
class FileReadError : public FileError
{
public:
FileReadError(const string& fileName, int lineNum);
int getLineNum() { return lineNum; }
private:
int lineNum;
};
FileReadError::FileReadError(const string& fileName, int lineNum)
: FileError(fileName), lineNum(lineNum)
{
ostringstream osstr;
ostr << "Error reading " << fileName << " at line " << lineNum;
setMessage(ostr.str());
}
```

为了保留行号，你需要修改 `readIntegerFile()` 来跟踪读取的行数，而不是直接读取整数。以下是一个使用新异常的新的 `readIntegerFile()` 函数：

```cpp
void readIntegerFile(const string& fileName, vector<int>& dest)
{
istringstream isr;
int temp;
string line;
int lineNumber = 0;
isr.open(fileName.c_str());
if (isr.fail()) {
// 无法打开文件：抛出异常。
throw FileOpenError(fileName);
}
while (!isr.eof()) {
// 从文件中读取一行。
getline(isr, line);
lineNumber++;
// 将行转换为字符串。
istringstream lineStream(line);
// 逐个读取整数并将其添加到 vector 中。
while (lineStream >> temp) {
dest.push_back(temp);
}
}
}
```

栈帧（Stack frames）。栈回溯（Stack unwinding）意味着所有局部作用域名称的析构函数都会被调用，并且每个函数中当前执行点之后的所有代码都会被跳过。

然而，在栈回溯过程中，指针变量不会被释放，也不会执行其他清理工作。这种行为可能会引发问题，如下代码所示：

```cpp
void funcOne();
void funcTwo();
int main()
{
try {
funcOne();
} catch (exception& e) {
cerr << "Exception caught!" << endl;
return 1;
}
return 0;
}
void funcOne()
{
string str1;
string* str2 = new string();
funcTwo();
delete str2;
}
void funcTwo()
{
istream istr;
istr.open("filename");
throw exception();
istr.close();
}
```

当 `funcTwo()` 抛出异常时，最近的异常处理器在 `main()` 中。控制权立即从 `funcTwo()` 中的这一行跳转：

```cpp
throw exception();
```

到 `main()` 中的这一行：

```cpp
cerr << "Exception caught!" << endl;
```
