
# 从用户获取数字

对于大多数程序，最重要的问题之一是用户界面。我们希望用户的体验是能够从发出的牌中保留任意组合，并丢弃任意组合。实现这一点的一种方法是对每张牌单独询问用户：

- 你想重抽第 1 张牌吗？Y
- 你想重抽第 2 张牌吗？N
- 你想重抽第 3 张牌吗？Y
...

但这将很无聊，谁想无聊呢？我们希望允许用户在一行内输入所有请求，如下：

丢弃牌：1, 3, 5

然而我们还可以做得更好。为什么要在数字之间需要逗号，甚至是空格呢？这里双位数是不可能的，因为唯一的有效选择都是单数字：1, 2, 3, 4, 或 5。因此，我们应该让用户连续输入她想要做的选择。

丢弃牌：135

有一种简单的方法可以支持这种输入系统。你可以索引字符串对象以获取字符，就像使用 C 字符串一样。例如：

## 从用户获取数字

你可以扫描字符串中的“1”到“5”的数字字符，并打印找到的每一个。正如第 8 章“字符串：分析文本”所示，如果你索引 C 字符串或 C++ 字符串对象，你会得到一个 `char` 类型的值。这实际上是一个在打印时会转换为字符的数字。514 页的表 E.1 列出了 ASCII 字符码。

```cpp
// 仅扫描数字字符串并打印'1' 到'5'
```

```cpp
for (int i = 0; i < sInput.size(); ++i) {
    int n = sInput[i] - '0';
    if (n >= 1 && n <= 5) {
        cout << n << " ";
    }
}
```

这个循环可以运行，尽管你可能不知道数字的 ASCII 值，但你可以依靠它们在序列中的相对顺序。所以，如果字符是 '0'，减去 '0' 产生数字 0，这是显然的。如果字符是 '1'，减去 '0' 产生数字 1，这也是 true。如果字符是 '2'，减去 '0' 产生数字 2，以此此类推。因此，减去 ASCII 值转换为数字数值。

我们可以利用它来识别 1 到 5 的数字，并将相应的索引数字 0 到 4 添加到数字向量（因为 C++ 有从 0 开始的数组）。

```cpp
for (int i = 0; i < sInput.size(); ++i) {
    int n = sInput[i] - '0';
    if (n >= 1 && n <= 5) {
        selVec.push_back(i - 1);
    }
}
```

# 示例 15.2. 抽牌扑

使用 `vector` 模板和扫描字符串获取单个数字的能力，我们终于可以编写允许玩家丢弃任意组合牌并抽取新牌的视频扑牌版本。

与示例 15.1 相比，新增或更改的代码行在此处以粗体显示。

## Poker2.cpp

```cpp
#include <iostream>
#include <string>
#include <cstdlib>
#include <ctime>
#include <vector>
using namespace std;
```

```cpp
// 包含牌组类和牌类
// 在此处进行声明和定义。
```

`Deck` `my_deck`;
`Card` `aFlags[5]`;
`vector<int>` `selVec`;

```cpp
void play_game();
bool draw();
```

```cpp
main() {
  string s;
  while (true) {
    play_game();
    cout << "Play again? (Y or N): ";
    getline(cin, s);
    if (s[0] == 'N' || s[0] == 'n') {
      break;
    }
  }
  return 0;
}
```

```cpp
void play_game() {
  for (int i = 0; i < 5; ++i) {
    aCards[i] = my_deck.deal_a_card();
    aFlags[i] = false;
    cout << i + 1 << " ";
    aCards[i].display() << endl;
  }
}
```

```cpp
cout << endl;
```

# 从玩家处获取数字

Poker2.cpp, 续

```cpp
// 抽取新牌，并重新显示
if (draw()) {
  for (int i = 0; i < 5; ++i) {
    cout << i + 1 << ".";
    cout << aCards[i].display();
    if (aFlags[i]) {
      cout << "*";
    }
    cout << endl;
  }
}
cout << endl;
```

