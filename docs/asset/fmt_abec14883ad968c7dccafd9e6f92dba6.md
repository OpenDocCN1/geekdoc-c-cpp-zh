
`const string &Orkan::Converse()`

```
{
    return Humanoid::Converse(); // 使用作用域解析来
    // 避免递归
}
```

在上述的 `Orkan` 类中，我们使用公共继承从 `Humanoid` 派生出 `Orkan`。一个 `Orkan` **是一个** `Humanoid`（Is-A `Humanoid`）。因此，`Humanoid` 中所有的公共接口对 `Orkan` 实例都是可用的。注意，我们的备用构造函数根据 `Orkan` 方言将默认问候消息设置为 `"Nanu nanu"`。

由于我们希望 `Orkan` 是一个具体的、可实例化的类，我们必须覆盖 `Humanoid::Converse()` 并在 `Orkan` 类中提供实现。然而，`Orkan::Converse()` 仅仅调用了 `Humanoid::Converse()`。也许 `Orkan` 认为其基类中的默认实现是可以的。注意，我们在 `Orkan::Converse()` 方法中使用 `Humanoid::` 作用域限定 `Converse()` 以避免递归。

有趣的是，如果 `Humanoid` 不是一个抽象类，`Orkan` 就不需要覆盖 `Converse()`——默认行为将被自动继承。然而，由于 `Humanoid` 被定义为抽象类，在 `Orkan` 中覆盖 `Converse()` 是必要的，否则 `Orkan` 也将被视为一个抽象类。别担心！我们可以利用默认 `Humanoid::Converse()` 的优势，仅需在 `Orkan::Converse()` 中调用它。这既满足了使 `Orkan` 具体的化的要求，又允许 `Humanoid` 保持抽象，同时仍为 `Converse()` 提供了罕见的默认行为！

### 目标类 Romulan

现在，让我们来看我们的下一个具体目标类：`Romulan`：

```cpp
class Romulan: public Humanoid
{
public:
    Romulan() = default; // 默认构造函数
    Romulan(const string &n2, const string &nl,
        const string &:): Humanoid(n2, nl, t, "jolan'tru")
    { }
    // 不需要默认构造函数原型
    // Romulan(const Romulan &h) = default;
    // 默认 op= 足够，因此下面注释掉，但
    // 让我们回顾一下如果需要的话如何编写它
    // 注意在调用基类后进行显式的返回转型
    // 类 Humanoid::operator= 以匹配返回类型
    // Romulan::operator=(const Romulan &h)
    {
        // 返回 dynamic_cast<Humanoid&>
        (Humanoid::operator=(h)); }
    // 析构函数原型。由于基类析构函数是虚的，不需要
    ~Romulan() override = default; // 虚析构函数
    const string &Converse() override;
};

// 必须覆盖 Converse 使 Romulan 成为具体类
const string &Romulan::Converse()
{
    return Humanoid::Converse(); // 使用作用域解析来
    // 避免递归
}
```

快速查看一眼上述的 `Romulan` 类，我们注意到此通知与其兄弟类 `Orkan` 类似。我们注意到传递给基类构造函数的默认问候消息是 `"jolan tru"`，以反映 `Romulan` 方言。我们本可以将 `Romulan::Converse()` 的实现写得更复杂，但我们选择了没有这样做。我们可以快速理解这个类的完整范围。

### 目标类 Earthling

接下来，让我们来看我们的第三个目标类：`Earthling`：

```cpp
class Earthling: public Humanoid
{
public:
    Earthly() = default; // 默认构造函数
    Earthly(const string &n2, const string &nl,
    const string &t): Humanoid(n2, nl, t, "Hello") { 
    // 不需要默认拷贝构造函数原型类型
    // Earthly(const Romulan &h) = default;
    // 默认 op= 足够，因此下面注释掉，但
    // 让我们回顾一下如果需要的话我们将如何编写它
    // 注意在调用基类后进行显式的 Earthly 转型
    // 类 Humanoid::op= 此处需要匹配返回类型
    // Earthly &operator==(const Earthly &)
    { return dynamic_cast<Earthly &
        (Humanoid::operator=(h));
    }
    // 析构函数原型。由于基类析构函数是虚的，不需要
    ~Earthly() override = default; // 虚析构函数
    const string& Converse(const Earthly &) override;
};

// 必须覆盖以使 Earthling 成为具体类
const string &Earthly::Converse()
{
    return Humanoid::Converse(); // 使用作用域解析来
} // 避免递归
```

