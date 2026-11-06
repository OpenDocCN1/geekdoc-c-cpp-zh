
## 第1册

### 第8章 使用类

这只是一个没有返回类型的简单函数。它接受一个对象指针作为参数。例如，吃完一块奶酪后，你可以调用：

```
OneMoreCheeseGone(MyBlock);
```

现在考虑这一点：如果你有一个堆上的对象，它没有名字。你通过一个指向它的指针变量来访问它。但如果代码当前正在某个对象的成员函数内部执行呢？你如何引用这个对象本身？

C++ 在每个成员函数内部都有一个隐藏变量：this。它是一个指针变量。this 变量始终指向当前对象。因此，如果代码正在某个成员函数内部执行，而你想调用 OneMoreCheeseGone()，并传入当前对象（或者说那块奶酪），你会传入 this。

代码清单 8-8 中展示的 CheeseClass 示例演示了这一点。该清单包含四个主要部分。首先是名为 Cheese 的类的定义。这个类包含几个成员函数。

接下来是函数 OneMoreCheeseGone() 以及它所修改的一个全局变量。这个函数从全局变量中减 1，并把一个字符串存入传给它的对象的成员变量 status 中。

接下来是类 Cheese 的实际成员函数。（我们把这些函数放在 OneMoreCheeseGone() 函数之后，因为它们会调用它。如果我们使用函数原型作为 OneMoreCheeseGone() 的前向引用，顺序就无关紧要了。）

最后是 main()，它创建两个新的 Cheese 实例。然后它把全局变量设为 2，这个变量跟踪剩余奶酪块的数量。接下来，它对 asiago 奶酪调用 eat 函数，对 limburger 奶酪调用 rot 函数。然后它打印发生的所有事情的结果：显示 Cheese 计数，并显示每个对象的 status 变量。

#### 代码清单 8-8：使用 *this* 变量从成员函数内部传递对象

```cpp
#include <iostream>

using namespace std;

class Cheese
{
public:
    string status;
    void eat();
    void rot();
};

int CheeseCount;

void OneMoreCheeseGone(Cheese *Block)
{
    CheeseCount--;
    Block->status = "Gone";
}

void Cheese::eat()
{
    cout << "Eaten up! Yummy" << endl;
    OneMoreCheeseGone(this);
}

void Cheese::rot()
{
    cout << "Rotted away! Yuck" << endl;
    OneMoreCheeseGone(this);
}

int main()
{
    Cheese *asiago = new Cheese();
    Cheese *limburger = new Cheese();

    CheeseCount = 2;

    asiago->eat();
    limburger->rot();

    cout << endl;
    cout << "Cheese count: " << CheeseCount << endl;
    cout << "asiago: " << asiago->status << endl;
    cout << "limburger: " << limburger->status << endl;

    return 0;
}
```

运行代码清单 8-8 中的应用程序时，你会看到以下输出：

```text
Eaten up! Yummy
Rotted away! Yuck

Cheese count: 0
asiago: Gone
limburger: Gone
```

第一行是调用 asiago->eat() 的结果，它打印一条消息。第二行是调用 limburger->rot() 的结果，它打印另一条消息。

第三行只是变量 CheeseCount 中的值。计算机每次调用 OneMoreCheeseGone() 函数时，这个变量都会减 1。因为这个函数被调用了两次，所以 CheeseCount 从 2 变成 1，再变成 0。

最后两行显示两个对象中 status 变量的内容。（OneMoreCheeseGone() 函数已经把字符串 Gone 存入这些变量中。）

#### 代码清单 8-9（续）

```cpp
class Door
{
private:
    int HowManyInside;

public:
    void Start();
    void GoThrough(Cat *acat);
    void GoThrough(Dog *adog);
    void GoThrough(Human *ahuman);
};

void Door::Start()
{
    HowManyInside = 0;
}

void Door::GoThrough(Cat *somebody)
{
    cout << "Welcome, " << somebody->name << endl;
    cout << "A cat just entered!" << endl;
    HowManyInside++;
}

void Door::GoThrough(Dog *somebody)
{
    cout << "Welcome, " << somebody->name << endl;
    cout << "A dog just entered!" << endl;
    HowManyInside++;
}

void Door::GoThrough(Human *somebody)
{
    cout << "Welcome, " << somebody->name << endl;
    cout << "A human just entered!" << endl;
    HowManyInside++;
}

int main()
{
    Door entrance;
    entrance.Start();

    Cat *SneekyGirl = new Cat;
    SneekyGirl->name = "Sneeky Girl";

    Dog *LittleGeorge = new Dog;
    LittleGeorge->name = "Little George";

    Human *me = new Human;
    me->name = "Jeff";

    entrance.GoThrough(SneekyGirl);
    entrance.GoThrough(LittleGeorge);
    entrance.GoThrough(me);

    delete SneekyGirl;
    delete LittleGeorge;
    delete me;

    return 0;
}
```

