

![](img/128ab511de4e7360e167e3b15cdd5dd0_597_0.png)

通常，当你有一个容器类，其中保存着另一个类的多个实例时，你会想使用这种方法。例如，你可能有一个名为 `Peripheral` 的类。你也可能有一个名为 `PeripheralList` 的容器类，它保存 `Peripheral` 的实例。之后你可能会从 `Peripheral` 派生出一个新类，名为 `Printer`，并从 `PeripheralList` 派生出一个新类，名为 `PrinterList`。如果 `PeripheralList` 有一个返回 `Peripheral` 实例的函数，你会在 `PrinterList` 中重写该函数。但不是让它返回 `Peripheral` 的实例，而是让它返回 `Printer` 的实例。清单 4-1 中所示的 OverridingDerived 示例展示了如何完成这项任务。

### 代码清单 4-1：重写并返回派生类

```cpp
#include <iostream>
#include <map>

using namespace std;

class Peripheral {
public:
  string Name;
  int Price;
  int SerialNumber;
  Peripheral(string aname, int aprice, int aserial) :
    Name(aname), Price(aprice),
    SerialNumber(aserial) {}
};

class Printer : public Peripheral {
public:
  enum PrinterType {laser, inkjet};
  PrinterType Type;
  Printer(string aname, PrinterType atype, int aprice,
    int aserial) :
    Peripheral(aname, aprice, aserial), Type(atype) {}
};

typedef map<string, Peripheral *> PeripheralMap;

class PeripheralList {
public:
  PeripheralMap list;
  virtual Peripheral *GetPeripheralByName(string name);
  void AddPeripheral(string name, Peripheral *per);
};

class PrinterList : public PeripheralList {
public:
  Printer *GetPeripheralByName(string name);
};

Peripheral *PeripheralList::GetPeripheralByName(string name) {
  return list[name];
}

void PeripheralList::AddPeripheral(string name, Peripheral *per) {
  list[name] = per;
}

Printer *PrinterList::GetPeripheralByName(string name) {
  return static_cast<Printer *>(
    PeripheralList::GetPeripheralByName(name));
}

int main(int argc, char *argv[]) {
  PrinterList list;
  list.AddPeripheral(string("Koala"),
    new Printer("Koala", Printer::laser,
    150, 105483932)
  );
  list.AddPeripheral(string("Bear"),
    new Printer("Bear", Printer::inkjet,
    80, 5427892)
  );

  Printer *myprinter = list.GetPeripheralByName("Bear");
  if (myprinter != 0) {
    cout << myprinter->Price << endl;
  }
  return 0;
}
```

这个示例使用了一种称为 `map` 的特殊类型，它只是一个容器或列表，以成对的形式保存项。对中的第一项称为*键*，第二项称为*值*。你可以根据键从 map 中检索值。这个示例根据名称（字符串，即键）存储 Peripheral（值）。

## 多重继承

在 C++ 中，通常最好只有一个基类供你的类继承。然而，也可以从多个基类继承，这一过程称为*多重继承*。

### 使用多重继承

一个类可能具有你希望在派生类中拥有的某些特性，而另一个类可能具有你希望在同一派生类中拥有的其他特性。如果是这种情况，你可以通过多重继承从两者继承。

多重继承很混乱，并且很难正确实现。但如果你谨慎使用它，就能让它发挥作用。清单 4-2 中所示的 `DerivingTwoDiff` 示例展示了如何完成这项任务。

![](img/128ab511de4e7360e167e3b15cdd5dd0_600_0.png)

**记住**

### 代码清单 4-2：从两个不同的类派生

```cpp
#include <iostream>

using namespace std;

class Mom {
public:
    void Brains() {
        cout << "I'm smart!" << endl;
    }
};

class Dad {
public:
    void Beauty() {
        cout << "I'm beautiful!" << endl;
    }
};

class Derived : public Mom, public Dad {
};

int main(int argc, char *argv[]) {
    Derived child;
    child.Brains();
    child.Beauty();
    return 0;
}
```

