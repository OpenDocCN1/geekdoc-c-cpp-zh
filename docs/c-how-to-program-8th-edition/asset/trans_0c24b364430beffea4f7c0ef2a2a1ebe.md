
**图23.5** | 使用 `regex_replace` 算法。（第2部分，共3部分。）

```cpp
// create the test strings
string testString1 = "This sentence ends in 5 stars *****";
string testString2 = "1, 2, 3, 4, 5, 6, 7, 8";
string output;

cout << "Original string: " << testString1 << endl;

// replace every * with a ^
testString1 =
   regex_replace( testString1, regex( "\\*" ), string( "^" ) );
cout << "^ substituted for *: " << testString1 << endl;

// replace "stars" with "carets"
testString1 =
   regex_replace( testString1, regex( "stars" ), string( "carets" ) );
cout << "\"carets\" substituted for \"stars\": "
   << testString1 << endl;

// replace every word with "word"
testString1 =
   regex_replace( testString1, regex( "\\w+" ), string( "word" ) );
cout << "Every word replaced by \"word\": " << testString1 << endl;

// replace the first three digits with "digit"
cout << "\nOriginal string: " << testString2 << endl;
string testString2Copy = testString2;

for ( int i = 0; i < 3; ++i ) // loop three times
{
   testString2Copy = regex_replace( testString2Copy,
      regex( "\\d" ), "digit", regex_constants::format_first_only );
} // end for

cout << "Replace first 3 digits by \"digit\": "
   << testString2Copy << endl;

// split the string at the commas
cout << "string split at commas [";

regex splitter( ",\\s" ); // regex to split a string at commas
sregex_token_iterator tokenIterator( testString2.begin(),
   testString2.end(), splitter, -1 ); // token iterator
sregex_token_iterator end; // end iterator

while ( tokenIterator != end ) // tokenIterator isn’t empty
{
   output += "\"" + (*tokenIterator).str() + "\", ";
   ++tokenIterator; // advance the iterator
} // end while

// delete the ", " at the end of output string
cout << output.substr( 0, output.length() - 2 ) << "]" << endl;
} // end of function main
```

**图23.5** | 使用 `regex_replace` 算法。（第3部分，共3部分。）

```
Original string: This sentence ends in 5 stars *****
^ substituted for *: This sentence ends in 5 stars ^^^^^
"carets" substituted for "stars": This sentence ends in 5 carets ^^^^^
Every word replaced by "word": word word word word word word ^^^^^

Original string: 1, 2, 3, 4, 5, 6, 7, 8
Replace first 3 digits by "digit": digit, digit, digit, 4, 5, 6, 7, 8
string split at commas ["1", "2", "3", "4", "5", "6", "7", "8"]
```

### 使用 `regex_replace` 替换子字符串