再次快速查看一眼上述的 `Earthling` 类，我们注意到这个具体目标与其兄弟类 `Orkan` 和 `Romulan` 相似。

现在我们已经定义了被适配器（Adaptee）、适配器（Adapter）以及多个目标类（Target），让我们通过检查程序的客户端（Client）部分将这些部分整合起来。

## 整合模式组件

最后，让我们考虑在整个应用程序中示例客户端可能可能是什么样的。无疑，它可能由许多包含各种类的文件组成。在最简单的形式下（如下），客户端将包含一个 `main()` 函数来驱动应用程序。现在让我们来看看我们的 `main()` 函数，看看模式是如何组织的：

```cpp
int main() {
    list<Humanoid *> allies;
    Orkan *ol = new Orkan("Mork", "McConnell", "Orkan");
    Romulan *r1 = new Romulan("Donatra", "Jarok", "Romulan");
    Earthling *el = new Earthling("Eve", "Xu", "Earthling");
    // 将特定的 Humanoid 添加到列表
    allies.push_back(ol);
    allies.push_back(r1);
    allies.push_back(el);
    // 处理 allies 列表（它们都是 Humanoid 
    // 的特化！）
    for (auto *entity : allies) {
        entity->GetInfo();
        cout << entity->Converse() << endl;
    }
    // 虽然每个 Humanoid 类型都有默认
    // 问候，但它们可以使用另一种语言扩展技能
    el->SetSalutation("Bonjour");
    el->GetInfo();
    cout << el->Converse() << endl; // 显示 Earthling 的能力
    delete ol;
    delete r1;
    delete el;
    return 0;
}
```

上述实现方式（使用私有基类从 Adaptee 派生出 Adapter）的优点是代码非常直观。通过这种方法，Adaptee 类中的任何保护（protected）方法都可以轻松地继承，并在 Adapter 方法的作用范围内使用。我们很快就会发现，如果我们改用关联（association）作为连接 Adapter 和 Adaptee 的手段，保护成员将成为问题。

前述方法的缺点是它是 C++ 特有的实现方式。其他语言不支持私有基类。或者，使用公有基类来定义 Adapter 和 Adaptee 之间的关系将导致无法隐藏不需要的 Adaptee 接口，并且这是一个非常糟糕的设计选择。

## 考虑 Adaptee 和 Adapter 的另一种规范（关联）

让我们简要考虑一下上述适配器模式实现的一个略微修改的版本。我们将改用关联来对 Adaptee 和 Adapter 之间的关系建模。具体的派生类（目标）仍然将像以前一样派生自 Adapter。

以下是使用 Adapter 和 Adaptee 之间的关联对我们的适配器类 `Humanoid` 进行的另一种实现方式。虽然我们只审查与初始方法不同的代码部分，但完整的实现可以在我们的 GitHub 仓库中找到，作为一个完整的程序：

`://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter18/Chp18-Ex2.cpp`

```cpp
// 假设 Person 已经存在 - 然而，
// Person::ModifyTitle() 必须从 protected 移动到 public
// 或者在无法修改 Person 的情况下不被使用。
// 假设我们已经将 Person::ModifyTitle() 移动到 public。
class Humanoid
    : abstract
{
private:
    Person *life = nullptr; // 将所有请求委托给
               // 的对象
    void SetTitle(const string &t)
        { life->ModifyTitle(t); }
public:
    Humanoid() = default;
    Humanoid(const string &, const string &,
             const string &, const string &);
    Humanoid(const Humanoid &h) // 我们有拷贝工作要处理！
    Humanoid&operator=(const Humanoid &h); // 还有 op= 需要处理
    virtual~Humanoid() // 虚析构函数
        { delete life; life = nullptr; }
// 为 Adapter 类添加的接口
const string &GetSecondaryName() const
    { return life->GetFirstName(); }
const string &GetPrimaryName() const
    { return life->GetLastName(); }
const string &GetTitle() const
    { return life->GetTitle(); }
void SetSatuation(const string &m)
    { life->SetGreeting(m); }
virtual void GetInfo() const { life->Print(); }
virtual string const& verse(const&) = 0; // 抽象类
};
nHumanoid::Humanoid(const string &n2, const string &n1,
    const string &planetNation, const string &greeting)
{
    life = new Person(n2, n1, ' ', planetNation);
    life->SetGreeting(greeting);
}
// 拷贝构造函数（我们需要自己写）
Humanoid::Humanoid(const Humanoid &h);
```

