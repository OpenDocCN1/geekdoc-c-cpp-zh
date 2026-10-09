
到目前为止，我们使用的数据都存储在当地变量或成员变量中。

局部变量不适合长期存储，因为它们的数据在变量超出作用域的瞬间就会被删除。

成员变量的存续时间仅与其包含该变量的对象相同。因此，存储在成员变量中的数据会在对象被删除后立即丢失。

使用 `new`，我们可以为数据创建长期存储。这些数据不会被自动删除，因此我们必须通过调用 `delete` 来手动删除它们。`new` 和 `delete` 就像是 `new[]` 和 `delete[]`，只不过它们创建和删除的是单个对象而非数组。当你使用了 `new[]` 时必须非常小心地使用 `delete[]`，当你使用了 `new` 时则必须使用 `delete`。

下面是一个使用 `new` 创建单独的 `Pair` 实例的示例。请注意对 `delete` 的调用以及 `->` 的使用。

```cpp
Pair* myPair = new Pair;
myPair->x = 1.3;
myPair->y = 2.5;

cout << "Pair (";
cout << (myPair->x);
cout << ", ";
cout << (myPair->y);
cout << ")\n";

delete myPair;
```

让我们看看如何使用以这种方式创建的数据在两个位置之间共享 `Instrument` 数据。

首先，我们为 `Position` 和 `Instrument` 定义类：

```cpp
class Instrument {
public:
    string bloombergTicker;
    string ricCode;
    string companyName;
    Instrument() {}
};

class Position {
public:
    string trader;
    double quantity;
    Instrument* instrument;
    explicit Position( Instrument* instrument );
};
```

```cpp
Position::Position( Instrument* instrument ) :
instrument( instrument ) {
}
```

你应该注意到，`Position` 包含一个指向 `Instrument` 的指针，而不是一个实际的 `Instrument`。你可以从字段 `Instrument` 的类型为 `Instrument*` 这一事实看出这一点。下面的代码初始化了一个由 `Position` 对象组成的向量，这些对象都指向同一个 `Instrument`。这就实现了我们共享数据的目标。

```cpp
vector<Position> constructPositions() {
// 该函数的调用者
// 在处理完所有位置后
// 应该对 instrument 调用 delete
vector<Position> positions;

Instrument* instrument = new Instrument;
instrument->companyName = "Google";
instrument->bloombergTicker = "GOOG US Equity";
instrument->ricCode = "GOOG.OQ";

Position p1(instrument);
p1.trader = "Han";
p1.quantity = 100.00;
positions.push_back( p1 );

Position p2(instrument);
p2.trader = "Leia";
p2.quantity = -100.00;
p2.instrument = instrument;
positions.push_back( p2 );

return positions;
}
```

然而，这里有一个陷阱，该函数的调用者被赋予了删除 instruments 的任务。

```cpp
void testConstructPositions() {
vector<Position> r = constructPositions();
int n = r.size();
for( int i=0; i<n; i++) {
cout << "Position "<<i<<"\n";
Position& p=r[i];
cout << "Trader "<<p.trader<<"\n";
cout << "Quantity "<<p.quantity<<"\n";
cout << "Instrument ";
cout << p.instrument->companyName<<"\n";
cout << "\n";
}
delete r[0].instrument;
}
```

`constructPositions` 的调用者必须精确知道如何调用 `delete`。这违反了信息隐藏原则——你需要了解 `constructPositions` 的实际工作方式才能安全地使用它。

## 危险！

初始化你的指针。我们在构造函数中初始化了字段 `instrument`。如果你不初始化指针，当你尝试使用它时，它将会灾难性地失败。

```cpp
// 不要这样做
Instrument* instrument;
cout << instrument->companyName << "\n";
```

有时你希望指定一个指针尚未指向任何对象，在这种情况下，你将其初始化为 `nullptr`。这里有一段代码，它在使用指针之前检查该指针是否为 `nullptr`。

```cpp
string getCompanyName( Position& position ) {
    if (position.instrument==nullptr) {
        return "Name not set";
    } else {
        return position.instrument->companyName;
    }
}
```

使用 `nullptr` 的危险在于，如果你忘记检查，你将遇到一个棘手的错误。

### 11.6.1 使用 shared_ptr 进行共享

类 `shared_ptr` 解决了删除问题。要使用 `shared_ptr`，你需要 `#include <memory>`。

`shared_ptr` 是一种所谓的“智能指针”的示例。这是一个 C++ 类，其行为像指针，但它可以代表你处理何时调用 `delete` 的问题。事实上，`shared_ptr` 是最通用的智能指针类，也是我们将在本书中唯一使用的类。

`shared_ptr` 的工作方式是，每个共享指针都会记录它被复制的次数。一旦现有的智能指针副本数量降为零，所指向的数据将被为你删除。具体如何实现这一点，我们要等到在第 16.2 节讨论析构函数时再介绍。