这个应用程序让它们像人类一样进入。这个应用程序的开头声明了三个类：Cat、Dog 和 Human，每个类都有一个 name 成员。接下来是 Door 类。私有成员 HowManyInside 跟踪已经进来了多少个对象。然后是一个名为 `Start()` 的公有函数，它用于激活门。最后，这个类包含重载函数。它们都有相同的名称和相同的返回类型。返回类型可以不同，但它们必须通过参数来区分。这些函数确实如此；一个接受 Cat 指针，一个接受 Dog 指针，还有一个接受 Human 指针。

接下来是成员函数的代码。第一个函数 `Start()` 很容易激活。它把 HowManyInside 设为 0。接下来的三个函数是重载的。它们做类似的事情，但写出的消息略有不同。每个函数接受不同的类型。

然后我们有 `main()`，它创建一个 Door 实例。我们没有把它做成指针（只是为了展示在应用程序中可以把指针和栈变量混用）。创建 Door 实例后，我们调用了它的 `Start()` 函数。接下来，我们创建了三个生物实例：一个 Cat、一个 Dog 和一个 Human。我们还为每个实例设置了 name 成员变量。

然后我们调用 `entrance.GoThrough()` 函数。第一次传入一个 Cat，然后传入一个 Dog，再传入一个 Human。（听起来很疼。）因为你能看到 Door 类，所以你知道我们正在调用三个不同的函数，只是它们碰巧名称都相同。但是当我们*使用*这个类时，我们会把它们都看作一个函数，只是碰巧可以接受 Cat、Dog 或 Human。这就是重载的目标：创造出感觉像是同一个函数的多个*版本*。

### 以构造函数开始，以析构函数结束

#### 以构造函数开始

当你创建类的新实例时，可能希望对这个对象做一些基本设置。假设有一个名为 Apartment 的类，它有一个名为 NumberOfOccupants 的私有成员变量和一个名为 ComeOnIn() 的成员函数。ComeOnIn() 的代码会把 NumberOfOccupants 加 1。

当你创建 `Apartment` 的新实例时，可能希望让 `NumberOfOccupants` 从 0 开始。最好的办法是给类添加一个特殊的成员函数，即*构造函数*。这个成员函数有一行类似这样的代码

```cpp
NumberOfOccupants = 0;
```

每当你创建类 `Apartment` 的新实例时，计算机首先会为你的新对象调用这个构造函数，从而把 `NumberOfOccupants` 设为 0。

把构造函数看作一个*初始化函数*：当你创建新对象时，计算机会调用它。

要编写构造函数，就把它作为另一个成员函数添加到类中，并把它设为 public。构造函数的名称与类名相同。对于类 `Apartment`，我们会把构造函数命名为 `Apartment()`。构造函数没有返回类型，连 `void` 也没有。构造函数中可以带有参数；参见本章后面的“向构造函数添加参数”。

本节后面的代码清单 8-10 展示了一个示例构造函数以及一个*析构函数*，我们将在下一节介绍析构函数。

#### 以析构函数结束

当你删除类的实例时，可能希望有一些*清理*代码，在对象前往天上的教室之前把相关事项整理清楚。例如，你的对象可能有一些成员变量是指向其他对象的指针。你可能想删除那些其他对象。

你把清理代码放在一个名为析构函数的特殊函数中。*析构函数*是一个终结函数，计算机会在删除你的对象之前调用它。

析构函数的名称与类名相同，只是名称开头有一个波浪号 `~`。（波浪号通常位于键盘左上角。）对于名为 `Squirrel` 的类，析构函数会是 `~Squirrel()`。析构函数没有返回类型，连 `void` 也没有，因为不能从析构函数返回任何内容（毕竟对象已经不存在了）。你只需以函数名开头，并且不带参数。

![](img/6ba99460b0feb3585671a4612ff5fabb_219_0.png)

下一节“构造函数和析构函数示例”将展示一个同时使用构造函数和析构函数的例子。

构造函数和析构函数是 C++ 程序员的日常。几乎每个类都有构造函数，许多类还有析构函数。
