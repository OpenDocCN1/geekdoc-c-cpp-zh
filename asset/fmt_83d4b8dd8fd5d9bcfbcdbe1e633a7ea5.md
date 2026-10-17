
```cpp
//10.2 - Minefield - Mark Lee
#include <iostream>
#include <exception>
#include <string>
#include <vector>
#include <cstdlib>
#include <ctime>

using std::string;
using std::vector;
using std::rand;
using std::time;

class StepOnMine ( ( {});
class FailedDisarm ( {});
class MineField {
    vector<bool> minefield;

    // 存储玩家去过的地方
    vector<bool> beenThere;

    // 玩家当前位置
    int location;

    int menu(string choices[], int numChoices)
    {
        using std::cout;
        using std::cin;

        int choice;
        do {
            for (int i = 0; i < numChoices; i++)
            {
                cout << i+1 << " " << choices[i] << "\n";
                cin >> choice;
            }
        } while (choice < 1 || choice > numChoices);
        return choice;
    }

public:
    MineField() // 4X4 雷区
    {
        srand((unsigned int)time(0));
        location = 0;
        for (int c = 0; c < 16; c++)
        {
            minefield.push_back(false);
            beenThere.push_back(false);
        }
        for (int i = 0; i < 10; i++) // 放置10个随机地雷
            minefield[rand() % 15+1] = true;
        beenThere[0] = true;
    }

    bool isAMine(int location)
    {
        return minefield[location];
    }

    string draw()
    {
        string s;
        for (int i = 0; i < 4; i++)
        {
            for (int c = 0; c < 4; c++)
            {
                if (location == i*4+c)
                    s += 'p';
                else
                {
                    if (beenThere[i*4+c])
                        s += "X";
                    else
                        s += " ";
                }
            }
            s += '\n';
        }
        return s;
    }

    bool moreMines() {
        for (int i = 0; i < 16; i++)
            if (beenThere[i])
                return true;
        return false;
    }

    int Directions()
    {
        string options[4];
        options[0] = "North";
        options[1] = "East";
        options[2] = "South";
        options[3] = "West";
        return menu(options, 4);
    }

    int& place() { return location; }
    void goThere(int place) { beenThere[place] = true; }

    void Detonate()
    {
        using std::cout;
        cout << "You detonated the mine. Ka-boom!!!\n";
    }

    void disarm()
    {
        int temp = rand() % 2+1;
        if (temp-1)
            throw FailedDisarm();
    }
};

int main(void)
{
    using std::set_terminate;
    using std::cout;
    using std::cin;
    set_terminate(Detonate);
    MineField m; // 创建雷区
    string input;

    cout << "Welcome to the MineField!\n";
    cout << "You are part of the elite ";
    cout << "XJ7 team, to clear a deadly ";
    cout << "minefield of mines.";
    cout << "Only the best and brightest will ";
    cout << "survive a day in the minefield. ";
    cout << "Compile this program, and see if ";
    cout << "you have what it takes.\n";

    try
    {
        while (m.moreMines())
        {
            cout << m.draw();
            cout << "Your position is marked with a P.\n";
            cout << "Which direction would you like to go?" << endl;

            bool proper = false;
            do {
                int goto_dir = m.Directions();
                if (goto_dir == 1)
                    m.place() -= 4;
                else if (goto_dir == 2)
                    m.place()++;
                else if (goto_dir == 3)
                    m.place() += 4;
                else if (goto_dir == 4)
                    m.place()--;

                if (m.place() < 0 || m.place() > 15) {
                    cout << "\nYou go that way.\n";
                } else {
                    m.goThere(m.place());
                    if (m.isAMine(m.place()))
                        throw StepOnMine();
                    proper = true;
                }
            } while (!proper);
        }
    :
        cout << "\nYou have cleared the minefield!\n";
    }
    catch(StepOnMine)
    {
        int input;
        do {
            cout << "\nYou encountered a mine.\n";
            cout << "What would you like to do?\n";
            cout << "[1]Attempt to Disarm.\n";
            cout << "[2]Run Away.\n";
            cin >> input;
        } while (input < 1 || input > 2);

        if (input == 1)
        {
            try {
                disarm();
            } catch(FailedDisarm) {
                terminate();
            }
            cout << "\nYou have disarmed the mine!!!\n";
            return 0;
        }

        cout << "\nYou have failed the XJ7 team.\n";
        return 0;
    }

    cout << "\nMaybe next kid.\n";
    return 0;
}
```

# 总结

本章虽然短，但非常重要。即使是最高水平的程序员也经常 `ignore the concept of this chapter`, and it is true that exception handling does not add to the functionality of your program. However, exception handling makes your programs stable, and if you want to advance from being a good programmer to being an excellent one, we strongly suggest that you make a habit of using it.

## 挑战

- 1. `try` 关键字的作用是什么？
- 2. 异常层级结构的目的是什么？
- 3. 你如何设计程序以使其不会崩溃？
- 4. 异常的定义是什么？
- 5. 在什么情况下使用断言？

[298页]

本页留白

[299页]

## 创建雷区游戏

本章的最后一部分是向你展示如何使用 C++ 来制作一个游戏。在本章中，你将学习到：

- 声明全局变量
- 创建飞船
- 飞船跨移动
- 绘制飞船

[300页]

## 介绍 GDK

一个人需要很多东西，但幸运的是，有一个库名为 `GDK`，你可以在 `http://www.microsoft.com/express/samples/gamecreators/default.aspx` 获取。

