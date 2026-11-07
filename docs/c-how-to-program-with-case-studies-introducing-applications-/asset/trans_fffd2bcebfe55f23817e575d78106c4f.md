

“发 52 张牌”可以细化如下：

- 对于 52 张牌中的每一张
  - 在牌组数组中找到牌号，并打印其牌面和花色

完整的第二次细化如下：

- 初始化花色数组
- 初始化牌面数组
- 初始化牌组数组
- 对于 52 张牌中的每一张
  - 将牌号放入牌组中随机选择的未占用槽位
- 对于 52 张牌中的每一张
  - 在牌组数组中找到牌号，并打印该牌的牌面和花色

“将牌号放入牌组中随机选择的未占用槽位”可以细化为：

- 随机选择牌组槽位
- 当所选的牌组槽位先前已被选择时
  - 随机选择牌组槽位
- 将牌号放入所选牌组槽位

“在牌组数组中找到牌号并打印其牌面和花色”可以细化为：

- 对于牌组数组中的每个槽位
  - 如果槽位包含牌号
    - 打印该牌的牌面和花色

合并这些扩展后，得到我们的第三次细化：

- 初始化花色数组
- 初始化牌面数组
- 初始化牌组数组
- 对于 52 张牌中的每一张
  - 随机选择牌组槽位
  - 当牌组槽位先前已被选择时
    - 随机选择牌组槽位
  - 将牌号放入所选牌组槽位
- 对于 52 张牌中的每一张
  - 对于牌组数组中的每个槽位
    - 如果槽位包含目标牌号
      - 打印该牌的牌面和花色

至此完成细化过程。

## 实现洗牌和发牌程序

洗牌和发牌程序及示例执行结果如图 7.16 所示。当函数 printf 使用转换说明 %s 打印字符串时，相应的实参必须是指向字符串的 char 指针，或包含字符串的 char 数组。第 59 行的格式说明将牌的牌面*右对齐*显示在五个字符宽的字段中，后跟 " of "，并将牌的花色*左对齐*显示在八个字符宽的字段中。%-8s 中的*负号*表示左对齐。

```c
// fig07_16.c
// Card shuffling and dealing.
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define SUITS 4
#define FACES 13
#define CARDS 52

// prototypes
void shuffle(int deck[][FACES]);
void deal(int deck[][FACES], const char *face[], const char *suit[]);

int main(void) {
   // initialize deck array
   int deck[SUITS][FACES] = {0};

   srand(time(NULL)); // seed random-number generator
   shuffle(deck); // shuffle the deck

   // initialize suit array
   const char *suit[SUITS] = {"Hearts", "Diamonds", "Clubs", "Spades"};

   // initialize face array
   const char *face[FACES] = {"Ace", "Deuce", "Three", "Four", "Five",
      "Six", "Seven", "Eight", "Nine", "Ten", "Jack", "Queen", "King"};

   deal(deck, face, suit); // deal the deck
}

// shuffle cards in deck
void shuffle(int deck[][FACES]) {
   // for each of the cards, choose slot of deck randomly
   for (size_t card = 1; card <= CARDS; ++card) {
      size_t row = 0; // row number
      size_t column = 0; // column number

      // choose new random location until unoccupied slot found
      do {
         row = rand() % SUITS;
         column = rand() % FACES;
      } while (deck[row][column] != 0);

      deck[row][column] = card; // place card number in chosen slot
   }
}
```

**图 7.16** | 洗牌和发牌。（第 1 部分，共 2 部分。）

```c
// deal cards in deck
void deal(int deck[][FACES], const char *face[], const char *suit[]) {
    // deal each of the cards
    for (size_t card = 1; card <= CARDS; ++card) {
        // loop through rows of deck
        for (size_t row = 0; row < SUITS; ++row) {
            // loop through columns of deck for current row
            for (size_t column = 0; column < FACES; ++column) {
                // if slot contains current card, display card
                if (deck[row][column] == card) {
                    printf("%5s of %-8s%c", face[column], suit[row],
                           card % 4 == 0 ? '\n' : ' '); // 4-column format
                }
            }
        }
    }
}
```

