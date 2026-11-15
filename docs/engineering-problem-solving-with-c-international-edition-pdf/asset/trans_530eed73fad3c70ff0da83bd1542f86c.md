

#include<iostream>//Required for cout, cin
#include<stack>//Required for stack, push(), top(), empty()
using namespace std;
int main()
{
    // Declare objects.
    stack<int> astack;
    int ivalue;
    cout << " enter integer values. 's' to stop\n";
    // While valid data, read value and add to stack.
    while(cin >> ivalue)
    {
        astack.push(ivalue);
    }
    // Print values to standard output.
    cout << " Elements from the stack: \n";
    while(!astack.empty())
    {
        // Access the top element.
        cout << astack.top() << endl;
        // Remove top element from the stack.
        astack.pop();
    }
    return 0;
}

如果从键盘输入数据 35 18 21 14 s，程序将生成以下输出：

```
Enter integer values. 's' to stop
Elements from the stack:
14
21
18
35
```

请注意，元素的顺序已被颠倒。

## 队列类

C++ STL 包含 `queue` 类，它提供了基于对象的队列实现。要使用 `queue` 类，必须包含编译器指令 `#include<queue>`。定义队列时，必须指定队列中元素的数据类型。以下语句定义了一个名为 aqueue 的空整数队列：

```
queue<int> aqueue;
```

| 成员函数 | 描述 |
|---|---|
| empty() | 如果队列为空则返回 true，否则返回 false。 |
| pop() | 从队列中移除前端元素。不返回值。 |
| push(value) | 将值添加到队列前端。 |
| size() | 返回队列中元素的数量。 |
| top() | 返回队列前端元素的值。该元素不会从队列中移除。 |

表 9.4 列出了队列类的一些成员函数。以下程序说明了这些函数中几个的用法：

```
/*------------------------------------------------------------*/
/* Program chapter9_12 */
/* */
/* This programs creates a queue of data entered from */
/* standard input. */
/* The queue is printed to standard output. */
/*------------------------------------------------------------*/
#include<iostream>//Required for cout, cin
#include<queue>//Required for queue, push(), empty(), top()
using namespace std;
int main()
{
// Declare objects.
queue<int> aqueue;
int ivalue;
cout << "enter integer values. 's' to stop\n";
// While valid data, read value and add to back of queue.
while(cin >> ivalue)
{
aqueue.push(ivalue);
}
// Print values to standard output.
cout << "Elements in the queue: \n";
while(!aqueue.empty())
{
// Access element at the front of the queue.
cout << aqueue.top() << endl;

// Remove element from the front of the queue.
aqueue.pop();
}
return 0;
}
```

如果从键盘输入数据 35 18 21 14 s，程序将生成以下输出：

```
Enter integer values. 's' to stop
Elements in the queue:
35
18
21
14
```

## 9.9 应用问题求解：文本文件的词汇索引

文本文件的词汇索引是文本文件中唯一单词的字母列表。以下是前一句的词汇索引：

- a
- an
- alphabetical
- concordance
- file
- in
- is
- list
- of
- text
- the
- unique
- words

编写一个程序，提示用户输入输入文本文件和输出文件的名称。构建文件的词汇索引，并将词汇索引打印到输出文件中。

### 1. 问题描述

构建文本文件的词汇索引。将词汇索引以及文本文件中唯一单词的计数写入输出文件。

### 2. 输入/输出描述

以下图显示程序的输入是一个文本文件，输出是文本文件的词汇索引及唯一单词的计数。我们将使用 list 类来定义一个列表，列表中的每个元素类型为 string。

![](img/f2bfa570e453b020c16e048c79a3ea0e_494_0.png)

### 3. 手动示例

假设我们的文本文件仅包含以下文本：

```
A concordance of a text file is an alphabetical list of
the unique words in the text file.
```

我们的程序将生成以下输出文件：

```
a
are
13
distinct
words
in
the
text
file:
an
alphabetical
concordance
file
in
is
list
of
text
the
unique
words
```

### 4. 算法开发

我们首先开发分解大纲，将解决方案分解为一系列顺序步骤：

分解大纲

- 1. 打开输入和输出文件。
- 2. 从输入文件读取一个单词。
- 3. 如果单词不在列表中，则插入该单词。
- 4. 对唯一单词列表进行字母排序。
- 5. 将列表的大小和内容写入输出文件。

分解大纲中的步骤 2 涉及一个循环，该循环一次读取文本文件的一个字符，直到遇到非字母字符。非字母字符将标志着单词的结束。除了用作单词之间的分隔符外，所有非字母字符都将被忽略。所有字母字符都将转换为小写。我们将使用一个函数来执行此任务。步骤 3 要求如果单词不在列表中，则插入该单词。我们将使用一个利用列表类成员函数的函数。步骤 4 涉及按升序对列表进行排序。我们将使用通用 sort() 函数。由于列表可能很长，步骤 5 将每行打印三个单词。我们将使用一个函数来执行此任务。伪代码中的细化如下：

### 伪代码中的细化

```
main: open input file
      get_word(istream,string)
      while(string size in not 0)
        insert_word(list,string)
        get_word(string)
      sort(list)
      print size of list
      display_list(ostream,list)
get_word(istream,string):
      clear string
      read a character
      while(not end of file and character is not alpha)
        read next character
      while(not end of file and character is an alpha)
        append lower case character to string
        input next character
insert_word(list, string)
      if(string is not in list)
        insert string
display_list(ostream,list)
      set counter to 0
      while(not end of list)
        print list element
        increment counter
        if(counter mod 3 is zero)
          print newline
```

伪代码中的步骤现在已足够详细，可以转换为 C++ 代码：

/*...................................................................*/
/* Program chapter9_13                                          */
/* This program builds a concordance of a text file.            */
/*                                                              */
#include <fstream>//Required for ifstream, ofstream
#include <string>//Required for string
#include <cctype>//Required for isalpha(), tolower()
#include <iomanip>//Required for setw()
#include <list>//Required for list, sort(), begin(), end()
#include <algorithm>//Required for find()
using namespace std;

// Function prototypes.
void get_word(ifstream& in_stream, string& w);
void insert_word(string word, list<string>& wordlist);
void display_list(ostream& out_stream, list <string> wordlist);

int main()
{
    // Declare objects.
    ifstream in_stream;
    ofstream out_stream;

    string infile, outfile;//filenames
    string word; // string to hold current word

    // Prompt for filenames and open files
    cout << "Enter the input file name ";
    cin >> infile;
    cout << "Enter the output file name ";
    cin >> outfile;

    in_stream.open(infile.c_str());
    if(in_stream.fail())
    {
        cout << "Fail to open file " << infile << endl;
    }
    else
    {
        out_stream.open(outfile.c_str());
        list <string> wordlist;
        list<string>::iterator iter;
        get_word(in_stream, word); // get a word

        // While non-empty word was returned
        while(word.size())
        {
            insert_word(word, wordlist);
            get_word(in_stream, word); // get a word
        }

        wordlist.sort();
        out_stream << "There were " << wordlist.size()
                   << " distinct words. \n";
        out_stream << "\nHere is the ordered list of words\n";
        display_list(out_stream,wordlist);
    }//end else

    return 0;
/*--------------------------------------------------------------*/
```