# 零基础 C++ 编程，第二版

```cpp
// 创建一个动画精灵并赋予它来自变量
// i 的 ID 号，接下来是文件名，现在我们来看横向和纵向
// 的帧数，在我们的案例中这是 4，最后我们来看精灵
// 将使用的图像 ID，我们再次使用 i
dbCreateAnimatedSprite ( i, "sprite.bmp", 4, 4, i );
```

```cpp
// 将我们的精灵放置在随机位置
dbSprite ( i, dbRnd ( 640 ), -dbRnd ( 1500 ), i );
```

```cpp
// 现在我们进入主循环，我们调用 LoopGDK，以便 GDK
// 执行一些内部工作
while ( LoopGDK ( ) )
```

```cpp
// 遍历我们所有的精灵
for ( int i = 2; i < 30; i++ ) )
```

```cpp
// 将精灵向下移动并播放它的动画
// 从第 1 帧移动到第 16 帧，延迟为 60 毫秒
dbMoveSprite ( i, -2 )
dbPlaySprite ( i, 1, 16, 60 );
```

```cpp
// 检查精灵的位置，如果它已经离开了屏幕
// 则将其重新定位并回到顶部
if ( dbSpriteY ( i ) > 500 )
dbSprite ( i, dbRnd ( 640 ), -dbRnd ( 1500 ), i );
```

```cpp
// 在这里检查是否按下了退出 键，如果按下
// 我们将跳出循环
if ( dbEscapeKey ( ) )
    break;
```

```cpp
// 在这里我们调用更新屏幕内容
dbSync ( );
```

// 当用户按下退出 键时，代码将跳转到此位置

// 我们可以释放之前分配的所有资源

```cpp
// 删除所有精灵
for ( int i = 1; i < 30; i++ )
 dbDeleteSprite ( i );
```

```cpp
// 删除背景图像
dbDeleteImage ( 1 );
```

```cpp
// 现在一切都准备好返回 Windows 了
return;
```

这段代码虽然充满了有用的注释，但初看之下可能会让人无从从。不要放弃希望！到本章结束，这段代码看起来将非常自然。

所以，勤奋的读者，你应该做的第一件事就是编译并运行这段代码，看看它到底做了什么。记住从创建一个“Dark GDK – 2D 游戏”项目开始。运行的程序如图 11.2 所示。

![](img/62e929c461e30706acae7c69369a00d9_303_0.png)

# 零基础 C++ 编程，第二版

现在，让我们开始分解这段代码来理解它。你首先注意到的是完全缺少 `main()` 函数。当使用 Dark GDK 而不是 `main()` 时，你必须创建一个 `DarkGDK()` 函数。该函数没有参数且返回值为 void。此程序中的所有代码都包含在这个函数中，而这些代码可以分为三部分：初始化、主循环和清理。

初始化是这三个部分中最长的。它包含了从 `DarkGDK()` 函数开始到这些行之间的所有：

```cpp
// 现在我们进入主循环，我们调用 LoopGDK，以便 GDK
// 执行一些内部工作
while ( LoopGDK ( )
```

初始化部分的第一步是以下两行：

```cpp
dbSyncOn ( );
dbSyncRate ( 60 );
```

Dark GDK 提供的每个函数都以 "`db`" 为开头。这是为了确保函数名不会与你的发生冲突；类似于 C++ 标准库使用 `std` 命名空间。

这两行代码设置了最大帧率。对于图形游戏，控制事情发生的速率是非常重要的，因为在现代计算机上，如果只是尽可能快地运行，会变得太快。这里的帧率设置为 60。这意味着屏幕上的图像每秒更新 60 次。

默认情况下，Dark GDK 程序会通过退出 键立即退出。通常你可能想在退出之前执行某些操作，或者想将退出 键用于其他用途。调用 `dbEscapeKey()` 禁用了 GDK 对退出 键的默认处理。C++ 标准库提供了生成随机数的功能，但 Dark GDK 有自己的。就像使用 `rand()` 初始化随机数生成器一样，我们使用 `dbRandomize` 来初始化 Dark GDK 的随机数生成器。使用 `dbTimer()` 就像使用 `time()`。

现在我们到了有趣的部分！`dbLoadImage()` 调用从图像文件读取背景以准备好显示。该函数接受两个参数：图像的文件名和你分配的 id。你必须记住这个数字，以便在代码中引用加载的图像。

# 第二章 · 创建海盗冒险

说到这里，加载的图像在下一行中使用。为了在屏幕上显示图像，我们必须首先将其加载到“精灵”。Dark GDK 中的精灵是一个二维图像，可以显示在屏幕上。当我们创建一个精灵时，我们赋予它一个 id 和整个屏幕的左上角位置 `(0,0)`。图像 id 用于引用之前加载的图像。使用 `dbSetColorKey()` 函数，你可以将某种颜色设为透明。最后一步是在随机位置创建精灵。这些精灵与背景不同。而不是 `dbLoadImage()`，我们使用 `dbAnimatedSprite()` 来加载精灵的动画帧。你必须提供每行的帧数和列数。尽管精灵是用此函数创建的，我们仍然调用 `dbSprite()` 给这个精灵一个位置。

![](img/62e929c461e30706acae7c69369a00d9_305_0.png) 图 11.3 图像文件

现在一切都初始化完毕，是时候进入主循环了。该循环结构如下：

```cpp
while(LoopGDK())
{
  ...
}
```
