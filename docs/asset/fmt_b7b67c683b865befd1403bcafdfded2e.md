
记号`\s`匹配单个空白字符（第 26、30 和 34 行）。用于`zipCode`字符串的表达式`\d{5}`（第 37 行）匹配任意五个数字。字符`"|"`（第 26、30 和 34 行）匹配其左侧或右侧的表达式。例如，`Hi (John|Jane)`匹配"Hi John"和"Hi Jane"。在第 26 行，我们使用字符`"|"`来表示地址可以包含一个或多个字符的单词，或一个或多个字符的单词后跟一个空格和另一个一个或多个字符的单词。注意使用括号对正则表达式的各个部分进行分组。量词可以应用于括号中包含的模式，以创建更复杂的正则表达式。

`lastName`和`firstName`变量（第 19 行和第 22 行）都接受以大写字母开头、长度任意的字符串。`address`字符串的正则表达式（第 26 行）匹配至少一位数字，后跟一个空格，然后是字母一个或多个字符，或者字母一个或多个字符后跟一个空格和另一个一个或多个字母的序列。因此，"10 Broadway"和"10 Main Street"都是有效的地址。按当前构成，第 26 行的正则表达式不匹配不以数字开头或包含超过两个单词的地址。`city`（第 30 行）和`state`（第 34 行）字符串的正则表达式匹配至少一个字符的任何单词，或者，如果单词由单个空格分隔，则匹配至少一个字符的任意两个单词。这意味着"Waltham"和"West Newton"都将匹配。同样，这些正则表达式不会接受包含超过两个单词的名称。`zipCode`字符串的正则表达式（第 37 行）确保邮政编码是五位数字。`phoneNumber`字符串的正则表达式（第 41 行）表示电话号码必须为`xxx-yyy-yyyy`的形式，其中`x`表示区号，`y`表示号码。第一个`x`和第一个`y`不能为零，如每个情况下的范围`[1-9]`所指定。

# 21.7.3 替换和拆分字符串

有时很有用将一个字符串的某些部分替换为另一个字符串，或根据正则表达式拆分字符串。为此目的，Boost.Regex库提供了算法`regex_replace`和`regex_token_iterator`类，我们在图 21.5 中演示。

算法`regex_replace`在字符串中用新文本替换与正则表达式匹配的文本。在第 23 行，`regex_replace`用`"A"`替换`testString1`中每个`"*"`的实例。请注意，正则表达式（`"\*"`）在字符`"*"`前加上反斜杠`\`。通常，`*`是一个量词，表示正则表达式应匹配前一个模式的任意次数出现。然而，在这种情况下，我们希望找到字面字符`"*"`的所有出现；为此，我们必须用字符`"\ "`转义字符`"*"`。通过用`\`转义特殊正则表达式字符，我们告诉正则表达式匹配引擎查找实际字符`"*"`而不是将其用作量词。第 27–28 行使用`regex_replace`替换字符串

```cpp
// Fig. 21.5: RegexSubstitution.cpp
// Using regex_replace algorithm.
#include <iostream>
using std::cout;
using std::endl;

#include <string>
using std::string;

#include "boost/regex.hpp"

