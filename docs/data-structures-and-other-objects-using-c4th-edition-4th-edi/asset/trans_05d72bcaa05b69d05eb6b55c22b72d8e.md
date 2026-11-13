

为派生类的任何成员变量，然后调用基类的析构函数。

- 6. 正午闹钟（NoonAlarm）重写了普通时钟的 advance 成员函数：

```cpp
class noon_alarm : public clock
{
public:
   void advance(int minutes);
};

void noon_alarm::advance(int minutes)
// Library facilities used: iostream
{
   int until_noon;

   // Calculate number of minutes until
   // noon.
   if (is_morning( ))
      until_noon =
         60 * (12-get_hour( ))
         - get_minute( );
   else if (get_hour( ) == 12)
      until_noon =
         60 * (24 - get_hour( ))
         - get_minute( );
   else
      until_noon =
         60 * 24
         - get_minute( );

   // Maybe print an alarm message.
   if (minutes > 0)
      if (minutes >= until_noon)
         cout << "Alarm!";
   // Call the base class member function.
   clock::advance(minutes);
}
```

- 7. ![](img/7bf56f684fab50d5ff9e94ae2818f3ac_756_0.png)

- 8. person 类的定义：

```cpp
class person
{
public:
   person( );
   person(string name, double weight,
          date birthdate, char gender);
   void set_weight(double weight);
   double get_weight( ) const;
   int getAge( ) const;

private:
   string name;
   date birthdate;
   double weight;
   char gender;
};
```

- 9. 派生类 adult 的构造函数：

```cpp
adult::adult(
   string name,
   double weight,
   date birthdate,
   char gender
   ) : person(name, weight, birthdate, gender)
{
}
```

- 10. plant 的定义如下：

```cpp
class plant : public organism
{
public:
   // CONSTRUCTOR
   plant(double init_size = 0,
         double init_rate = 0);
   // MODIFICATION FUNCTIONS
   void nibbled_on(double amount);
};
```

The member functions are implemented here:

```cpp
plant::plant(double init_size,
             double init_rate)
   : organism(init_size, init_rate)
   {
      // All work is done by the organism
      // constructor.
   }
void plant::nibbled_on(double amount)
// Library functions used: cassert
{
   assert(amount >= 0);
   assert(amount <= get_size( ));
   alter_size(-amount);
}
```

- 11. 请参见第 709 页图 14.10 中的解答。

- 12. 这是一个解答：

```cpp
const int N = 10;
const int SELECT = 5;
const organism SAMPLE[16];
vector<organism> blobs(N, SAMPLE);
int i, index;
double answer;
vector<organism>::iterator it;

for (i = 1; i <= SELECT; ++i)
{
    index = rand() % N;
    blobs[index].assign_rate(2);
}

answer = 0;
for (it = blobs.begin();
     it != blobs.end();
     ++it)
    answer +=
    it->get_rate();

cout << answer << "total of rates\n";
```

- 14. rand 选择了一个生物体两次（另外三个生物体各被选择了一次）。

- 15. 我们将部分内容留给你自己完成，但这是新的成员函数：

```cpp
void carnivore::chase
(animal& prey, double chance)
// Library facilities used: cassert, cstdlib
{
    assert(chance >= 0);
    assert(chance <= 1);
    if (chance > 0)
    if (rand()/double(RAND_MAX)
        < chance)
    {
        eat(prey.get_size());
        prey.death();
    }
}
```

- 16. 基类有一个成员函数 f，它会激活另一个成员函数 g。这个 g 成员函数将在派生类中被重写。当派生类的对象激活 f 时，它将使用 f 的基类版本。但在 f 内部，我们希望它使用派生类中被重写的 g。

- 17. 虚成员函数的正确版本仅在运行时确定。在执行期间，程序根据激活该方法的对象的数据类型来选择成员函数。

- 18. 该类不提供纯虚函数的任何实现。由于没有实现，任何包含纯虚函数的类都称为抽象类，且抽象类的实例不能出现在程序中。纯虚函数预期将在派生类中被重写。

- 19. `virtual double calculate_bmr() = 0;`

- 20. 这是一个使用标准库函数 atoi 将字符串转换为整数的解答（参见附录 G）：

