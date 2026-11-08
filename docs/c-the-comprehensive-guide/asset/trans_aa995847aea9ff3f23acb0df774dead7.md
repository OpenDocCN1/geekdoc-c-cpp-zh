
因此，unique_ptr 不是被复制，而是被移动。准确地说，被移动的是它的内容。这意味着 unique_ptr 将新创建的临时值（内部）所管理的裸指针转移到（外部的）unique_ptr<MyDialog> dialog 中。

在 showModal() 中，事情变得更加有趣。原则上，这里发生的事情与 createDialog() 中相同。但这个方法通过移动来返回一个已存在的值。那么为什么不直接写成 return btnOk_ 呢？这是因为 btnOk_ 不是临时值。正如你在第 16 章所见，我们只能安全地从那些你知道很快就会消失的对象中“窃取”。临时值就属于这种情况。然而，btnOk_ 不是临时值，而是一个数据成员——一个具有名称的对象。如果编译器悄悄取走它的裸指针，那会让人感到意外。¹

好吧，在这里你确定想要从现有变量中提取内容——把它当作临时值来移动。通过 std::move，你告诉编译器：“是的，亲爱的编译器，请把 btnOk_ 视为临时值”，于是它就像在 createDialog() 中那样行事。也就是说，unique_ptr 从返回值中取得裸指针，并将其转移到 showDialog()。

到目前为止一切顺利：程序做了它该做的事，你看到文本输出“Thank you for pressing OK”。然而，你绝对不能做的是调用 dialog->showModal() 两次：

```cpp
int showDialogAgain() {
    unique_ptr<MyDialog> dialog = createDialog();
    unique_ptr<Button> pressedOne = dialog->showModal();
    unique_ptr<Button> pressedTwo = dialog->showModal(); // ✖ not twice
    return pressedTwo->id_; // ✖ Error; likely crash
}
```

你肯定已经认识到，通过对 pressedOne 调用 showModal()，dialog 中的 btnOk_ 数据成员被转移到了 pressedOne 变量。两者都是 unique_ptr，但只有一个能成为裸指针的所有者：那个用 new 创建一次的 Button*。而在第一次调用 showModal() 后，pressedOne 现在包含这个 Button 指针，dialog.btnOk_ 则包含 nullptr，即“空”值。在这个示例中，第二次 showModal() 仍然能工作；然后你会把这个 nullptr 转移到 pressedTwo。如果你随后对这个 nullptr 尝试 ->id_，程序（往好里说）会崩溃。

请原谅这段关于 unique_ptr 作为返回值能做什么的小教程。它说明了 unique_ptr 凭借其独占所有权会产生副作用。这些正是你想要的副作用：编译器自己不会想到从具有名称的变量或数据成员中窃取内容。我用 std::move() 帮了忙。

¹ 请注意，这正是 auto_ptr 会做的事情。因此，从 C++11 起请不要使用它。

### “std::move” 自身并不移动

因为你在这里第一次看到 `std::move()`，我想给出一点提示；没有这个提示，你可能会陷入误解。`std::move()` 函数本身并不移动，它只是允许某个东西被移动——在这里，是函数的返回值。

实际上，这只是一个到临时值引用的类型转换，有些人可能更希望把它叫作 `move_cast`。

