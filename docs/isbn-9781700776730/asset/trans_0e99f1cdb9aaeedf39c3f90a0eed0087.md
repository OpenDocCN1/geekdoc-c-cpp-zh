

```
int* ptr1 = new int[5];
int** ptr2 = new int*[8];
...
delete [] ptr1;
delete [] ptr2;
```

使用方括号是为了告诉编译器在堆上期望一个对象数组。当你需要删除一个用户定义对象的数组时，这具有重要意义。

因此，规则是：如果你在 `new` 中使用了方括号，那么在 `delete` 中也要使用方括号。如果你在 `new` 中没有使用方括号，那么在 `delete` 中就不要使用方括号。

注意：如果传递给 `delete` 的指针内容包含零或 `null`，这是完全允许的，因为这种情况保证不会产生任何有害影响。

在接下来的示例中，用户被要求从键盘输入字符串数据。输入被捕获到一个固定长度的缓冲区区域，然后将其复制到堆上。请注意，为每个字符串分配的堆空间恰好是其所需的量。在输入所有字符串后，将它们打印出来，并通过 `delete` 释放它们的堆空间。

关键数据元素是 `ptr`，这是一个指向指针的指针，这样用于跟踪字符串的指针数组就可以在堆上动态增长。

```cpp
// Dynamic Memory Allocation

#include <iostream>
#include <string.h>

using namespace std;

void input(char**& ptr, int& counter);
void output(char** ptr, int counter);
void release(char** ptr, int counter);
```

```cpp
int main() {
  char** pptr = 0;
  int counter = 0;
  input(ptr, counter);
  output(ptr, counter);
  release(ptr, counter);
  return 0;
}
```

```cpp
void input(char** pptr, int& counter) {
  const int MAX = 256;

  cout << "Enter string: ";
  char buf[MAX];
  // 使用 Ctrl-D 结束输入
  while (!(cin >> buf).eof()) {
    // 获取实际空间大小
    char* temp = new char[strlen(buf) + 1];
    strcpy(temp, buf);
    // 指针数组动态增长
    char** temp_pptr = new char*[counter+1];
    for (int i = 0; i < counter; ++i) {
      temp_pptr[i] = pptr[i];
    }
    temp_pptr[counter++] = temp;
    // 释放旧指针的空间
    delete []pptr];
    // 更新指针指向当前指针数组
    pptr = temp_pptr;
    cout << "Next string: ";
  }
}
```

```cpp
void output(char** pptr, int counter) {
  const char QUOTE = "'";

  if (counter > 0) {
    cout << "\nstrings:\n";
    for (int i = 0; i < counter; ++i) {
      cout << QUOTE << pptr[i] << QUOTE << '\n';
    }
  } else {
    cout << "Empty list\n";
  }
}
```

```cpp
void release(char** pptr, int counter) {
  for (int i = counter - 1; i >= 0; --i) {
    delete []pptr[i]];
  }
  delete []pptr];
}
```

# 输出如下：

Enter string: All
Next string: you
Next string: need
Next string: is
Next string: love.
Next string:
The strings:
"All"
"you"
"need"
"is"
"love."

# 指针陷阱

指针变量为程序员提供了极大的活性，但它们可能导致程序出现难以发现和修正的错误。我们将检查常见问题，并提供如何避免它们的提示。

假设以下类型和变量声明：

```cpp
int *first = NULL;
int *second;
int *third;
int num = 4;
```

我们还假设以下代码已经执行：

```cpp
second = new int;
*second = 2;
```

# 解引用 NULL

解引用 NULL 是一个错误。这是最安全的错误，因为系统通常会在运行时捕获该错误。

```cpp
cout << *first << endl; // 错误，first 为 NULL
```

如果你的类型是类或结构体，使用 `->` 运算符解引用 NULL 同样是一个问题。NULL 指针指向任何地方。解引用会获取指针所指向的内容。

# 悬空指针

解引用一个没有正确赋值的指针是一个错误。这个错误可能会导致最终崩溃，但通常是在错误运行一段时间后。

```cpp
cout << *third << endl; // 错误，third 没有值
```

有趣的是，很可能会打印某些内容。如果这个值对运行中的程序看起来像是一个有效指针，我们将获得几个内存位置的内容，并将其解释为 `int`，而无论它们实际上包含什么。

更糟糕的是：

```cpp
*third = 3;      // 严重错误 - 修改了随机内存位置
```

指针可以通过赋值 NULL 或另一个已知的有效指针来获得有效值。你可以给它赋值调用 `operator new` 的结果。你也可以获得一个有效指针。

# 别名问题

为同一个单元格拥有多个名称会增加危险。例如，删除不是通过 `new` 分配的单元格是一个错误；然而，删除一个不是通过 `new` 分配的指针是一个错误。在最后句话中，我们说“删除一个指针”。被删除的不是指针本身。

# 在未分配的情况下删除

删除 NULL 指针是一个逻辑错误。但在 C++ 中这是可以的，系统会忽略它。然而，这样做有时表明你的逻辑存在错误；删除一个不是通过 `new` 分配的指针是一个错误。