```cpp
void connect4::make_move
(const string& move)
// Library facilities used: cassert, cstdlib
{
    int row, column;
    assert(is_legal(move));
    column = atoi(move.c_str());
    row = many_used[column]++;
    data[row][column] = next_mover();
    most_recent_column = column;
    game::make_move(move);
}
```

- 21. Alpha-beta 剪枝是停止评估（例如极小极大搜索）的过程，如果它无法产生比已确定的解更好的解。

## 编程项目

如需更深入的项目，请参见 www.cs.colorado.edu/~main/projects/

- 1. 集合类似于袋子，但集合不允许任何元素有多个副本。如果你尝试插入集合中已存在的项目的新副本，则集合将保持不变。对于本项目，请将集合实现为从你的某个袋子类派生的新类。你的实现应仅重写 insert 成员函数。

- 2. 重写第 707 页图 14.10 中的池塘生命程序，使得程序开始处声明的值不再是常量。程序的用户应能够为所有这些常量输入值。此外，扩展该程序，使鱼更加真实。具体来说，鱼应该出生时体型较小，并生长到某个最大体型。每条鱼还应有一个与其当前体型成正比的每周食物需求。

- 3. 扩展第 14.2 节中的生物对象层次结构，使其中包含一个新类 `carnivore`，如第 712 页自测练习 14 所述。在小岛生命模型中使用该层次结构，该岛上包含灌木、吃灌木的大雁和吃大雁的狐狸。程序应允许用户更改岛上的初始条件（例如狐狸的数量、维持一只狐狸所需的食物量等）。

- 4. 将袋子模板类实现为列表的派生类。使用标准模板库中的列表。袋子应具有第 340 页图 6.7 中的所有操作。

- 5. 实现第 702 页自测练习 8 中的人员基类。此外，实现男性和女性派生类，并根据以下公式计算 BMR：男性：66 + (30.14 × 磅重) + (1.97 × 英寸高) - (6.8 × 年龄)；女性：655 + (21.12 × 千克重) + (7.1 × 英寸高) - (4.7 × 年龄)。扩展类层次结构，包含一个计算推荐每日热量摄入量的函数。每日热量摄入量是 BMR 乘以表示身体活动水平的常数。常数为：久坐（1.2）、中度活跃（1.55）、轻度活跃（1.35）和高度活跃（1.725）。

- 6. 编写一个程序，维护一个人员向量（来自上一个项目）以表示健身俱乐部成员。程序应向用户提供菜单选项以修改和查看个人健康信息。还应包含按性别计算所有俱乐部成员平均年龄、体重和活动水平的函数。

- 7. 重做第 10 章编程项目 12，以存储其他形式的媒体（例如 CD、DVD、VHS 和磁带）。创建一个基类 Item，并根据需要派生其他形式（包括书籍）。基类应包含 ISBN，但派生类可能包含不同的成员，具体取决于其媒体类型。用户应能够像以前一样查看和修改项目，但还应提供查看特定媒体类型项目的功能。

- 8. Tic-Tac-Twice 是由 Pat Baggett 和 Andrzej Ehrenfeucht 发明的一种游戏。其规则由 Aristoplay 公司分发。规则很简单，从两个 4x4 棋盘开始，每个棋盘都有 16 个字母（或其他对象）的图案。如果使用字母 A 到 P，则两个棋盘具有以下图案：

**棋盘 1**

| A | B | C | D |
|---|---|---|---|
| E | F | G | H |
| I | J | K | L |
| M | N | O | P |

**棋盘 2**

| B | K | M | H |
|---|---|---|---|
| P | E | C | J |
| G | N | L | A |
| I | D | F | O |

两名玩家（人类和计算机）轮流进行。在你的回合中，你可以在棋盘 1 的空位上放置你颜色的棋子。同时，你在棋盘 2 的同一格子上放置带有相同字母的你颜色的棋子。例如，如果你将棋子放在棋盘 1 的左下角（字母 M），那么你将同时在棋盘 2 顶行的第三个位置放置一个你的棋子（也是字母 M）。

通过在任一棋盘上使你的四个棋子成一行（水平、对角线或垂直）来获胜。请注意，你不需要在两个棋盘上都成行，只需在其中一个棋盘上即可。

实现一个类，允许用户与计算机对战 Tic-Tac-Twice。使用第 14.3 节中的 game 类作为基类。