int main()
{
    // create the test strings
    string testString1 = "This sentence ends in 5 stars *****";
    string testString2 = "1, 2, 3, 4, 5, 6, 7, 8";
    string output;

    cout << "Original string: " << testString1 << endl;

    // replace every * with a ^
    testString1 =
        boost::regex_replace( testString1, boost::regex( "\\*" ), "^" );
    cout << "^ substituted for *: " << testString1 << endl;

    // replace "stars" with "carets"
    testString1 = boost::regex_replace(
        testString1, boost::regex( "stars" ), "carets" );
    cout << "\"carets\" substituted for \"stars\": "
        << testString1 << endl;

    // replace every word with "word"
    testString1 = boost::regex_replace(
        testString1, boost::regex( "\\w+" ), "word" );
    cout << "Every word replaced by \"word\": " << testString1 << endl;

    // replace the first three digits with "digit"
    cout << "\nOriginal string: " << testString2 << endl;
    string testString2Copy = testString2;

    for ( int i = 0; i < 3; i++ ) // loop three times
    {
        testString2Copy = boost::regex_replace( testString2Copy,
            boost::regex( "\\d" ), "digit", boost::format_first_only );
    } // end for

    cout << "Replace first 3 digits by \"digit\": "
        << testString2Copy << endl;

    // split the string at the commas
    cout << "string split at commas [";

    boost::sregex_token_iterator tokenIterator( testString2.begin(),
        testString2.end(), boost::regex(",\\s"), -1 ); // token iterator
    boost::sregex_token_iterator end; // empty iterator

    while ( tokenIterator != end ) // tokenIterator isn't empty
    {
        output += "\"" + *tokenIterator + "\", "; // add the token to output
        tokenIterator++; // advance the iterator
    } // end while

    // delete the ", " at the end of output string
    cout << output.substr( 0, output.length() - 2 ) << "]" << endl;

    return 0;
} // end of function main
```

```text
Original string: This sentence ends in 5 stars *****
^ substituted for *: This sentence ends in 5 stars ^^^^^
"carets" substituted for "stars": This sentence ends in 5 carets ^^^^^
Every word replaced by "word": word word word word word word ^^^^^

