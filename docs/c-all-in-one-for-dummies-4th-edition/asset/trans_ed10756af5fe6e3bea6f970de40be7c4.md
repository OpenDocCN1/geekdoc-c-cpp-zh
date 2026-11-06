
## 定义标准的 this 指针用法

本节介绍在当今大多数应用程序中，this 如何用于应用程序开发。清单 1-9 中展示的 CheeseClass 示例演示了这一点。

**清单 1-9：** 在其方法内部使用 this 变量传递对象

```
#include <iostream>

using namespace std;

class Cheese {
public:
    string status;
    void eat();
    void rot();
};

int CheeseCount;

void OneMoreCheeseGone(Cheese *Block) {
    CheeseCount--;
    Block->status = "Gone";
};

void Cheese::eat() {
    cout << "Eaten up! Yummy" << endl;
    OneMoreCheeseGone(this);
}

void Cheese::rot() {
    cout << "Rotted away! Yuck" << endl;
    OneMoreCheeseGone(this);
}

int main() {
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

这个清单包含四个主要部分。首先是名为 Cheese 的类的定义。该类包含几个方法。

接下来是函数 `OneMoreCheeseGone()` 以及它所修改的全局变量。该函数从全局变量中减去 1，并将一个字符串存储到传入对象的属性 status 中。

接下来是 Cheese 类的实际方法。（你必须将这些函数放在 `OneMoreCheeseGone()` 之后，因为它们会调用它。如果你使用函数原型作为 `OneMoreCheeseGone()` 的前向引用，那么顺序就无关紧要。）

最后，`main()` 创建两个新的 Cheese 实例。然后它将全局变量设置为 2，该变量跟踪剩余的块数。接下来，它为 `asiago` 奶酪调用 `eat()` 函数，为 `limburger` 奶酪调用 `rot()` 函数。然后它打印所发生一切的结果：显示 Cheese 计数，并显示每个对象的状态。

运行清单 1-9 中的应用程序时，你会看到以下输出：

```
Eaten up! Yummy
Rotted away! Yuck

Cheese count: 0
asiago: Gone
limburger: Gone
```

第一行是调用 `asiago->eat()` 的结果，它会打印一条消息。第二行是调用 `limburger->rot()` 的结果，它会打印另一条消息。第三行只是变量 CheeseCount 中的值。每次计算机调用 OneMoreCheeseGone() 时，这个变量都会*递减*一次。由于该函数被调用了两次，CheeseCount 从 2 变为 1 再变为 0。最后两行显示两个对象中 status 变量的内容。（OneMoreCheeseGone() 将 "Gone" 存储在这些变量中。）

仔细看看 OneMoreCheeseGone() 函数。它通过将传入的当前对象的 status 变量设置为字符串 Gone 来操作该对象。`eat()` 方法调用它，并使用 `this` 传入当前对象。`rot()` 方法也调用它，同样通过 `this` 传入当前对象。

## C++ 20 中对 this 指针的更改

除非你实际上要在相当详细的层面上使用 C++ 20，否则你很可能可以跳过本节，而不会真正错过太多。当然，你可能只是好奇，而学习新东西总是一件好事。

C++ 20 随之对 `this` 指针带来了一些更改。尽管直到第 3 册你才会看到有关函数式编程的内容，但重要的是要知道，就像本章中的示例一样，你可以在 lambda 表达式中使用 `this` 指针。一个 *lambda 表达式* 是一种基于数学的方法，用于处理某些类型的编程问题，它简洁且比某些标准 C++ 方法更容易理解。你也可以像传递任何其他参数一样，将 lambda 表达式（本质上是一种函数）传递给其他函数。lambda 表达式中 `this` 指针用法的变化只是一种澄清——你现在必须实际声明使用 `this` 指针，然后才被允许使用它。你可以在以下内容中大致了解 lambda 表达式：

**清单 1-10：** *(续)*

```
    HowManyInside++;
}

void Door::GoThrough(Human *somebody) {
    cout << "Welcome, " << somebody->name << endl;
    cout << "A human just entered!" << endl;
    HowManyInside++;
}

int main() {
    Door entrance;
    entrance.Start();

    Cat *SneakyGirl = new Cat;
    SneakyGirl->name = "Sneaky Girl";
    Dog *LittleGeorge = new Dog;
    LittleGeorge->name = "Little George";
    Human *me = new Human;
    me->name = "John";

    entrance.GoThrough(SneakyGirl);
    entrance.GoThrough(LittleGeorge);
    entrance.GoThrough(me);

    delete SneakyGirl;
    delete LittleGeorge;
    delete me;
    return 0;
}
```

该应用程序允许狗和猫像人一样进入。这个应用程序的开头声明了三个类：Cat、Dog 和 Human，每个类都有一个 name 成员。接下来是 Door 类。私有成员 HowManyInside 跟踪已经有多少个生物进入。Start() 函数激活门。最后，该类包含重载函数。它们都具有相同的名称和相同的返回类型。你可以有不同的返回类型，但为了让编译器将这些函数识别为不同的函数，它们必须通过参数来区分。这些函数确实如此；一个接受 Cat 指针；一个接受 Dog 指针；一个接受 Human 指针。

接下来是这些方法的代码。第一个函数 Start() 将 HowManyInside 设置为 0。接下来的三个函数是重载的。它们做类似的事情，但写出略有不同的消息。每个函数接受不同的类型。

`main()` 中的第一步是创建一个 Door 实例。代码没有使用指针，以表明在应用程序中可以将指针与栈变量混用。创建 Door 实例后，代码调用 `Start()`。接下来，代码创建三个生物实例：Cat、Dog 和 Human，并为每个实例设置 name 属性。

对 `entrance.GoThrough()` 方法的调用分别传入 Cat、Dog 和 Human（按此顺序）。由于你可以看到 Door 类，你知道代码调用了三个名称都相同的不同方法。但在使用该类时，你会把它们看作一个接受 Cat、Dog 或 Human 的方法。这就是重载的目标：创建出感觉像是同一个函数的多个版本。运行此应用程序时，你会看到以下内容：

```
Welcome, Sneaky Girl
A cat just entered!
Welcome, Little George
A dog just entered!
Welcome, John
A human just entered!
```

## 以构造函数和析构函数开始和结束

你可以向类中添加两个特殊方法，让你提供特殊的启动和关闭功能：*构造函数*和*析构函数*。以下各节将详细介绍这些方法。

### 从构造函数开始

创建类的新实例时，你可能想进行一些基本的对象设置。假设你有一个名为 Apartment 的类，它有一个名为 `NumberOfOccupants` 的私有属性，以及一个名为 `ComeOnIn()` 的方法。`ComeOnIn()` 的代码会将 `NumberOfOccupants` 加 1。

创建 Apartment 的新实例时，你可能希望将 `NumberOfOccupants` 初始化为 0。做到这一点的最佳方法是向类中添加一个特殊方法，即 *构造函数*。该方法包含一行类似下面的代码：

```
NumberOfOccupants = 0;
```