```text
Ace of Hearts    Jack of Hearts    Five of Clubs    King of Clubs
Eight of Diamonds    Three of Clubs    Deuce of Hearts    Four of Hearts
Ace of Clubs    Deuce of Spades    Queen of Diamonds    Six of Hearts
Seven of Clubs    Five of Hearts    Deuce of Clubs    King of Hearts
Nine of Spades    Ace of Spades    Ace of Diamonds    Eight of Spades
Eight of Hearts    Ten of Spades    Ten of Hearts    Queen of Clubs
Jack of Spades    Jack of Diamonds    Three of Spades    Four of Clubs
Four of Spades    Ten of Clubs    King of Diamonds    Six of Spades
Nine of Clubs    Six of Diamonds    Queen of Spades    King of Spades
Four of Diamonds    Eight of Clubs    Jack of Clubs    Seven of Hearts
Seven of Diamonds    Three of Hearts    Five of Spades    Nine of Hearts
Nine of Diamonds    Three of Diamonds    Deuce of Diamonds    Queen of Hearts
Six of Clubs    Seven of Spades    Five of Diamonds    Ten of Diamonds
```

**图 7.16** | 洗牌和发牌。（第 2 部分，共 2 部分。）

## 改进发牌算法

发牌算法存在一个缺陷。一旦找到匹配项，两个内层 for 语句仍会继续搜索牌组中剩余的元素。我们将在本章练习和第 10 章的一个案例研究中纠正这一缺陷。

## 相关练习

本“洗牌和发牌”案例研究由以下练习支持：

- 练习 7.12（洗牌和发牌：发扑克牌手牌）
- 练习 7.13（项目：洗牌和发牌——哪手扑克牌更好？）
- 练习 7.14（项目：洗牌和发牌——模拟发牌员）
- 练习 7.15（项目：洗牌和发牌——允许玩家抽牌）
- 练习 7.16（洗牌和发牌修改：高性能洗牌）

## 自测题

**1（填空）** 如果已经洗过的牌被反复随机选中，我们给出的洗牌算法可能会无限执行下去。这种现象称为________。

**答案：** 无限期推迟。

**2（判断正误）** 格式说明 "%5s of %-8s" 将字符串左对齐打印在五个字符宽的字段中，后跟 " of "，并将字符串右对齐打印在八个字符宽的字段中。

**答案：** 错误。实际上，该格式说明将字符串右对齐打印在五个字符宽的字段中，后跟 " of "，并将字符串左对齐打印在八个字符宽的字段中。

## 7.12 函数指针

在第 6 章中，我们看到数组名实际上是数组首元素在内存中的地址。类似地，函数名实际上是执行该函数任务的代码在内存中的起始地址。函数指针包含函数在内存中的地址。函数指针可以传递给函数、从函数返回、存储在数组中、赋值给相同类型的其他函数指针，并相互比较是否相等或不相等。

### 7.12.1 按升序或降序排序

为了演示函数指针，图 7.17 给出了图 7.11 冒泡排序程序的修改版本。新版本由 main 以及函数 bubbleSort、swap、ascending 和 descending 组成。除了 int 数组和数组大小之外，函数 bubbleSort 还接收一个函数指针作为实参——即函数 ascending 或函数 descending 的指针。用户选择按升序（1）还是降序（2）对数组排序。如果用户输入 1，main 将指向函数 ascending 的指针传递给函数 bubbleSort。如果用户输入 2，main 将指向函数 descending 的指针传递给函数 bubbleSort。

```c
1 // fig07_17.c
2 // Multipurpose sorting program using function pointers.
3 #include <stdio.h>
4 #define SIZE 10
5
6 // prototypes
7 void bubbleSort(int work[], size_t size, int (*compare)(int a, int b));
8 int ascending(int a, int b);
9 int descending(int a, int b);
10
```

