
*向玩家显示其已猜中神秘单词中的几个字母*
*获取玩家的下一个猜测*
*当玩家输入了已经猜过的字母时*
*获取玩家的猜测*
*将新猜测加入已用字母集合*
*如果猜测的字母在神秘单词中*
*告诉玩家猜测正确*
*用新字母更新目前已猜出的单词*
*否则*
*告诉玩家猜测错误*
*增加玩家错误猜测的次数*
*如果玩家错误猜测次数过多*
*告诉玩家他或她已被吊死*
*否则*
*祝贺玩家猜出了神秘单词*

尽管这段伪代码没有涵盖我将要编写的每一行 C++ 代码，但我认为它很好地描述了我需要完成的任务。然后我就开始编写程序。

## 设置程序

和往常一样，我先写一些注释，并包含所需的头文件。

```
// Hangman
// The classic game of hangman

#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
#include <ctime>
#include <cctype>

using namespace std;
```

注意，我包含了一个新文件——cctype。它是标准库的一部分，其中包含将字符转换为大写的函数，这样在比较单个字符时，我就可以进行“同等级别”的比较（大写对大写）。

## 初始化变量和常量

接下来，我启动 main() 函数，并为游戏初始化变量和常量。

```
int main()
{
    //setup
    const int MAX_WRONG = 8;  //maximum number of incorrect guesses allowed

    vector<string> words;  //collection of possible words to guess
    words.push_back("GUESS");
    words.push_back("HANGMAN");
    words.push_back("DIFFICULT");

    srand(static_cast<unsigned int>(time(0)));
    random_shuffle(words.begin(), words.end());
    const string THE_WORD = words[0];            //word to guess
    int wrong = 0;                               //number of incorrect guesses
    string soFar(THE_WORD.size(), '-');          //word guessed so far
    string used = "";                           //letters already guessed

    cout << "Welcome to Hangman. Good luck!\n";
```

MAX_WRONG 是玩家可以做出的最大错误猜测次数。words 是一个由候选猜测单词组成的 vector。我使用 random_shuffle() 算法对 words 进行随机化处理，然后将 vector 中的第一个单词赋给 THE_WORD，即玩家必须猜出的神秘单词。wrong 是玩家已经做出的错误猜测次数。soFar 是玩家目前已猜出的单词。soFar 初始是一串破折号——神秘单词中每个字母对应一个破折号。当玩家猜出神秘单词中的一个字母时，我会用该字母替换相应位置的破折号。

## 进入主循环

接下来，我进入主循环，该循环会一直持续，直到玩家错误猜测次数过多或猜出了单词。

```
//main loop
while ((wrong < MAX_WRONG) && (soFar != THE_WORD))
{
```

```
cout << "\n\nYou have " << (MAX_WRONG - wrong);
cout << " incorrect guesses left.\n";
cout << "\nYou've used the following letters:\n" << used << endl;
cout << "\nSo far, the word is:\n" << soFar << endl;
```

## 获取玩家的猜测

接下来，我获取玩家的猜测。

```
char guess;
cout << "\n\nEnter your guess: ";
cin >> guess;
guess = toupper(guess); //make uppercase since secret word in uppercase
while (used.find(guess) != string::npos)
{
    cout << "\nYou've already guessed " << guess << endl;
    cout << "Enter your guess: ";
    cin >> guess;
    guess = toupper(guess);
}

used += guess;

if (THE_WORD.find(guess) != string::npos)
{
    cout << "That's right! " << guess << " is in the word.\n";
    //update soFar to include newly guessed letter
    for (int i = 0; i < THE_WORD.length(); ++i)
    {
        if (THE_WORD[i] == guess)
        {
            soFar[i] = guess;
        }
    }
}
else
{
    cout << "Sorry, " << guess << " isn't in the word.\n";
    ++wrong;
}
```