```cpp
bool draw() {
  string sInput;
  selVec.clear();
  cout << "Input #s of cards to redraw: ";
  getline(cin, sInput);
  if (sInput.size() == 0) {
    return false;
  }
  // 读取输入字符串，每读到一个数字
  // 就向 selVec 中添加一个元素。
  for (int i = 0; i < sInput.size(); ++i) {
    int n = sInput[i] - '0';
    if (n >= 1 && n <= 5) {
      selVec.push_back(n - 1);
    }
  }
  // 对于 selVec 中的每个数字 (0-4)，
  // 重新抽取对应的牌牌。
  for (int i = 0; i < selVec.size(); ++i) {
    int j = selVec[i]; // 选择一张牌
    aCards[j] = my_deck.deal_a_card();
    aFlags[j] = true;
  }
  return true;
}
```

# 第 15 章 面对象的扑克游戏

这是一个示例会话。你应该注意到其中的不同，即玩家可以重新抽取任意组合的牌！与之前的示例会话一样，输入以**粗体**显示。

- 1. 黑桃 A。
2. 方梅 10。
3. 黑花 K。
4. 黑梅桃 3。
5. 红桃 A。

输入要重抽的牌数：234
1. 黑桃 A。
2. 方梅 A。*
3. 方梅 7。*
4. 黑梅桃 7。*
5. 红桃 A。

再玩一次？N
哇，一个葫芦：三个 A 和两个 7！如果程序能识别出这一事实并给予相应的奖励，那有多好啊？这就是我们在本章最后部分要在程序中添加的内容。

![](img/b88f5481c752ba5bbade24ce372725ab_408_0.png)

## 工作原理

程序新版本的第一件事是声明一些新的数据结构：

```cpp
bool aFlags[5]; vector<int> selVec;
```

`aFlags` 是一组五个标记，每个标记对应手牌中的一张牌。当标记被设置为 true 时，意味着该牌已被重新抽取。这使得可以方便地在每张代表重抽的牌旁边标记上星号（*）。
接下来，修改了 `play_game` 函数，使其调用 `draw` 函数，该函数从用户处获取关于哪些牌（如果有）应该重抽的输入。如果用户按下回车键且没有输入，则假设她只是想保留现有的牌，并且对这手牌不采取进一步操作。返回 false 表示这种情况。

```cpp
if (draw()) {
  // 重新打印手牌...
}
```

# 从玩家处获取数字 377

`draw` 函数有两个主要任务，每项任务都通过一个简单的循环完成：1) 询问用户哪些牌需要重抽；2) 根据用户识别的 1 到 5 数字，通过向 `Deck` 对象请求新牌来重抽这些牌。这些操作可以分解为以下伪代码：

```
提示用户输入字符串
遍历输入字符串中的每个字符
如果字符是 1 到 5 之间的数字
将 N-1 推入 selVec
遍历 selVec 中的每个元素
将 J 设置为 selVec 的当前元素
用新牌替换 aCards[J]
```

通过示例，这些循环可能会更容易理解。假设用户输入了 "125"。第一个循环将每个数字减 1，产生一个包含如下值的向量：第二个循环遍历这些值并重抽牌。

| 用户输入 | 结果向量 |
|---|---|
| 125 | 0, 1, 4 |

| 索引 | aCards 索引 |
|---|---|
| 0 | aCards[0] |
| 1 | aCards[1] |
| 4 | aCards[4] |

# 从玩家处获取数字 378

第 15 章 面向对象的扑克游戏

![](img/b88f5481c752ba5bbade24ce372725ab_10.png)

## 练习

- **15.2.1.** 重写 `play_game` 函数，在每张牌旁边打印星号。
- **15.2.2.** 使用第 13 章讨论的技术实现 `selVec`。
- **15.2.3.** 使用普通数组 `aFlags`（提示：你需要）。
- **15.2.4.** 防止任何牌被重抽多次。

# 如何评估牌

我们可以通过检查 `rankCounts` 和 `SuitCounts` 这两个数组来评估牌型。这里有很多工作要做，仅仅是因为需要考虑的牌型太多了。

出于模块化设计的考虑，我们将所有的牌型评估代码放在另一个类中，我将其命名为“Eval”。与其他类一样，我们只只创建一个对象，并通过该对象调用函数。

有一种牌型该类无法识别。在扑克中，王牌既可以是高牌也可以是低牌，大多数情况下对玩家有利。在实践中，这几乎意味着王牌总是高牌，但有一个例外：A-2-3-4-5 牌（无论顺序如何）构成了一个 5 高顺子，并被称为“五轮子”。识别这种牌型留给你们作为练习。

## eval.cpp