这些数据成员都是 `unique_ptr` 指针。没有指针的简单数据成员在这里就足够了。但也许你以后想以多态方式扩展 *MyDialog*：为此，你需要指针。这里的*多态*意味着，例如，你从类 `TextField` 派生出一个 `ColorfulTextField` 类，然后把该类的一个实例放入 `unique_ptr<TextField> txtFirstName_`。如果 `txtFirstName_` 不是指针（或引用），`ColorfulTextField` 的特性就会丢失。你可以在[第 15 章](#)中找到一个这样的例子。

你可以应用使用 `unique_ptr` 的经验法则。例外证明规则：

- 你很可能可以将 `unique_ptr` 用作引用参数。此时该参数的行为与任何其他引用一样。此外，你还可以传入 `nullptr` 表示“未定义状态”，这有时很有用。
- 作为 `unique_ptr` 的值参数会在调用时“消耗”该参数。传给函数的变量随后会变为空。当对象应当只走一条路径时，这很有用。这将是 *汇点*（或*排空*）设计模式的应用。
- 函数可以按值返回 `unique_ptr`。当你在函数内用 `new` 创建被包装的对象时，这尤其合适——本质上相当于一个*生产者函数*或*工厂*。
- 只有当指针事先已经存在时，你才返回对 `unique_ptr` 的引用。因此，从自由函数中，你返回一个参数；或者从方法中，返回类的数据成员。
- 作为类的数据成员，`unique_ptr` 很合适，因为你不必担心删除问题。与值不同，`unique_ptr` 可以有一个未定义阶段并存储 `nullptr`。它当然比裸指针更好。
- 你可以将 `unique_ptr` 放入标准容器。此时容器拥有它所包含的所有对象。如果你需要从另一个位置引用各个容器元素，可以通过对 `unique_ptr` 的引用，或作为指向被包装对象的裸指针来实现。如果你不想在另一个包含这些对象的容器中引用原容器的多个元素，后者很有用。

### 20.5.2 “shared_ptr”

shared_ptr 也用于受管的所有权，但它并不那么占有欲强。shared_ptr 愿意与许多其他对象共享它拥有的对象——只要它们也是 shared_ptr 或 weak_ptr。被包装的对象只存在一次。当最后一个引用该对象的 shared_ptr 消失时，该对象也会消失。

当不清楚谁拥有这些对象以及它们究竟应在何时被清理时——甚至当你确信有时会有多个实体拥有这些对象时——你可以使用这种机制。总而言之，shared_ptr 可能还有许多不同的用例，正是因为它允许在所有权方面有很大的自由。

```cpp
// https://godbolt.org/z/4KP9lZbq
#include <vector>
#include <iostream>
#include <memory>                    // shared_ptr
#include <random>                    // uniform_int_distribution, random_device
namespace {                          // Beginning of the anonymous namespace
using std::shared_ptr; using std::make_shared;
using std::vector; using std::cout;
struct Asteroid {
    int points_ = 100;
    int structure_ = 10;
};
struct Ship {
    shared_ptr<Asteroid> firedLastOn_{};
    int score_ = 0;
    int firepower_ = 1;
    bool fireUpon(shared_ptr<Asteroid> a);
};
struct GameBoard {
    vector<shared_ptr<Asteroid>> asteroids_;
    explicit GameBoard(int nAsteroids);
    bool shipFires(Ship& ship);
};
// Implementation of Ship
bool Ship::fireUpon(shared_ptr<Asteroid> a) {
    if(!a) return false;             // invalid asteroid
    a->structure_ -= firepower_;
    if(a.get() == firedLastOn_.get())
        firepower_ *= 2;              // increase damage
    else
        firepower_ = 1;               // reset
    firedLastOn_ = a;
    return a->structure_ <= 0;        // destroyed?
}
// Implementation of GameBoard
GameBoard::GameBoard(int nAsteroids) : asteroids_{}
{   // some standard asteroids
    for(int idx=0; idx<nAsteroids; ++idx)
        asteroids_.push_back( make_shared<Asteroid>() );
}
int rollDice(int min, int max) {
    /* static std::default_random_engine e;*/  // Pseudo-random generator
    static std::random_device e;            // random generator
    return std::uniform_int_distribution<int>{min, max}(e); // roll dice
}
bool GameBoard::shipFires(Ship &ship) {
    int idx = rollDice(0, asteroids_.size()-1);
    bool broken = ship.fireUpon(asteroids_[idx]);
    if(broken) {
        ship.score_ += asteroids_[idx]->points_;
        asteroids_.erase(asteroids_.begin()+idx);  // remove
    }
    return asteroids_.size() == 0;                // everything is destroyed
}
} // End of the anonymous namespace
int main() {
    GameBoard game{10};                           // 10 asteroids
    Ship ship{};
    for(int idx = 0; idx < 85; ++idx) {           // 85 shots
        if(game.shipFires(ship)) {
            cout << "The space is empty after " << idx+1 << " shots. ";
            break;
        }
    }
    cout << "You have scored " << ship.score_ << " points.\n";
}
```

**清单 20.6** 一个包含各种对象的游戏板。

如果你运行这个程序，运气好的话也许能清空“太空”。以下是几次运行的结果：

```text
You have reached 700 points.
You have reached 800 points.
You have reached 800 points.
You have reached 600 points.
Space is empty after 84 shots. You have reached 1000 points.
```
