

一个常见的测试用例思路是设置一个单元测试，即针对某个特定函数运行的测试用例。基本上，你有一个函数的输入，然后有一些你期望看到的输出。当你编写一个函数时，运行多个单元测试以确保函数按预期工作是个好主意。

这个程序旨在让用户输入一些文本，然后它会检查该文本是否为回文（a）。它通过调用函数 is_palindrome（b）来实现这一点，该函数会调用 remove_spaces 来从文本中删除空格（c）。然后，它会遍历字符的前半部分（21），将其与另一侧的对应字符进行比较（22）。如果全部匹配，则为回文；否则不是。

由于我们关注的是 is_palindrome 函数，你可以将其视为对 is_palindrome 函数本身的单元测试。你希望为 is_palindrome 函数提供一个输入并检查输出是否正确。

对于你的单元测试，你将检查你的函数是否适用于一个非常简单的测试字符串：aaa。这应该是一个回文，但当你运行程序检查它时，你得到了错误的结果！

```
// Program 14_1
// Example program to debug contains an error!
#include <iostream>
#include <string>
using namespace std;
string remove_spaces(string s) {
    string ret = "";
    int i;
    for (i = 0; i < s.size(); i++) {
        if (s[i] != ' ') {
            ret += s[i];
        }
    }
    return ret;
}
```

```
bool is_palindrome(string s) {
    string no_spaces = remove_spaces(s);
    bool could_palindrome = true;
    for (int i = 0; i < no_spaces.size() / 2; i++) {
        if (no_spaces[i] != no_spaces[no_spaces.size() - i]) {
            could_palindrome = false;
        }
    }
    return could_palindrome;
}
```

```
int main() {
    cout << "This will tell you whether certain text is a palindrome. Enter some text:";
    cout << endl;
    string user_input;
    getline(cin, user_input);
    if (is_palindrome(user_input)) {
        cout << "It is a palindrome!" << endl;
    } else {
        cout << "It's not a palindrome." << endl;
    }
}
```

## STEP 2: NARROW

现在你有一个可以用来调试程序的错误，下一步调试过程就是找出代码中失败发生的位置。这就是 Visual Studio（在 PC 上）或 Xcode（在 Mac 上）中的调试器可以派上用场的地方。

然后，你需要逐步缩小程序中可能发生错误范围。在上一个已知正常点和第一个已知错误点之间选择程序中的另一个点，并分析内存中的变量是否正确。如果该点存在问题，那么你可能会将错误点移动到那里。目标是尽可能多地逐步缩小错误发生的位置。

当你运行程序时，似乎计数的数据是正确的。你确实在字符串中这样做了，并且 remove_spaces 没有引入任何错误。因此，你可以假设到那一点为止，一切都很好。

调试器只能帮助你了解程序中发生了什么；它不会为你解决问题，甚至不会告诉你错误发生在哪里。

你同样可以检查返回前将要返回的值。如果你添加另一行输出，在返回语句之前打印将要返回的值，你可以检查问题是在 is_palindrome 函数返回之前还是之后。

你的目标是找到程序中给出错误结果的第一行。通常，这意味着内存中的某个变量出错了。

在这种情况下，你知道程序开始时一切正常，末尾存在问题，所以你应该检查中间的一个点。

```
// Code here
int age;
age = birth_year-current_year;
-10
ageage
memory
Wrong value
Gives incorrect result
```

你也可以通过使用打印调试来简单地打印语句：在 remove_spaces 函数返回后插入一行以输出其中的内容。

| 26 | cout << "About to return:" << could_be_palindrome<<endl; |
| 27 | return could_be_palindrome; |

如果你没有调试器，你始终可以使用输出语句在途中打印出来。

| 19 | string no_spaces = remove_spaces(s); |
| 20 | cout << "String with no spaces:" << no_spaces << endl; |
| 21 | bool could_be_palindrome = true; |

果然，当你运行程序时，它返回 0，即 false，这是不正确的。所以，你知道在 for 循环之前一切正常，而之后则出错。你需要进一步缩小范围。

为了缩小错误，你应该从你知道一切都正常的程序点开始。最坏的情况下，那将是程序的第一行和最后一行！但在许多情况下，你有更好的想法——通常是在调用你刚编写的新函数之前和之后。

在调试器中，你可以在循环开始处设置断点，以确保你就在那里。查看变量时，could_be_palindrome 为 true，正如它应有的那样。

## STEP 3: IDENTIFY

