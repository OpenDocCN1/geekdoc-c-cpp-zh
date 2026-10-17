
`public`:

```
Derived(char *s) : Base(s) {

    upper = new char[strlen(s) + 1];

    strcpy(upper, toupper(s));

}

~Derived() {

    delete [] upper;

}

char *getUpper() {

    return upper;

}

};
```

```cpp

int main() {

    Derived d("Haley Laurel");

    cout << d.getStr() << endl;

    cout << d.getUpper() << endl;

    return 0;

}

```

output:
Haley Laurel
HALALY LAUREL

注意，`Derived` 构造函数调用了 `Base` 构造函数，后者拷贝了 `s` 所指向的字符串。当 `Base` 类型对象离开作用域时，析构函数会删除此内存块。

## 构造函数重载

使用现有实例初始化类会调用拷贝构造函数。记住，如果你没有写构造函数，编译器会自动提供一个。注意，即使你为派生类写了拷贝构造函数，编译器也不会自动调用基类的拷贝构造函数。

## 重载赋值运算符

在派生类中重载赋值运算符的处理方式与重载拷贝构造函数类似。当你需要在派生类中编写一个重载的 `operator=()` 函数时，你有责任在该函数中显式地调用基类中重载的 `operator=()` 函数。

与重载拷贝构造函数不同，你对何时进行此调用有完全的控制权，尽管立即进行该调用是有合理的，这样派生对象的基类部分就可以先获得数据成员赋值，然后是处理派生部分。

请记住，如果基类没有重载赋值运算符，编译器将只提供一个（我们可能并不喜欢它）。

```cpp

// assign.cpp

#include <iostream>

using namespace std;

class Base {

protected:

    int bnum;

public:

    Base(int x=0) : bnum(x) {

        cout << "base constructor" << endl;

    }

    Base(const Base& b) : bnum(b.bnum) {

        cout << "base copy constructor" << endl;

    }

    Base& operator=(const Base& b) {

        cout << "base operator=" << endl;

        if (&this != &b) {

            bnum = b.bnum;

        }

        return *this;

    }

    ~Base() {

        cout << "base destructor" << endl;

    }

    int getBnum() const {

        return bnum;

    }

};

```

```cpp

class Derived : public Base {

  private:

    int dnum;

  public:

    Derived(int x=0, int y=0) : Base(x), dnum(y) {

        cout << "derived constructor" << endl;

    }

    Derived(const Derived& d) : Base(d), dnum(d.dnum) {

        cout << "derived copy constructor" << endl;

    }

    Derived& operator=(const Derived& d) {

        cout << "derived operator=()" << endl;

        if (&d != &this) {

            Base::operator=(d);

            dnum = d.dnum;

        }

        return *this;

    }

    ~Derived() {

        cout << "derived destructor" << endl;

    }

    int getDnum() const {

        return dnum;

    }

};

int main() {

  Derived d1(1, 2);

  Derived d2;

  d2 = d1;

  cout << "d2 = " << d2.getBnum() << ", " << d2.getDnum() << endl;

  return 0;

}

```

output:
base constructor
derived constructor
base constructor
derived constructor
derived operator=()
base operator=
d2 = 1 2
derived destructor
base destructor
derived destructor
base destructor

注意，对函数 `Base::operator()` 的显式调用是使用函数符号编写的。如果你想使用中缀符号，可以使用以下两种方法：

- `(Base*)this = d;`
- `((Base&)*this) = d;`

第一个语句将 Derived 指针转换为 Base 指针，然后对结果进行解引用，产生调用实例的 Base 类部分。因此，将调用基类的 `operator=()`。

第二个语句实现了相同的结果，但方式更加直接，调用实例本身现在被转换为 Base 类的引用。

## 从派生类向基类的转换

将派生类实例、指针或引用转换为相同类型的基类对象，对编译器来说没有问题。我们之前已经看到派生类拷贝构造函数中的“指向派生类的引用”是如何传递给基类拷贝构造函数并作为“指向基类的引用”被接收的。

由于派生类实例始终包含一个基类实例，当转换发生时，编译器简单地忽略正在使用、指向或引用的实例的派生类部分。例如：

```cpp

Derived d(1, 2);

```

创建了一个派生类对象。

```cpp

Base b = d;

```

创建了一个基类对象。然而，这里使用一个派生实例来初始化一个基类实例。对象 b 现在只包含对象 d 的 Base 类部分。

```cpp

Base *pbase = new Derived;

```

