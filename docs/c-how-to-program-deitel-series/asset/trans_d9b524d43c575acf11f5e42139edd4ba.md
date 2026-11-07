

## 12 面向对象编程：多态

![](img/b42ba5cd262b1358d16610173f975e4d_552_0.png)

> 纯真无邪的沉默，
> 在言语失效时更具说服力。
>
> ——威廉·莎士比亚

> 一般性的命题
> 不能决定具体案件。
>
> ——奥利弗·温德尔·霍姆斯

> 一位杰出的哲学家
> 不会在真空中思考。
> 即使是他最抽象的思想，
> 在某种程度上也受限于
> 他所生活的时代里
> 已知或未知的事物。
>
> ——阿尔弗雷德·诺思·怀特海

### 目标

在本章中，你将学习：

- 多态如何使编程更方便、系统更具扩展性。
- 抽象类与具体类的区别，以及如何创建抽象类。
- 使用运行时类型信息（RTTI）。
- C++ 如何实现虚函数和动态绑定。
- 虚析构函数如何确保对象上所有适当的析构函数得以运行。

### 12.2 多态简介：多态视频游戏

假设我们设计一个视频游戏，其操作许多*不同类型*的对象，包括类 Martian、Venutian、Plutonian、SpaceShip 和 LaserBeam 的对象。想象这些类都继承自公共基类 SpaceObject，该基类包含成员函数 draw。每个派生类以适合该类的方式实现此函数。屏幕管理器程序维护一个容器（例如 vector），其中保存指向各个类对象的 *SpaceObject 指针*。为了刷新屏幕，屏幕管理器定期向每个对象发送相同的消息——即 draw。每种类型的对象以独特的方式做出响应。例如，Martian 对象可能会用红色绘制自身并带有适当数量的天线，SpaceShip 对象可能会绘制成一个银色飞碟，而 LaserBeam 对象可能会绘制成一道穿过屏幕的亮红色光束。*同一消息*（此处为 draw）发送给*各种*对象会呈现*多种形式*的结果——因此得名多态。

多态屏幕管理器有助于以对代码的最小修改将新类添加到系统中。假设我们想向视频游戏添加 Mercurian 类的对象。为此，我们必须构建一个继承自 SpaceObject 的类 Mercurian，但提供它自己的成员函数 draw 定义。然后，当指向 Mercurian 类对象的*指针*出现在容器中时，您无需修改屏幕管理器的代码。屏幕管理器对容器中的*每个*对象调用成员函数 draw，*无论*对象的类型如何，因此新的 Mercurian 对象就可以“直接插入”。这样，无需修改系统（除了构建并包含类本身之外），您就可以使用多态来容纳其他类，包括系统创建时*甚至未曾设想*的类。

> **软件工程观察 12.1**
>
> *多态使您能够进行一般性处理，并让运行时环境关注具体细节。您可以让各种对象以适合这些对象的方式行为，甚至无需知道它们的类型——只要这些对象属于同一个继承层次结构，并通过公共基类指针或公共基类引用进行访问。*

> **软件工程观察 12.2**
>
> *多态促进可扩展性。编写用于调用多态行为的软件时，与消息所发送到的对象的具体类型无关。因此，能够响应现有消息的新类型对象可以被合并到这样的系统中，而无需修改基础系统。只有实例化新对象的客户端代码必须修改以适应新类型。*

### 12.3 继承层次结构中对象之间的关系

第 11.3 节创建了一个员工类层次结构，其中类 BasePlusCommissionEmployee 继承自类 CommissionEmployee。第 11 章的示例通过使用

#### *创建对象并显示其内容*

在图 12.1 中，第 13–14 行创建了一个 CommissionEmployee 对象，第 17 行创建了一个指向 CommissionEmployee 对象的指针；第 20–21 行创建了一个 BasePlusCommissionEmployee 对象，第 24 行创建了一个指向 BasePlusCommissionEmployee 对象的指针。第 31 和 33 行使用每个对象的名称调用其 print 成员函数。

#### *将基类指针指向基类对象*

第 36 行将基类对象 commissionEmployee 的地址赋给基类指针 commissionEmployeePtr，第 39 行使用该指针在 commissionEmployee 对象上调用成员函数 print。这将调用基类 CommissionEmployee 中定义的 print 版本。

#### *将派生类指针指向派生类对象*

类似地，第 42 行将派生类对象 basePlusCommissionEmployee 的地址赋给派生类指针 basePlusCommissionEmployeePtr，第 46 行使用该指针在 BasePlusCommissionEmployee 对象上调用成员函数 print。这将调用派生类 BasePlusCommissionEmployee 中定义的 print 版本。

