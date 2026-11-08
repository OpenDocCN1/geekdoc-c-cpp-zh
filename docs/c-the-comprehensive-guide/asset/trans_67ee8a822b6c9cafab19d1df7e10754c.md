

产生错误行为。除以零？数组少一个元素？那么你的程序就有了一个*缺陷*。幸运的话，你可以通过错误码保护自己免受致命后果，但更多时候是通过异常。

- **质量错误**

  质量错误是指那些虽然不会阻止最终用户获得正确结果，但仍然会给用户或程序员带来妥协的问题。对用户而言，这可能意味着程序运行太慢或对话框难以使用。对程序员而言，这可能意味着软件难以维护，并可能导致未来的编程错误。这个广泛的类别还涉及代码可读性、测试、文档等主观因素。

  质量错误通常源于缺乏对编码标准和最佳实践的遵循，这可能导致代码库支离破碎且不一致。这种不一致会使协作开发更加困难，并在进行更改时增加引入新缺陷的可能性。因此，解决质量错误不仅对于确保流畅愉悦的用户体验至关重要，而且对于维持可持续且高效的开发过程也至关重要。

你可以看到，*错误*一词涵盖了许多完全不同的事情。在本章中，我们完全不涉及质量错误，很少涉及编程和程序错误，部分涉及意外状态，而主要涉及不期望的状态。当你处理错误时，在某种程度上你是在预料它们——而本章正是关于错误处理的。

### 10.1 使用错误码处理错误

使用错误码时，通过返回值和错误参数来传达错误状态的信息。如下面的代码清单所示。

```cpp
//https://godbolt.org/z/EWqqGjnn
#include <iostream> // cout,cerr
#include <fstream>
#include <vector>
#include <string>
using std::vector; using std::string; using std::cout; using std::cerr;

int countWords(const string& filename) { // return negative on error
  std::ifstream file(filename);
  if(!file) { // was there an error opening the file?
    cerr << "Error opening " << filename << "\n";
    return -1; // report an error to the caller using a special value
  }
  int count = 0;
  string word;
  while(!file.eof()) {             // not at the end yet?
      file >> word;
      ++count;
  }
  return count-1;                  // one more word was read at EOF
}

bool process(const vector<string>& args) { // return true if all okay
    if(args.size() == 0) {                // expecting parameters
        cerr << "Command line argument missing\n";
        return false;                     // report an error via return
    } else {
        bool result = true;               // for the final result
        for(const string filename : args) {
            cout << filename << " ";
            int count = countWords(filename);
            if(count < 0) {               // special return indicates error
                cout << "Error!\n";
                result = false;            // at least one error
            } else {
                cout << count << "\n";    // output normal result
            }
        }
        return result;                    // return overall result
    }
}

int main(int argc, const char* argv[]) {
    bool result = process(              // return value contains error indicator
        {argv+1, argv+argc} );           // const char*[] to vector<string>
    if(result) {                         // evaluate return value
        return 0;
    } else {
        cerr << "An error occurred.\n";
        return 1;                        // indicate error externally
    }
}
```

**清单 10.1** 使用不同类型的返回值应对多种状态。

你常常会看到用`if`检查那些不理想的状态：

- 通过`if(!file)`，我检查文件是否打开成功。
- 通过`if(args.size()==0)`，我检查用户是否至少提供了一个命令行参数。
- 通过`if(count < 0)`，我使用函数的特殊返回值来对错误做出反应。
- 通过`main()`中的`if(result)`，我检查转发的结果。

每种情况的处理方式不同：

- `countWords` 返回一个计数（始终为零或更大），所以在 `countWords` 中返回值 `-1`；通过特殊值 `-1` 向调用者指示错误。
- 在 `process` 中通过 `if(count < 0)` 检查返回值，可能会进行特殊处理，最后通过 `return result;` 向外传递。
- `process` 中 `if(args.size() == 0)` 的测试可以直接通过 `return false;` 返回失败。
- 而如果某处发生错误，它最终会到达 `bool result = process();`，甚至通过 `main()` 中的 `return 1;` 传递给程序的调用者。

如果你以这种方式处理错误，你就是在通过函数调用传递错误状态，使用的载体是 `bool` 或 `int` 代码，或者——在极端情况下——是单独的错误对象。

我想快速解释一下 `process` 的参数 `{argv+1, argv+argc}`：函数 `process` 接收一个 `const vector<string>&` 作为参数。然而，给定的参数是一个由 `const char*` 组成的初始化列表。编译器可以利用 `vector` 和 `string` 的相应构造函数毫无问题地完成转换。

为了向你展示如何使用这个程序，下面是在不同情况下它的反应：

```text
$ touch empty_file
$ echo "Two words" > two_words.txt
$ ./28-codes.x
Command line argument missing
An error occurred.
$ ./28-codes.x empty_file two_words.txt 28-codes.cpp
empty_file: 0
two_words.txt: 2
28-codes.cpp: 252
$ ./28-codes.x two_words.txt DOES_NOT_EXIST.txt empty_file
two_words.txt: 2
DOES_NOT_EXIST.txt: Error opening DOES_NOT_EXIST.txt
empty_file: 0
Error!
An error occurred.
```

首先，使用 `touch` 和 `echo` 准备两个文件，内容分别为零个和两个单词。当你运行不带参数的 `./28-codes.x` 时，你会得到一个错误。使用三个参数（`empty_file ...`）运行则正常工作，并统计每个文件中的单词数。当使用 `DOES_NOT_EXIST.txt` 运行时，不存在的文件名会导致错误。

无论你实现什么——错误码、异常，还是两者都不用——函数在出错时的行为都是接口的一部分。作为接口的一部分，你必须像记录返回值、参数和常规行为一样记录它。在标准库中，你会看到许多如何完成这种文档化的示例。

### 10.2 什么是异常？

你无法回避对错误状态的那些真正重要的检查：你必须教会计算机什么是错误，什么不是。但是传递代码既乏味又冗长。你可以用另一种方法集中处理在多个地方出现的错误。

你可以不生成并传递错误码，而是*触发异常*——换句话说，*抛出异常*。

```cpp
// https://godbolt.org/z/j8abxvvyo
#include <iostream>              // cout, cerr
#include <vector>
#include <string>
#include <fstream>               // ifstream
#include <stdexcept>             // invalid_argument
using std::vector; using std::string; using std::cout; using std::ifstream;
size_t count(const string& filename) { // 0 or?
    std::ifstream file{};        // create unopened
    // register for exceptions
    file.exceptions(ifstream::failbit | ifstream::badbit);
    file.open(filename);         // could throw an exception
    size_t count = 0;
    string word;
    file.exceptions(ifstream::badbit); // EOF no longer an exception
    while(!file.eof()) {         // not at the end yet?
        file >> word; ++count;
    }
    return count-1;               // one more word was read at EOF
}

void process(const vector<string>& args) {
    if(args.size() == 0) {       // process expects parameters
        throw std::invalid_argument("Command line argument missing"); // trigger
    } else {
        for(const string filename : args) {
            cout << filename << ": " << count(filename) << std::endl;
        }
    }
}
```