```cpp
{ // 记住 life 成员变量类型是 Person
delete life; // 删除之前的关联对象
life = new Person(h.GetSecondaryName(),
    h.GetPrimaryName(), '', h.GetTitle());
    life->SetGreeting(h.life->Speak());
}
// 重载运算符=（我们需要自己写）
Humanoid&Humanoid::operator=(const Humanoid &h)
{
    if (this != &h)
        life->Person::operator=(dynamic_cast<const Person &>(h));
    return *this;
}
```

`const string &Humanoid::verse()` // 默认定义
{ // 纯虚函数 - 不寻常
    return life->Speak();
}

在我们的适配器类 `Humanoid` 的前述实现中，`Humanoid` 不再派生自 `Person`。相反，`Humanoid` 将增加一个私有数据成员 `Person *life;`，它将代表 Adapter (`Humanoid`) 和 Adaptee (`Person`) 之间的关联。在 `Humanoid` 的构造函数中，我们需要分配 Adaptee (`Person`) 的底层实现。我们还需要在析构函数中删除 Adaptee (`Person`)。

与上的实现类似，`Humanoid` 在其公共接口中提供了相同的成员函数。然而，请注意每个 `Humanoid` 方法都通过关联对象将调用委托给相应的 Adaptee 方法。例如，`Humanoid::GetSecondaryName()` 仅仅调用了 `life->GetFirstName()`；以此委托请求（而不是调用继承的相应 Adaptee 方法）。

与我们的初始实现一样，派生自 `Humanoid` 的派生类（`Orkan`、`Romulan` 和 `Earthling`）是以相同的方式指定的，我们在 `main()` 函数中的客户端也同样如此。

## 选择 Adaptee 和 Adapter 之间的关系

在选择 Adaptee 和 Adapter 之间使用私有继承还是关联时，一个值得考虑的点是 Adaptee 是否包含任何保护成员。回想一下，`Person` 的原始代码包含一个保护 `ModifyTitle()` 方法。Adaptee 类中是否应该存在保护成员？私有基类实现允许这些继承的保护成员在 Adapter 类的作用范围内（即，通过 Adapter 的方法）继续被访问。然而，使用基于关联的实现时，Adaptee（`Person`）中的保护方法在 Adapter 的作用域内是不可用的。为了让这个示例运行，我们被迫将 `Person::ModifyTitle()` 移动到公有。

## 使用适配器作为包装器

在我们之前定义的外部函数中，假设所有函数都经过了充分测试，并允许从数据库读取或写入 `Person` 实例。为了支持这种模拟，我们创建了一个带有 `Person objectRead` 的 `Person` 实例：用于为新读取的实例提供一个简短的非栈存储位置（由 `db_read()` 使用），直到新读取的实例被捕获为返回值。请记住，现有的外部函数并不代表封装的解决方案。

现在，让我们创建一个简单的包装器类来封装这些外部函数。包装器类 `CitizensDataBase` 将代表我们的适配器类：

`// CitizensDataBase 是适配器类`

```cpp
class CitizenDataBase // Adapter封装了不想要的接口
{
  private:
    string name;
  public:
    // 没有默认构造函数（异常）
    CitizenDataBase(const string& unusual);
    CitizenDataBase(const CitizenDataBase &) = delete;
    CitizenDataBase&operator=(const CitizenDataBase&) = delete; // 禁止赋值 =
    virtual ~CitizenDataBase(); // 虚析构函数
    inline Person Read(const string &);
    inline const string Write(Person &);
};
CitizenDataBase::CitizenDataBase(const string& n) : name(n)
{
    db_open(name); // 调用现有外部函数
}
CitizenDataBase::~CitizenDataBase()
{
    db_close(name); // 使用外部关闭数据库
    // 函数
}
Person &CitizenDataBase::Read(const string &key)
{
    return db_read(name, key); // 调用外部函数
}
const string CitizenDataBase::Write(Person &data)
{
    return db_write(name, data); // 调用外部函数
}
```