#### *将基类指针指向派生类对象*

然后第 49 行将派生类对象 basePlusCommissionEmployee 的地址赋给基类指针 commissionEmployeePtr，第 53 行使用该指针调用成员函数 print。这种“交叉”是允许的，因为派生类的对象也是其基类的对象。尽管基类 CommissionEmployee 指针指向派生类 BasePlusCommissionEmployee 对象，但调用的是基类 CommissionEmployee 的 print 成员函数（而不是 BasePlusCommissionEmployee 的 print 函数）。该程序中每次 print 成员函数调用的输出表明，所调用的功能取决于用于调用函数的指针（或引用）的类型，而不是成员函数被调用的对象的类型。在第 12.3.4 节中，当我们介绍虚函数时，我们将证明可以调用对象类型的功能，而不是调用句柄类型的功能。我们将看到这对于实现多态行为至关重要——这是本章的关键主题。

#### 12.3.2 将派生类指针指向基类对象

在 12.3.1 节中，我们将派生类对象的地址赋给基类指针，并解释了 C++ 编译器允许这种赋值，因为派生类对象也是基类对象。我们在图 12.2 中采取相反的做法，将派生类指针指向基类对象。[注意：该程序复用了第 11.3.5 节中类 CommissionEmployee 和 BasePlusCommissionEmployee 的最终版本。] 图 12.2 的第 8–9 行创建了一个 CommissionEmployee 对象，第 10 行创建了一个 BasePlusCommissionEmployee 指针。第 14 行试图将基类对象 commissionEmployee 的地址赋给派生类指针 basePlusCommissionEmployeePtr，但编译器产生错误。编译器阻止这种赋值，因为 CommissionEmployee 不是 BasePlusCommissionEmployee。

考虑如果编译器允许这种赋值会有什么后果。通过 BasePlusCommissionEmployee 指针，我们可以为指针所指向的对象（即基类对象 commissionEmployee）调用每一个 BasePlusCommissionEmployee 成员函数，包括 setBaseSalary。然而，CommissionEm-

```cpp
virtual void draw() const;
```

将出现在基类 Shape 中。上述原型声明了函数 draw 是一个虚函数，它不带参数且不返回任何内容。该函数被声明为 const，因为 draw 函数通常不会修改被调用的 Shape 对象——虚函数不一定是 const 函数。

![](img/b42ba5cd262b1358d16610173f975e4d_562_0.png)

> **软件工程观察 12.5**
>
> *一旦一个函数被声明为 virtual，它从该点起在继承层次结构中一直保持为 virtual，即使派生类覆盖该函数时没有显式声明为 virtual。*

![](img/b42ba5cd262b1358d16610173f975e4d_562_1.png)

> **良好编程实践 12.1**
>
> *即使某些函数由于在类层次结构中较高位置声明而隐式地为 virtual，也应在类层次结构的每一层显式地将这些函数声明为 virtual，以提升程序清晰度。*

![](img/b42ba5cd262b1358d16610173f975e4d_562_2.png)

> **软件工程观察 12.6**
>
> *当派生类选择不覆盖基类中的虚函数时，派生类继承其基类的虚函数实现。*

#### *通过基类指针或引用调用虚函数*

如果程序通过指向派生类对象的基类指针（例如 shapePtr->draw()）或派生类对象的基类引用（例如 shapeRef.draw()）调用虚函数，程序将根据对象类型（而不是指针或引用类型）在运行时动态地选择正确的派生类 draw 函数。在运行时（而不是编译时）选择要调用的适当函数称为动态绑定或后期绑定。

#### *通过对象名称调用虚函数*

当通过名称引用特定对象并使用点成员选择运算符（例如 squareObject.draw()）调用虚函数时，函数调用在编译时解析（这称为静态绑定），所调用的虚函数是该特定对象的类所定义（或继承）的版本——这不是多态行为。因此，使用虚函数的动态绑定仅发生在指针（以及我们很快将看到的引用）上。

#### *CommissionEmployee 层次结构中的虚函数*

现在让我们看看虚函数如何在我们的员工层次结构中实现多态行为。图 12.4–12.5 分别是类 CommissionEmployee 和 BasePlusCommissionEmployee 的头文件。我们修改了这些头文件，将每个类的 earnings 和 print 成员函数声明为 virtual（图 12.4 的第 29–30 行和图 12.5 的第 19–20 行）。由于函数 earnings 和 print 在类 CommissionEmployee 中是虚函数，因此类 BasePlusCommissionEmployee 的 earnings 和 print 函数覆盖了类 CommissionEmployee 的函数。此外，类 BasePlusCommissionEmployee 的 earnings 和 print 函数被声明为 override。