```cpp
// 注意包含该类的程序必须包含 <string>
// 还要使用 namespace std;
//
class Eval {
public:
    Eval(Card* pCards);
    string rank_hands();
private:
    int rankCounts[13];
    int suitCounts[4];
    int has_reps(int n);
    bool is_straight();
    bool verify_straight(int n);
    bool is_flush();
    bool is_two_pair();
};
Eval::Eval(Card* pCards) {
    for (int i = 0; i < 13; ++i) { // 清空数组
        rankCounts[i] = 0;
    }
    for (int i = 0; i < 4; ++i) {
        suitCounts[i] = 0;
    }
    for (int i = 0; i < 5; ++i) { // 初始化数组
        int r = pCards[i].rank;
        int s = pCards[i].suit;
        ++rankCounts[r];
        ++suitCounts[s];
    }
}
```

## 如何评估扑克牌

## 381

eval.cpp, 续。

```cpp
string Eval::rank_hands() {
    string s;
    if (is_straight() && is_flush()) {
        if (ranksCount[12] && ranksCount[11]) { // A&K
            s = "你获得了皇家同花！派率 = 800";
        } else {
            s = "你获得了同花顺子！派率 = 50";
        }
    } else if (has_reps(4)) {
        s = "你获得了四条！派率 = 25";
    } else if (has_reps(3) && has_reps(2)) {
        s = "你获得了葫芦！派率 = 9";
    } else if (is_flush()) {
        s = "你获得了同花！派率 = 6";
    } else if (is_straight()) {
        s = "你获得了顺子！派率 = 4";
    } else if (has_reps(3)) {
        s = "你获得了三条。派率 = 3";
    } else if (is_two_pair()) {
        s = "你获得了两对。派率 = 2";
    } else if (has_reps(2)) {
        s = "你获得了对子。派率 = 1";
    } else {
        s = "你没有对子。派率 = 0";
    }
    return s;
}
```
// has_reps 函数。
// 如果任何点数重复了
// 指定次数，则返回 true。

```cpp
int Eval::has_reps(int n) {
    for(int i = 0; i < 13; ++i) {
        if (rankCounts[i] == n) {
            return true;
        }
    }
    return false;
}
```

下页待续

## 382 第 15 章 面向对象的扑克

```cpp
// is_straight 函数。
// 在点数中寻找第一个“孤立点数”，
// 然后验证它是否开始了一个顺顺子。
bool Eval::is_straight() {
    for (int i = 0; i < 8; ++i) {
        if (rankCounts[i] == 1) {
            return verify_straight(i);
        }
    }
    return false;
}
bool Eval::verify_straight(int n) {
    for (int i = n + 1; i < n + 5; ++i) {
        if (rankCounts[i] != 1) {
            return false;
        }
    }
    return true;
}
bool Eval::is_flush() {
    for (int i = 0; i < 4; ++i) {
        if (suitCounts[i] == 5) {
            return true;
        }
    }
    return false;
}
bool Eval::is_two_pair() {
    int n = 0;
    for (int i = 0; i < 13; ++i) {
        if (rankCounts[i] == 2) {
            n++;
        }
    }
    return n == 2;
}
```

## 五抽扑克派率！

以下代码展示了与 Eval 类交互的修改后的主程序。（不包含任何类的声明和定义）。只需要在 Eval 中添加两行，这两行将以**粗体**打印。

```cpp
Poker3.cpp
#include <iostream>
#include <string>
#include <cstdlib>
#include <ctime>
#include <vector>
using namespace std;
// 包含牌组、卡牌和 Eval 类
// 声明和定义。
Deck my_deck;
Card aCards[5];
bool aFlags[5];
vector<int> selVec;
void play_game();
bool draw();
int main() {
    string s;
    while (true) {
        play_game();
        cout << "再次开始？(Y 或 N): ";
        getline(cin, s);
        if (s[0] == 'N' || s[0] == 'n') {
            break;
        }
    }
    return 0;
}
```

## 384 第 15 章 面向对象的扑克

Poker3.cpp, 续

```cpp
void play_game() {
    for (int i = 0; i < 5; ++i) {
        aCards[i] = my_deck.deal_card();
        aFlags[i] = false;
        cout << i + 1 << ". " << aCards[i] << endl;
    }
}
// 抽牌，然后重新显示
if (draw()) {
    string sInput;
    selVec.clear();
    cout << "要重抽的牌数: ";
    getline(cin, sInput);
    if (sInput.size() == 0) {
        return false;
    }
```