Original string: 1, 2, 3, 4, 5, 6, 7, 8
Replace first 3 digits by "digit": digit, digit, digit, 4, 5, 6, 7, 8
string split at commas ["1", "2", "3", "4", "5", "6", "7", "8"]
```

## Fig. 21.5 | Using regex_replace algorithm. (Part 2 of 2.)

第 31–32 行将`testString1`中的"stars"替换为字符串"carets"。第 33–34 行使用`regex_replace`将`testString1`中的每个单词替换为字符串"word"。

第 41–45 行将`testString2`中前三个数字实例（`\d`）替换为文本"digit"。我们向`regex_replace`传递了一个额外的参数`boost::format_first_only`（第 43–44 行）。该参数告诉`regex_replace`仅替换与正则表达式匹配的第一个子字符串。通常`regex_replace`会替换模式的所有出现。我们将此调用放在运行三次的`for`循环中；每次都将数字的第一个实例替换为文本"digit"。我们使用`testString2`的副本（第 39 行），以便在示例的下一部分仍能使用原始的`testString2`。

接下来我们使用`regex_token_iterator`将一个字符串划分为多个子字符串。`regex_token_iterator`会遍历与正则表达式匹配的字符串各部分。第 53 行和第 55 行使用`boost::sregex_token_iterator`，它是一个typedef，表示结果将使用`string::const_iterator`进行操作。我们通过构造函数创建迭代器（第 53–54 行），向其传递两个迭代器（`testString2.begin()`和`testString2.end()`），它们表示要遍历的字符串的开始和结束，以及要查找的正则表达式。在我们的例子中，我们希望遍历与正则表达式不匹配的部分。为此我们向构造函数传递`-1`。这表示它应遍历每个与正则表达式不匹配的子字符串。原始字符串会在匹配指定正则表达式的分隔符处被拆分。我们使用`while`语句（第 57–61 行）将每个子字符串添加到输出字符串（第 17 行）。`regex_token_iterator`的`end`（第 55 行）是一个空迭代器。当`tokenIterator`等于`end`（第 57 行）时，我们已遍历完整个字符串。

# 21.8 使用 Boost.Smart_ptr 的智能指针

C 和 C++ 代码中的许多常见错误都与指针有关。智能指针通过为标准指针提供额外功能来帮助你避免错误。此功能通常会加强内存分配和释放的过程。智能指针还有助于你编写异常安全的代码。如果在对指针调用`delete`之前程序抛出异常，就会造成内存泄漏。抛出异常后，智能指针的析构函数仍会被调用，它会为你调用`delete`。

C++ 标准库提供了一个基本的智能指针`std::auto_ptr`。`auto_ptr`负责管理动态分配的内存，并在`auto_ptr`被销毁或超出作用域时自动调用`delete`以释放动态内存。这些智能指针非常适合自动变量。第 16.12 节讨论了`auto_ptr`。

`auto_ptr`有一些限制。例如，`auto_ptr`不能指向数组。删除指向数组的指针时必须使用`delete[]`以确保数组中所有对象的析构函数都被调用，但`auto_ptr`使用`delete`。`auto_ptr`的另一个限制是它不能与 STL 容器一起使用——STL 容器中的元素必须能够安全地复制。当`auto_ptr`被复制时，内存的所有权会转移到新的`auto_ptr`，而原`auto_ptr`会被设为`NULL`。STL 容器可能会复制其元素，因此你无法保证在处理容器元素结束的算法完成后`auto_ptr`的有效副本仍然存在。

Boost.Smart_ptr 库提供了额外的智能指针，以填补`auto_ptr`不起作用的空白。TR1 包含了 Boost.Smart_ptr 库中六种智能指针类型中的两种，即`shared_ptr`和`weak_ptr`。这些智能指针并非旨在取代`auto_ptr`。相反，它们提供了具有不同功能的其他选项。

## 21.8.1 引用计数的 shared_ptr

`shared_ptrs`持有指向资源（例如动态分配的对象）的内部指针，该资源可能与程序中的其他对象共享。你可以有任意数量的`shared_ptrs`指向同一资源。`shared_ptrs`确实共享资源——如果你使用一个`shared_ptr`修改资源，其他`shared_ptrs`也会"看到"这些更改。内部指针会在指向该资源的最后一个`shared_ptr`被销毁时被删除。`shared_ptrs`使用引用计数来确定有多少个`shared_ptrs`指向该资源。每次为资源创建新的`shared_ptr`时，引用计数就会增加；每次销毁一个时，引用计数就会减少。当引用计数达到零时，内部指针将被删除并释放内存。

`shared_ptrs`在需要多个指向同一资源的指针的情况下很有用，例如在 STL 容器中。`auto_ptrs`不能在 STL 容器中使用，因为容器或操作它们的算法可能会复制存储的元素。`auto_ptr`的副本不相等，因为复制后原指针会被设为`NULL`。另一方面，`shared_ptrs`可以安全地复制并在 STL 容器中使用。

`shared_ptr`还允许你确定资源将被如何销毁。对于大多数动态分配的对象，使用`delete`。然而，一些资源需要更复杂的清理。在这种情况下，你可以向`shared_ptr`构造函数提供自定义的 deleter 函数或函数对象。deleter 决定如何销毁资源。当引用计数达到零且资源准备好被销毁时，`shared_ptr`调用自定义析构函数。此功能使`shared_ptr`能够管理几乎任何类型的资源。

## Example Using shared_ptr

图 21.6–21.7 定义了一个简单的类来表示一本书，使用字符串来表示书名。类`Book`的析构函数（图 21.7，第 16–19 行）在屏幕上显示一条消息，指示正在销毁一个实例。我们使用此类来演示`shared_ptr`的常见功能。

图 21.8 中的程序使用`shared_ptrs`来管理多个类`Book`的实例。我们包含`"boost/shared_ptr.hpp"`头文件以便能够使用`shared_ptrs`。我们

```cpp
// Fig. 21.6: Book.h
// Declaration of class Book.
#ifndef BOOK_H
#define BOOK_H
#include <string>
using std::string;

class Book
{
public:
    Book( const string &bookTitle ); // constructor
    ~Book(); // destructor
    string title; // title of the Book
};
#endif // BOOK_H
```

Fig. 21.6 | Book header file.

```cpp
// Fig. 21.7: Book.cpp
// Member-function definitions for class Book.
#include <iostream>
using std::cout;
using std::endl;

#include <string>
using std::string;

#include "Book.h"

Book::Book( const string &bookTitle ) : title( bookTitle )
{
}

Book::~Book()
{
    cout << "Destroying Book: " << title << endl;
} // end of destructor
```

Fig. 21.7 | Book member-function definitions.