算法 `regex_replace` 会在原字符串与正则表达式匹配的位置，用新文本替换字符串中的文本。在第19行，`regex_replace` 将 `testString1` 中每一处 `"*"` 替换为 `"^"`。正则表达式（`"\\*"`）在字符 `"*"` 前加了一个反斜杠（`\`）。通常，`"*"` 是一个量词，表示正则表达式应匹配前一模式任意次出现。然而，在本例中我们想查找字面字符 `"*"` 的所有出现，因此必须用字符 `"\\"` 转义字符 `"*"`。通过用 `\` 转义正则表达式特殊字符，我们告诉正则表达式匹配引擎查找实际的字符 `"*"`，而不是将其用作量词。此外，这个版本的函数 `regex_replace` 的第一个和最后一个实参必须是字符串。第23–24行使用 `regex_replace` 将 `testString1` 中的字符串 `"stars"` 替换为字符串 `"carets"`。第29–30行使用 `regex_replace` 将 `testString1` 中的每个单词替换为字符串 `"word"`。

第37–41行将 `testString2` 中前三个数字实例（`"\\d"`）替换为文本 `"digit"`。我们将 `regex_constants::format_first_only` 作为附加实参传给 `regex_replace`（第39–40行）。该实参告诉 `regex_replace` 只替换与正则表达式匹配的第一个子字符串。通常，`regex_replace` 会替换该模式的所有出现。我们将此调用放在一个运行三次的 for 循环中；每次将第一个数字实例替换为文本 `"digit"`。我们使用 `testString2` 的一个副本（第35行），以便在示例的下一部分使用原始 `testString2`。

### 使用 `regex_token_iterator` 获取子字符串

接下来，我们使用 `regex_token_iterator` 将字符串划分为若干子字符串。`regex_token_iterator` 会遍历字符串中与正则表达式匹配的部分。第49行和第51行使用 `sregex_token_iterator`，它是一个 typedef，表示结果要用 `string::const_iterator` 来操作。我们通过向构造函数传入两个迭代器（`testString2.begin()` 和 `testString2.end()`）来创建该迭代器（第49–50行），它们分别表示要遍历的字符串的开头和结尾，以及要查找的正则表达式。在本例中，我们要遍历字符串中不与正则表达式匹配的部分。为此，我们向构造函数传入 -1。这表示它应遍历每个不与正则表达式匹配的子字符串。原字符串在匹配指定正则表达式的分隔符处被断开。我们使用 `while` 语句（第53–57行）将每个子字符串添加到字符串 output 中。该迭代器最初设置为字符串中的第一个标记。当 `tokenIterator` 等于 `end` 时（第53行），我们就遍历完了整个字符串。

## 23.6 智能指针

**注意：** 本节示例中使用的 C++0x 库特性在 Microsoft Visual C++ 2010 Express 和 GNU C++ 4.5 中均可使用。GNU C++ 将这些特性视为实验性的，并要求使用命令行选项 `-std=c++0x` 才能正确编译这些示例。

C 和 C++ 代码中的许多常见缺陷都与指针有关。**智能指针**通过为标准指针提供额外功能来帮助避免错误。这种功能通常会加强内存分配和释放过程。智能指针还能帮助编写异常安全的代码。如果程序在调用指针的 `delete` 之前抛出异常，就会造成内存泄漏。异常抛出后，智能指针的析构函数仍会被调用，它会替你对该指针调用 `delete`。

第16.11节介绍了一种智能指针类——`unique_ptr`——它负责管理动态分配的内存。当 `unique_ptr` 被销毁或离开作用域时，`unique_ptr` 会自动调用 `delete` 释放其关联的动态内存。`unique_ptr` 是一种基本的智能指针。C++0x 还提供了其他具有额外功能的智能指针选项。

### 23.6.1 引用计数的 shared_ptr

`shared_ptr`（来自头文件 `<memory>`）持有指向某个资源的内部指针（例如动态分配的对象），该资源可与程序中的其他对象共享。你可以拥有任意数量的 `shared_ptr` 指向同一资源。`shared_ptr` 确实共享该资源——如果你通过一个 `shared_ptr` 修改资源，其他 `shared_ptr` 也会“看到”这些修改。一旦指向该资源的最后一个 `shared_ptr` 被销毁，内部指针就会被删除。`shared_ptr` 使用**引用计数**来确定有多少个 `shared_ptr` 指向该资源。每当创建一个指向该资源的新 `shared_ptr`，引用计数就增加；每当销毁一个，引用计数就减少。当引用计数达到零时，内部指针被删除，内存被释放。

在需要多个指针指向同一资源的情况下（例如在 STL 容器中），`shared_ptr` 很有用。`shared_ptr` 可以安全地复制并在 STL 容器中使用。

`shared_ptr` 还允许你决定资源将如何被销毁。对于大多数动态分配的对象，使用 `delete`。然而，有些资源需要更复杂的清理。在这种情况下，你可以向 `shared_ptr` 构造函数提供一个自定义的**删除器**函数或函数对象。删除器决定如何销毁资源。当引用计数达到零且资源准备销毁时，`shared_ptr` 会调用自定义删除器函数。这一功能使 `shared_ptr` 几乎能管理任何类型的资源。

#### 使用 shared_ptr 的示例

图23.6–23.7定义了一个简单的类来表示 Book，并用一个字符串表示 Book 的标题。Book 类的析构函数（图23.7，第12–15行）会在屏幕上显示一条消息，表示某个实例正在被销毁。我们使用这个类来演示 `shared_ptr` 的常见功能。