在这个示例中，`new Derived` 返回指向 Derived 对象的指针，并用于初始化一个指向 Base 对象的指针。换句话说，指向 Derived 的指针被用于初始化指向 Base 的指针。因此，pBase 只“看到”了堆上 Derived 对象的 Base 类部分。

请记住，由于派生类实例始终包含一个基类实例，当转换发生时，编译器简单地忽略了所指向实例的 Derived 类部分。

## 从基类向派生类的转换

相反，如果你尝试将基类实例、指针或引用转换为相同类型的派生类对象，编译器将会报错，因为你现在尝试做的是将一个较小的对象（基类）放入一个较大的对象（派生类）中。编译器不会让你自动执行此操作。我们暂时不担心这个问题。

## 指向基类和派生类实例的指针

正如我们已经看到的，指向基类和派生类实例的指针可以像其他类型指针一样声明。在赋值方面，你始终可以将派生类指针赋值给基类指针，因为派生类实例始终包含一个基类实例。

- 基类指针始终可以指向基类实例
- 派生类指针始终可以指向派生类实例

当使用类型为 Base 的指针调用成员函数，且该函数在基类和派生类中都有定义时，不存在歧义。这里的决定因素是指针的类型。

```cpp

class Base {

public:

    void print() { cout << "Base class print()" << endl; }

}

class Derived : public Base {

  public:

    void print() { cout << "Derived class print()" << endl; }

};

int main() {

  Base* pBase = new Base; // 基类实例

  Derived* pDerived = new Derived; // 派生类实例

  pBase->print(); // 调用 Base class()

  pDerived->print(); // 调用 Derived class()

  pDerived->Base::print(); // 调用 Base()

  delete pBase;

  delete pDerived;

  return 0;

}

```

output:
Base class print
Derived class print
Base class print

注意 `pBase->Derived::print()` 是不允许的。声明了两个指针并各自调用其所属类的 `print()` 函数。此外，只要使用作用域运算符限定函数名，派生类指针就可以调用基类的函数。

## 指向派生类对象的基类指针

当使用基类指针存储派生类对象的地址时，情况会变得有趣得多。这对编译器来说没有问题，因为指针实际上只是指向派生实例的基类部分。（记住，派生类实例始终包含一个基类实例）。

现在，假设指向派生类对象的基类指针被用于调用一个在基类中定义并在派生类中重写的成员函数。哪个函数会被调用？

答案是将使用基类的成员函数！

为什么？

因为编译器在编译时就会生成函数的偏移地址，即使指针中存储的实例地址在运行时可能会改变。因此，编译器必须生成：

> “我知道指针的类型是基类，所以我将生成一个相对于某个基类实例起始位置的地址。”

如果在运行时，指针所指向的实例是 Derived 类类型，那太遗憾了，我仍然会调用基类中的函数，而不是派生类中重写的函数。

```cpp

class Base {

public:

    void print() { cout << "Base Class Print()" << endl; }

};

class Derived : public Base {

public:

    void print() { cout << "Derived class Print()" << endl; }

};

```

```cpp

int main() {

    Base* pBase = new Derived();

    pBase->print(); // calls Base::print

    delete pBase;

    return 0;

}

```

output:
Base class print()

如果这个结果让你感到困扰，那么你的直觉是对的，因为“锁定”在基类世界中没有任何实际作用，尽管基类指针可以合法地指向各种派生类对象。

如果你考虑任何类型的容器对象（例如数组、链表、队列、栈、树等），这些对象可能将基类指针作为其数据，这种情况会变得尤为令人困扰。

例如，假设我们正在经营一家二手车行，我们声明了一个基类 `Vehicle`，并从 `Vehicle` 类派生了多个派生类（雷克萨斯、福特、宝马）。因此我们还创建了一个基类指针数组，即指向 `Vehicle` 对象的指针，并将每个基类指针指向一个动态创建的派生对象（雷克萨斯、福特、宝马）。所以，我们的库存由指向车场内各种汽车的“指针”集合组成。随后有人要求我们提供一份所有现有汽车的清单。于是，我们开始扫描指针集合，并向每辆车发送某种“请自我介绍”的消息，理所当然地期望每辆车都能以某种独特的方式标识自己。遗憾的是，就目前而言，我们从所有汽车那里得到的唯一响应类型实际上是：“我是一辆汽车（I AM A VEHICLE）”。消息发送到了基类的 `identify()` 函数，而永远到达派生类中的 `identify()` 函数。这没什么用！