运行这段代码时，你会看到以下输出：

```text
I'm smart!
I'm beautiful!
```

在前面的代码中，Derived 类继承了 Mom 和 Dad 两个类的函数。正因如此，编译器允许 Derived 的实例 child 调用这两个函数。你可以使用这种方法从多个类派生：

```cpp
class Derived : public Mom, public Dad
```

与单继承一样，你从单个冒号右侧的基类开始，并用逗号分隔各个类。你还要在每个类前加上继承类型 public。

### 在多重继承中设置访问权限

与单继承一样，你可以使用 public 之外的继承方式。但你不必对所有类使用相同的访问权限。例如，下面的写法虽然有点令人困惑，但可以接受：

```cpp
class Derived : public Mom, protected Dad
```

这意味着从 Dad 派生的 public 成员现在在 Derived 类中变为 protected，这也意味着用户不能调用从 Dad 继承的方法，也不能访问从 Dad 继承的任何属性。如果你在清单 4-2 中使用了这种继承方式，下面这行代码将不再有效：

```cpp
child.Beauty();
```

如果你尝试编译它，就会看到以下错误，因为 Beauty() 成员现在是 protected：

```text
'void Dad::Beauty()' is inaccessible
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_601_0.png)

使用多重继承时，请注意理解你的代码在做什么。尽管它可能正确编译，但仍可能无法正确运行，从而导致那种著名的令人毛骨悚然的东西——bug。

### 观察多重继承出错

多重继承可能会发生奇怪、离奇、诡异的事情。如果两个基类都有一个名为 Bagel 的属性，编译器就会混淆。假设你用 Bagel 效果增强这两个基类（如 DerivingTwoDiff2 示例所示）：

```cpp
class Mom {
public:
    int Bagel;
    void Brains() {
        cout << "I'm smart!" << endl;
    }
};

class Dad {
public:
    int Bagel;
    void Beauty() {
        cout << "I'm beautiful!" << endl;
    }
};

class Derived : public Mom, public Dad {
};
```

在前面的代码中，Mom 和 Dad 这两个基类各自都有一个 Bagel 成员。编译器会允许你这样做。但如果你尝试访问该成员，如下面的代码所示，就会出错：

```cpp
Derived child;
child.Bagel = 42;
```

以下是我们在 Code::Blocks 中看到的错误消息：

```text
error: request for member 'Bagel' is ambiguous
```

该消息意味着编译器不确定代码指的是哪个 Bagel：是从 Mom 继承的那个，还是从 Dad 继承的那个。如果你编写这样的代码，请确保你知道自己指的是哪个继承成员，以便修复问题。

![](img/128ab511de4e7360e167e3b15cdd5dd0_602_0.png)

现在这看起来会很奇怪，但它是正确的。假设你指的是从 Mom 继承的 Bagel。你可以把名称 Mom 放在单词 Bagel 前面，并用两个冒号分隔：

```cpp
child.Mom::Bagel = 42;
```

是的，这确实正确，尽管看起来有点奇怪。如果你想引用来自 Dad 的那个，可以这样做：

```cpp
child.Dad::Bagel = 17;
```

这两行都能正确编译，因为你消除了所有歧义。此外，你可以使用同样的技巧分别访问它们：

```cpp
cout << child.Mom::Bagel << endl;
cout << child.Dad::Bagel << endl;
```

### 虚继承

有时，在派生新类时，你可能会看到加入 `virtual` 这个词，如下所示：

```cpp
class Diamond : virtual public Rock
```

加入 `virtual` 是为了修复可能出现的一个奇怪问题。当你使用多重继承时，可能会遇到一种疯狂的情况：出现菱形继承，如图 4-1 所示。

在图 4-1 中，你可以看到基类是 Rock。Diamond 和 Jade 类派生自 Rock。此时，代码使用多重继承从 Diamond 和 Jade 派生出 MeltedMess 类。是的，你可以这样做。但你必须小心。

![](img/128ab511de4e7360e167e3b15cdd5dd0_603_0.png)