我使用定义在 cctype 文件中的 toupper() 函数将猜测的字母转换为大写。这样做是为了在比对猜测字母与神秘单词中的字母时，能进行大写字母与大写字母的比较。

如果玩家猜了一个已经猜过的字母，我就让玩家重新猜测。如果玩家猜对了字母，我就更新目前已猜出的单词。否则，我告诉玩家该字母不在神秘单词中，并增加玩家的错误猜测次数。

## 结束游戏

此时，玩家要么已猜出单词，要么错误猜测次数已经超过限制。无论哪种情况，游戏都结束了。

```
//shut down
if (wrong == MAX_WRONG)
{
    cout << "\nYou've been hanged!";
}
else
{
    cout << "\nYou guessed it!";
}

cout << "\nThe word was " << THE_WORD << endl;

return 0;
}
```

我要么祝贺玩家，要么告诉他或她已被吊死的坏消息。然后我会揭示神秘单词。

## 本章小结

在本章中，你学习了以下概念：

- ■ 标准模板库（STL）是一个功能强大的编程代码集合，提供了容器、算法和迭代器。
- ■ 容器是允许你存储和访问同类型值集合的对象。
- - STL 中定义的算法可与容器一起使用，并提供处理对象组的常用函数。
- - 迭代器是标识容器中元素的对象，可以通过操作在元素之间移动。
- - 迭代器是充分利用容器的关键。许多容器成员函数都需要迭代器，STL 算法也需要它们。
- - 要获得迭代器引用的值，必须使用解引用运算符 (*) 对迭代器进行解引用。
- - vector 是 STL 提供的一种顺序容器。它的行为类似动态数组。
- - 遍历 vector 非常高效。在 vector 末尾插入或删除元素也非常高效。
- - 在 vector 中间插入或删除元素可能效率较低，尤其是在 vector 很大的情况下。
- - 伪代码介于英语和编程语言之间，用于规划程序。
- - 逐步细化是一个重写伪代码以使其能够投入实现的过程。

## 问题与解答

问：为什么 STL 很重要？

答：因为它节省了游戏程序员的时间和精力。STL 提供了常用的容器类型和算法。

问：STL 快吗？

答：绝对快。STL 经过数百名程序员的精心打磨，在每个支持的平台上都尽可能挖掘出最高性能。

问：什么时候应该使用 vector 而不是数组？

答：几乎总是如此。vector 高效且灵活。它们确实比数组多占用一些内存，但这种权衡几乎总是值得的。

问：vector 和数组一样快吗？

答：访问 vector 元素可以像访问数组元素一样快。另外，遍历 vector 也可以像遍历数组一样快。

问：如果我可以对 vector 使用下标运算符，为什么还需要迭代器？

答：有几个原因。第一，许多 vector 成员函数需要迭代器（insert() 和 erase() 就是两个例子）。第二，STL 算法需要迭代器。第三，大多数 STL 容器不能使用下标运算符，所以你迟早都要学会使用迭代器。

问：访问 vector 元素的最佳方式是什么——通过迭代器还是通过下标运算符？

答：这要看情况。如果你需要随机访问元素，那么下标运算符是最自然的选择。如果你需要使用 STL 算法，那么你必须使用迭代器。

问：那遍历 vector 的元素呢？我应该使用下标运算符还是迭代器？

答：两种方法都可以。不过，使用迭代器的一个优点是，它能让你灵活地用另一个 STL 容器（如 list）替换 vector，而不需要改动太多代码。

问：为什么 STL 定义了不止一种顺序容器类型？

答：不同的顺序容器类型有不同的性能特性。它们就像工具箱里的工具；每种工具最适合不同的工作。

问：什么是容器适配器？

答：容器适配器基于 STL 顺序容器之一；它们代表标准的计算机数据结构。虽然它们不是正式的容器，但它们的外观和使用感觉与容器并无二致。

问：什么是栈？

答：一种数据结构，其元素的移除顺序与添加顺序相反。这意味着最后添加的元素是第一个