我们将如何从这种局面中出来是多态和虚函数的主题。

## 容器关系与继承作业

1. 创建两个类 A 和 B，带有向标准输出声明自己身份的默认构造函数。从 A 派生一个名为 C 的新类，并在 C 中创建一个 B 类的成员对象，但不要为 C 创建构造函数。在 `main()` 中创建一个 C 类的对象并解释执行结果。

2. 创建一个三层级的类层次结构，并带有默认构造函数和析构函数，这两者都会向 `cout` 声明自己的身份。验证对于一个最派生类型的对象，所有三个构造函数和析构函数是否都会自动调用。解释这些调用的顺序。

3. 作为军事视频游戏的一部分，一个设计师创建了一个车辆类层次结构。基类是 `Vehicle`，它的派生类有 `AirVehicle`、`LandVehicle` 和 `SeaVehicle`。`SeaPlane` 类同时自 `AirVehicle` 和 `SeaVehicle`。具体来说，开发 `SeaPlane` 类时必须考虑哪些设计问题？

4. 在不执行以下代码的情况下，给出程序的输出。

```cpp

class A {

protected:

    int fa;

public:

    A(int va = 0) : fa(va) {

        cout << "A constructor" << endl;

    }

    A(const A& va) : fa(va.fa) {

        cout << "A copy constructor " << endl;

    }

    ~A() {

        cout << "A destructor" << endl;

    }

    A& operator=(const A& va) {

        cout << "A operator" << endl;

        fa = va.fa;

        return *this;

    }

};

```

```cpp

class B : public A {

  protected:

    int fb;

  public:

    B(int va = 0, int vb = 0) : fb(vb), A(va) {

      cout << "B constructor " << endl;

    }

    B(const B& vb) : fb(vb.fb), A(vb) {

      cout << "B copy constructor " << endl;

    }

    ~B() {

      cout << "B destructor" << endl;

    }

    B& operator=(const B& vb) {

      cout << "B operator" << endl;

      A::operator=(vb.fb);

      return *this;

    }

};

int main() {

  B b1(1, 2);

  B b2;

  b2 = b1;

  B b3(b1);

}

```

## 继承实验（String 类）

C++ 中定义最流行的类之一是模拟 C 语言字符串字面量的类。原原因是字符串在 C 中不是内置类型，但它又被频繁使用。因此，为了对字符串进行各种操作，你必须调用 `string.h` 库中的函数来执行诸如拷贝、复制、比较等操作。在 C++ 中，这种需求通过使用函数和运算符重载被消除了。为了表示 String 对象的状态，你将使用两个数据成员：

- 字符串的长度 `length`，类型为 `int`
- 指向 `char*` 类型字符串字面量的指针 `buf`

使用指向字符的指针（`char*`）而不是固定长度的字符数组，以便于在运行时（通过 `operator new`）分配内存，因此对字符串的长度不施加任何限制（太大或太小）。长度字段并非严格强制，因为始终可以通过 `strlen()` 函数从字符串指针获取长度。然而，避免重复调用 `strlen()` 也许是一个好主意。

## 重载构造函数函数

每个 String 实例的创建都涉及在堆上分配空间、拷贝字符串字面量并相应地设置长度数据成员。由于 String 对象有许多初始化方式，因此 String 类的构造函数必须经过重载以适应所有情况。

首先，如果带没有任何初始化带创建一个 String 对象，则将调用默认构造函数。

```cpp

String();

```

其次，由于字符串字面量（`char*`）与 String 类之间存在如此密切的关系，应该基于该字面量创建一个 String 对象。在这种情况下，必须对字面量进行拷贝以便封装到类中。

```cpp

String(const char*);

```

第三，可能有用从一个字符创建一个 String 对象。

```cpp

String(char);

```

第四，这里有一个从 `int` 创建 String 对象的构造函数。这意味着在堆上分配字节，并将第一个字节设置为 `NULL`。注意，小于零的值应被解释为零。

```cpp

String(int);

```

回顾我们对拷贝构造函数的讨论，如果你没有编写一个，编译器会自动提供一个。这对于不包含指针成员的类没有问题，但如果存在一个指针成员，就会产生大问题。其原因是两个或多个指针成员可能指向堆上的同一空间，结果是接收实例的相应指针数据成员将指向该空间。因此，现在有必要为 String 类创建一个拷贝。

```cpp

String(const String&);

```

最后，可能有用用字符和次数创建并初始化 String 对象。

```cpp

String(char, int);
```