could_be_palindrome true

逐步执行第一行，你可以检查并看到 i 的值为 0，正如预期的那样。所以，到目前为止，一切似乎都很好。

现在你知道错误发生的位置，下一步是识别错误源。源不仅仅是代码中出错的那一行；它是导致该行代码出错的原因。是简单的拼写错误，还是程序根本逻辑上的错误？

再逐步执行一行，你已经进入了 false，这是不对的！对于这个输入，你不应该到达这一点。

关键点是，在尝试修复它之前，你需要了解是什么导致了这个错误。如果是像拼写错误这样基本错误，那么修复起来会很简单。但如果它是程序中的逻辑错误，你需要确保你真正理解出了什么问题以及为什么。调试过程中没有捷径可以绕过这部分。

这意味着错误必须发生在前一行——你在比较 no_spaces[i] 与 no_spaces[no_spaces] 的地方。你可以检查这些值：i 为 0，正如预期的那样，而 no_spaces.size(-1) 为 3。这是不对的。你希望查看字符串的最后一个元素，它应该是元素 2，而不是 3。

在回文程序中，对于一个 3 个字符的字符串，你试图将字符 0 与字符 3 进行比较。问题是最后一个字符不会从字符串的开头开始；它实际上是 size 减 1，所以你需要将字符 0 与字符 2 进行比较。因此，在这种情况下，错误来自用于比较的公式。

```
bool is_palindrome(string s) {
    string no_spaces = remove_spaces(s);
    for (int i = 0; i < no_spaces.size() / 2; i++) {
        if (no_spaces[i] != no_spaces[no_spaces.size() - 1 - i]) {
            return false; // elapsed here
        }
    }
    return true;
}
```

## STEP 4: FIX

一旦你知道了问题，下一步就是修复错误。这可能很简单——只是正确选择变量名或更改一个字符。

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_162_0.png)

这可能涉及重写一行代码。或者你可能在方法上是错误的，最好的修复方法是扔掉整个程序并重新开始！

在这里，bug 很简单：你从字符串末尾的元素编号中减去 1。当 i 为 0 时，当 i 为 1 时，你应该与 size(-1)-2 进行比较，等等。

- if (no_spaces[i] != no_spaces[no_spaces.size()-1]) {

## STEP 5: RETEST

一旦错误被修复，你需要重新测试一切。目标不仅仅是证明你所做的修复解决了你隔离和识别的问题。你还想确保在此期间没有破坏其他任何东西。如果你保存了所有测试，现在是重新运行它们并确保它们对之前正确的一切仍然给出正确结果——加上你刚刚修复的测试的时候！

当你现在在 aaa 上测试回文程序时，它返回回文。你可以检查其他测试：abc 不是回文；bob 是回文。程序现在似乎工作正常。

## STEP 6: CONSIDER

在调试完成之前，还有最后一步：你应该考虑代码中的错误是否可能有类似的错误。

当存在相同计算的不同版本时，错误往往会成倍增加。有时，人们会从一个地方复制代码到另一个地方并复制任何错误。其他时候，如果你的思路有误，你可能会在代码的其他部分犯同样的概念性错误。

关键是花时间思考你所做的修复是否也适用于其他地方。所以，并且修复你代码的那个部分。

对于回文程序，你应该思考：“我是否还有其他地方假设字符串一直到 size 而不是 size 输入？答案是否定的，所以你已经完成了调试。

```
// Program 14_2
// Example program to debug - fixed!
#include <iostream>
#include <string>
using namespace std;

string remove_spaces(string s) {
    string ret = "";
    int i;
    for (int i = 0; i < s.size(); i++) {
        if (s[i] != ' ') {
            ret += s[i];
        }
    }
    return ret;
}
```

```
bool is_palindrome(string s) {
    string no_spaces = remove_spaces(s);
    bool could_palindrome = true;
    for (int i = 0; i < no_spaces.size() / 2; i++) {
        if (no_spaces[i] != no_spaces[no_spaces.size() - 1 - i]) {
            could_palindrome = false;
        }
    }
    return could_palindrome;
}
```

```
int main() {
    cout << "This will tell you whether certain text is a palindrome." << endl;
    string string_input;
    getline(cin, user_input);
    if (is_palindrome(user_input)) {
        cout << "It is a palindrome!" << endl;
    } else {
        cout << "It's not a palindrome." << endl;
    }
}
```

Lecture 14 | Systematic Debugging, Writing Exceptions

