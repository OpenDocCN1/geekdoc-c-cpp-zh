

让第一个函数为 get_board_size。
基本上，你需要询问用户要使用的棋盘大小，然后返回该大小。
size 将是 2 个数字：行数和列数。因为你
需要返回 2 个值，你将使用传引用方式。

以及要使用的行数 (a)。这些将通过传引用 (b) 返回给调用程序。

## STUBS AND SCAFFOLDS

函数本身的代码非常
简单：你只需输出几个
提示并读取列数

记住，每当你写一段
代码时，你应该尽量确保它在继续之前是稳定的。当你完成时
对其运行单元测试，
测试它是否受支持。所以，你
你设置对函数的调用在
主程序中并输出它返回的内容 (c)。
这样做时，确认一切正常。

注意你打算写的并非所有函数
都有代码。
这种方法——构建一个实际上什么都不做的函数——在开发中相当常见
你可能知道
程序需要此函数并且
需要从
你正在处理的代码中调用该函数，但你
还没有真正编写其他
函数。你可以被调用
并返回正确类型的某个值，这被称为 stub。

// Program 15_1_2
// Connect 4 Program - stage 2
#include <iostream>
#include <vector>
using namespace std;

void get_board_size(int columns, int &rows) {
    /* Get size of board from user */
    cout << "How many columns should the board have?";
    cin >> columns;
    cout << "How many rows should the board have?";
    cin >> rows;
}

void initialize_board() {
    /* Initialize the board itself, to empty squares */
}

void initialize_game() {
    /* Initialize the entire game */
}

int main() {
    int a, b;
    get_board_size(a, b);
    cout << "Returned " << a << " columns and " << b << " rows." << endl;
}
```

同样，有时你需要一些
其他数据或操作来
执行但你并不一定想
在你正在处理的
被调用之前编写所有必要的代码。在这种情况下，你可以创建一个
scaffold，它会设置好
你关心的一个函数
并且可以被测试。

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_172_0.png)

现在你可以继续填充其他函数。例如，你可以填充 initialize_board 函数，它将需要接收行数和列数并返回一个棋盘。在这种情况下，棋盘将是一个向量组成的向量。每个列将有一个向量，因此是一个向量集合。棋盘的每个元素将为 0 以表示该位置为空 (d)。

不得不为 get_board_size 和 initialize_board 函数创建函数。

并且从那里继续，你可以填充与你在自上而下设计中创建的层次结构中每个节点对应的所有其他函数。你希望逐步开发——一个函数并彻底测试它，然后再继续编写下一个函数。

注意 initialize_game 函数调用了创建的另外两个函数。它调用 get_board_size 来获取行数和列数，然后调用 initialize_board 来实际创建空棋盘 (e)。

整个程序长 200 行——但这 200 行分布在许多不同的函数中。没有单个函数过大，每个函数都应该可以理解。

如果你想以不同的顺序做这件事——也就是说先写 initialize_game 函数——那么你已经

花点时间查看这段代码，看看它如何反映了大纲程序的自上而下设计。

> 要查看整个程序，请访问 TheGreatCourses.com/CPlusPlus。

// Program 15_1_3
// Connect 4 Program - stage 3
#include <iostream>
#include <vector>
using namespace std;
void get_board_size(int columns, int rows) {
    /* get_size of board from user */
    cout << "How many columns should the board have? ";
    cin >> columns;
    cout << "How many rows should the board have? ";
    cin >> rows;
    return board;
}
```

```
vector<int> initialize_game() {
    /* initialize the board itself */
    vector<int> column(rows, 0);
    vector<vector<int>> board(columns, column);
    return board;
}
```

```
get_board_size(c, r);
return initialize_board(c, r);

int main() {
    vector<vector<int>> board;
    board = initialize_game();
}
```

自上而下设计与函数定义结合得非常容易，使得原本具有挑战性的问题变得更加易于处理。

## // BOTTOM-UP DESIGN

自下而上设计的思想是利用你已知的现有事物并将它们组合成新的事物。然后，你可以利用它来做一些工作，沿着层次结构向上，使用单个函数作为构建块。

在这个简单的示例中，你可能在文字处理器中使用，你有一个函数 pos_first，它可以找到字符串中某个单词的第一次出现 (f)。你还有另一个函数 replace_string，它可以把字符串的一个部分替换为另一个字符串 (g)。你可以查看这些函数并意识到你可以用它们来替换一个单词的第一次出现为另一个单词。所以，你会创建一个新的函数 search_and_replace，它将替换更大的字符串 (h)。

// Program 15_2_1
// Example of bottom-up program - string processing (incomplete) -
Stage 1
#include <iostream>
#include <string>
using namespace std;

int pos_first(string& string_to_find, string& string_to_search) {
    /* Returns the first position of string_to_find in string_to_search,
    or -1 if it is not in there */
    // Code Here
}

void replace_string(string& string_to_modify, int start_pos, int end_pos, string& string_to_insert) {
    /* Inserts string_to_insert into string_to_modify, replacing anything
    in positions start_pos to just BEFORE end_pos */
    // Code Here
}

bool search_and_replace(string& string_to_modify, string& old_string, string& new_string) {
    /* Replace first occurrence of old_string with new_string and returns
    true, or returns false if it did not find old_string */
}

int main() {
    // Code Here
}
```

替换你根据已有内容填写 search_and_replace 的代码？

以下是该函数可能被编写的方式。你可以使用 pos_first 函数来找到你要搜索的字符串的位置 (24)。如果未找到，你返回 false(i)；否则，你确定字符串将在何处结束 (28)。最后，你可以使用 replace_string 来替换字符串并返回 true(j)。

并且你可以建立在之上创建另一个层级。你可以将刚刚创建的函数与一个循环结合起来，这将让你用另一个单词替换字符串中每个单词的出现。你可以创建一个新的函数，从你创建的函数构建而来，它只是重复循环直到它返回 false——也就是说，直到它找不到用于更长字符串的字符串 (k)。

自下而上设计是向软件添加功能的绝佳方式。当你有一个产品已经可以做一件事，然后有一个新想法可以与之整合时，你可以创建一个新的软件产品，加入额外的功能。

自下而上设计倾向于关注用现有资源能做什么，而不是自上而下哲学中特定问题是如何解决的。因此，自下而上的实现往往在更广泛的应用范围内有用。这使得自下而上方法成为开发相关函数库的好方法——一组函数，你可能在多个领域中使用。

// Program 18_2
// Example of bottom-up program string processing (incomplete) - Stage 3
#include <iostream>
#include <string>
using namespace std;

pos_first(string& string_to_find, string& string_to_search) {
    // Returns the first position of string_to_find in string_to_search,
    // or -1 if it is not there *
    return -1;
}

void replace_string(string& string_to_modify, int start_pos, int end_pos, string& string_to_insert) {
    string_to_insert
    // Inserts string_to_insert into string_to_modify, replacing anything
    in positions start_pos to BEFORE end_pos *
}

bool search_and_replace(string& string_to_modify, string& old_string, string& new_string) {
    int start_pos = pos_first(old_string, string_to_modify);
    if (start_pos == -1) {
        return false;
    }
    int end_pos = start_pos + old_string.size();
    replace_string(string_to_modify, start_pos, end_pos, new_string);
    return true;
}

void search_and_replace_all(string& string_to_modify, string& old_string, string& new_string) {
    // Replaces every occurrence of old_string with new_string and returns
    // or false if it did not find old_string *
    while (search_and_replace(string_to_modify, old_string, new_string));
}

int main() {
    // Code Here
}
```

Lecture 15 | Functions in Top-Down and Bottom-Up Design

