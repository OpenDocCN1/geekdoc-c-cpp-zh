

## STEP 6

代码的工作方式与你预期的一样，但如果想在用户输入数字 30 时显示某些内容怎么办？试试这个：

```
{
    int num;
    cout << "Enter a number: ";
    cin >> num;
    if ( num < 30 )
    {
        cout << "The number is less than 30!" << endl;
    }
    else if ( num > 30 )
    {
        cout << "The number is greater than 30!" << endl;
    }
    else if ( num == 30 )
    {
        cout << "The number is exactly 30!" << endl;
    }
    return 0;
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_134_0.png)

## STEP 7

代码中的新增加部分被称为嵌套的 if... else 语句。这使你能够检查多个条件。在此例中，如果用户输入小于 30、大于 30 或正好是 30 的数字，会向他们呈现不同的结果。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_134_1.png)

## STEP 8

你可以更进一步，创建一个双人数字猜谜游戏。首先创建变量：

```
int num, guess, tries = 0;
cout << "***** Two-player number guessing game *****" << endl;
cout << "\nPlayer One, enter a number for Player Two to guess: " << endl;
cin >> num;
cout << string(50, '\n');
```

## STEP 9

`cout << string(50, \n)` 行会清除屏幕，这样玩家二就看不到输入的数字。现在你可以创建一个 do... while 循环，结合 if... else：

```
do
{
    cout << "\nPlayer Two, enter your guess: ";
    cin >> guess;
    tries++;
    if (guess > num)
    {
        cout << "\nToo High!\n" << endl;
    }
    else if (guess < num)
    {
        cout << "\nToo Low!\n" << endl;
    }
    else if (guess == num)
    {
        cout << "Well done! You got it in " << tries << " guesses!" << endl;
    }
} while (guess != num);
return 0;
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_134_2.png)

## STEP 10

找一个第二名玩家，然后构建并运行代码。玩家一输入要猜的数字，然后玩家二可以猜任意多次直到猜对。想让它更难吗？也许使用小数。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_134_3.png)

## Working with Code

![](img/2f9c26fcf758b5bc56897d9c75b6347f_136_0.png)

到现在为止，你应该已经掌握了在 Python 和 C++ 中编程的基本构建模块。你可以创建代码、存储数据、向用户提问、为他们提供选择并重复函数直到它们为真并提供正确的输出。那么接下来呢？

本节最后将介绍 Python 和 C++ 初学者常犯的一些编码错误，以及你下一步可以去哪里继续你的编程冒险。

## 138 Common Coding Mistakes

## 140 Beginner Python Mistakes

## 142 Beginner C++ Mistakes

## 144 Where Next?

## Common Coding Mistakes

当你开始做新事物时，难免会犯错误，这纯粹是由于经验不足，而这些错误本身就是很好的老师。然而，即使是专家也会偶尔出现失误。关键是要尽可能从中学习。

## X=MISTAKE, PRINT Y

程序员需要注意的陷阱有很多，太多无法在此全部列出。能够识别错误并修复它，是你开始进入更高级领域的时候。

## SMALL CHUNKS

能够像《黑客帝国》电影中的尼奥那样工作会很棒。只需询问，你的操作员就会把它加载到你的记忆中，你瞬间就能了解该主题的一切。可惜我们做不到。第一个主要陷阱是有人试图学得太多、太快。所以请以小块的方式学习编码，并慢慢来。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_137_0.png)

## EASY VARIABLES

对变量进行有意义的命名是消除常见编码错误的关键。使用字母表上的字母是可以的，但当代码指出 x 变量有问题时，并不难将变量命名为 lives、money、player1 等等。

```
var points = 1023;
var lives = 3;
var totalTime = 45;
write("Points: "+points);
write("Lives: "+lives);
write("Total Time: "+totalTime+" secs");
--------------------------------------------------
var totalScore = 0;
write("Your total Score is: "+totalScore);
```

## //COMMENTS

使用注释。这是一个简单的概念，但在你下次查看代码时，注释可以节省很多麻烦。插入注释行可以帮助你快速筛选出导致问题的代码段；如果需要回顾旧代码也很有用。

```
orig += 2;
target += 2;
--n;
}
endif
if (n == 0)
return;
//
// Loop unrolling. Here be dragons.
//
// (n & (~3)) is the greatest multiple of 4 n
// In the while loop ahead, orig will move over
// increments (4 elements of 2 bytes).
// end marks our barrier for not falling out
char const * const end = orig + 2 * (n & ~3);
//
// See if we’re aligned for writing in
if (definedi amd64 ) || defined ( x
```

## PLAN AHEAD

虽然某天早上醒来决定编写一个经典的文本冒险游戏很棒，但在没有良好计划的情况下并不总是切实可行。无需太多思考和计划就可以编写小段代码，但更长、更深入的代码需要一个良好的工作计划来坚持并帮助排除错误。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_137_1.png)

## USER ERROR

用户输入往往是代码中令人瘫痪的错误。例如，当用户应该输入年龄的数字时，却用字母输入。用户常常会输入太多内容，导致某些内部缓冲区溢出，从而使代码崩溃。注意那些用户输入，并清楚地说明他们需要做什么。

```
Enter an integer number
aswdfdsf
You have entered wrong input
8
You have entered wrong input
"!""!"!
You have entered wrong input
sdfedf213213123
You have entered wrong input
123234234234234234
You have entered wrong input
12
the number is: 12

Process returned 0 (0x0)   execution time : 21.495 s
Press any key to continue.
```

## BACKUPS

始终备份你的工作，并为所做的任何更改做二次备份。如果有良好的备份可以恢复，那么错误是可以纠正的，尤其是在出现问题时。这样更容易从你离开的地方继续，而不是从头开始。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_138_0.png)

## RE-INVENTING WHEELS

你很容易花费数天时间试图弄清楚一段代码以实现给定结果，这令人沮丧且常常浪费时间。虽然自己解决问题同样令人满意，但通常同样的代码在互联网上的某个地方已经存在。不要试图重新发明轮子，看看是否有人已经先做过。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_138_1.png)

## SECURE DATA

如果你编写代码来处理用户名和密码或其他敏感数据，那么请确保数据不是明文。学习如何创建一个函数来加密敏感数据，然后再将其输入到可能传输或存储它的例程中，以免有人能够查看它。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_138_2.png)

## HELP!

寻求帮助是大多数人过去都挣扎过的事情。我们问的人会嘲笑我们吗？我是在浪费大家的时间吗？有人默默忍受是一个常见的错误。然而，只要你以正确的方式提问，遵守任何论坛规则并保持礼貌，你的问题就不会愚蠢。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_138_3.png)

## MATHS

如果你的代码进行多次计算，那么你需要确保其背后的数学是正确的。有成千上万的实例表明，程序因糟糕的数学编码而提供错误数据，这可能产生灾难性的后果，具体取决于代码的用途。总之，请仔细检查你的代码方程。

```
set terminal x11
set output

max = 5
max = 500

complex (x, y) = x + (0, 1) * y + (0, 1)
mandel (x, y, z, n) = (abs (z) > max) || (n==0) ? n : mandel (x, y, z + complex (x, y), n - 1)

set xrange [-0.5:0.5]
set yrange [-0.5:0.5]
set samples 200
set size square
set pm3map
set palette
s = 0
plot mandel(x,-0.100,-0.100,complex(x,y),0) notitle
```