为了使用 `shared_ptr` 所做的改动非常简单。这里是一个新版本使用 `shared_ptr` 的 `Position` 类。

```cpp
class PositionV2 {
public:
    string trader;
    double quantity;
    shared_ptr<Instrument> instrument;
    explicit PositionV2(shared_ptr<Instrument> ins);
};

PositionV2::PositionV2(shared_ptr<Instrument> ins) :
    instrument( ins ) {
}
```

区别在于，它现在包含的是一个 `shared_ptr<Instrument>` 而不是 `Instrument*`。前者意味着“指向一个 instrument 的共享指针”，后者意味着“指向一个 instrument 的指针”。前者实际上更容易阅读，虽然不可否认的是它更难输入。

当我们使用 `shared_ptr` 时，我们可以像操作普通指针一样使用运算符 `->` 和 `*`。

```cpp
vector<PositionV2> constructPositionsV2() {
    vector<PositionV2> positions;

    shared_ptr<Instrument> ins
        = make_shared<Instrument>();
    ins->companyName = "Google";
    ins->bloombergTicker = "GOOG US Equity";
    ins->ricCode = "GOOG.OQ";

    PositionV2 p1(ins);
    p1.trader = "Han";
    p1.quantity = 100.00;
    positions.push_back( p1 );

    PositionV2 p2(ins);
    p2.trader = "Leia";
    p2.quantity = -100.00;
    p2.instrument = ins;
    positions.push_back( p2 );

    return positions;
}
```

关键的区别在于，我们使用函数 `make_shared` 而不是 `new` 来创建一个 `shared_ptr`。

```cpp
shared_ptr<Instrument> ins
       = make_shared<Instrument>();
```

`make_shared` 定义在 `<memory>` 中，是命名空间 `std` 的一部分。

引入 `shared_ptr` 的好处可以在调用函数中体现出来。

```cpp
void testConstructPositionsV2() {
   vector<PositionV2> r = constructPositionsV2();
   int n = r.size();
   for (int i=0; i<n; i++) {
     cout << "Position "<<i<<"\n";
     PositionV2& p=r[i];
     cout << "Trader "<<p.trader<<"\n";
     cout << "Quantity "<<p.quantity<<"\n";
     cout << "Instrument ";
     cout << p.instrument->companyName<<"\n";
     cout << "\n";
   }
 }
```

核心要点是我们不再需要调用 `delete`，因此信息隐藏原则已经恢复。

## 危险！

使用原始指针进行编程很难。你可能觉得你永远都不会忘记调用 `delete`，因此你可以不使用 `shared_ptr` 而使用指针，从而编写更快的代码。如果是这样，下面是一个可能会让你陷入困境的问题示例。

```cpp
int* a = new int[10];
int* b = new int[20000000];
cout << "Arrays created";
delete[] a;
delete[] b;
```

这段代码有什么错误？好吧，如果第二次调用 `new` 失败，因为我们内存不足并抛出错误怎么办？那么第一个对象将永远不会被删除。因此，当你的程序内存已经不足时，它刚刚泄漏了内存。它很快就会崩溃。

`shared_ptr` 对于大多数实际用途都工作得很好，但它确实存在一个问题：如果你的数据对象之间存在循环引用，那么它们将永远不会被删除。解决这个问题的方法要么避免循环引用，要么使用更智能的指针库。在本书中，我们选择简单地避免循环引用。

## 11.7 使用引用共享数据

你可以用指针做的很多事情，也可以用引用来做。例如，你可以拥有一个成员变量是引用。如果你通过引用存储数据，就像通过指针存储数据一样，可以节省内存。

使用引用而不是指针的一个优点是，你*必须*在构造函数中初始化作为引用的成员变量。这意味着由空指针和未初始化指针引起的错误在引用中是*不可能*发生的。

然而，使用引用成员变量通常不如选择 *shared_ptr* 成员变量有用。原因是，拥有一个对象的 *shared_ptr* 意味着你得到保证，对象不会在你不再需要它之前被删除。另一方面，如果你使用引用，存在别人可能会删除你的对象的风险。

让我们举一个例子，说明为什么通常不应该将引用用作成员变量。首先，我们定义一个新的 *Position* 类，其中包含一个指向 *Instrument* 的引用。

```cpp
class PositionV3 {
public:
   string trader;
   double quantity;
   Instrument& instrument;
   explicit PositionV3( Instrument& instrument );
};

PositionV3::PositionV3( Instrument& instrument ) :
   instrument(instrument) {
}
```

这段代码在技术上是正确的。特别要注意的是，我们在构造函数中初始化了成员变量引用，这是所必需的。

这种设计的问题在于，*Position* 类无法控制 *instrument* 何时被删除。以下代码起初似乎可以工作，它确实能编译：

```cpp
PositionV3 constructPositionV3() {
   // *这个函数不起作用，instrument*
   // *已被删除，因此所有返回的位置*
```

