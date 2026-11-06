
被称为属性。因为 C++ 不支持属性，所以我们无法真正向您展示示例代码，但思路会像这样：

```cpp
mydog.weight = 10;
cout << mydog.weight << endl;
```

尽管第一行看起来只是把 10 存入 weight 变量，但如果这是基于属性的语言，这样的代码反而会导致您的“属性设置器”方法被调用。在该方法中，您会编写代码来测试该值，并确保在存储之前它是有效值。同样，第二行看起来只是读取 weight 变量，却会间接调用获取 weight 值的方法。因此，这段代码的执行效果会像下面这段代码一样：

```cpp
mydog.SetWeight(10);
cout << mydog.GetWeight() << endl;
```

看到我们如何调用两个方法了吗——一个设置 weight，一个获取 weight？这就是属性背后的思想。它们让您编写的代码看起来是在读写成员变量，但实际上代码分别调用“获取器”和“设置器”方法。（在使用其他语言时，您可以编写这样的属性：让用户读取值、写入值，或读取和写入值，因此后台功能仍然依赖于实际上相当于两个方法：一个用于设置值，一个用于获取值。）C++ 没有属性，但许多现代语言都有。现在在学习对象时了解它们，将有助于您在最终使用支持属性的其他语言时理解属性。

## 构建层次结构

C++ 的强大能力之一是能够拿一个类并在其基础上构建新类。当您使用任何可用的 C++ 库（例如标准 C++ 库）时，可能会遇到许多彼此相关的类——有时会有几十个类。有些类派生自其他类，不过也有些类是独立的。这为程序员提供了极大的灵活性。灵活是好事。血液在您的身体系统中流动得更顺畅，您也会更放松。而在编程中，类库具有灵活性也是好事，因为当您使用灵活的库时，在要使用的不同类方面会有很多选择。

### 建立层次结构

设计类时，您可以选择让正在创建的类派生自某个原始基类——创建子/父关系。新类继承基类的能力和特征。通常，在基类中为公有的成员在派生类中仍为公有。在基类中为受保护的成员在派生类中仍为受保护；因此，如果您继续进一步派生，那些最终类也将继承这些受保护成员。然而，私有成员只存在于基类中。

![](img/6ba99460b0feb3585671a4612ff5fabb_279_0.png)

在图 1-3 中，请注意我们以 C++ 形式编写了成员变量和函数的行。通常您不会这样做；而是使用一种称为统一建模语言（UML）的特殊表示法来代替 C++，我们会在本章稍后（简要）介绍它，并在本书其余部分更详细地讨论它。

### 继承时保护成员

在 C++ 中，您可以选择如何派生类。要理解这一点，请记住：当您派生一个类时，派生类会继承基类的成员。通过不同的派生类方式，您可以指定这些继承成员在派生类中是公有、受保护还是私有。选项如下：

- **公有：** 当您以 *公有* 方式派生新类时，基类中所有公有成员在此派生类中仍为公有。
- **受保护：** 当您以 *受保护* 方式派生新类时，基类中所有公有成员现在在此新类中变为受保护。这意味着基类中原本为公有的成员将无法被此新类的使用者访问。
- **私有：** 当您以 *私有* 方式派生新类时，基类中此新类可以访问的所有成员都将变为私有。这意味着这些成员将无法被您以后从此新类派生的任何类访问——毕竟它们是私有的。

可以把它看作一种访问权限递减的顺序：最高访问权限是公有。当成员为公有时，用户可以访问该成员。中间访问权限是受保护。用户不能访问受保护成员，但派生类可以访问受保护成员。最低访问权限是私有。用户不能访问私有成员，派生类也不能。

![](img/6ba99460b0feb3585671a4612ff5fabb_279_1.png)

这里我们讨论的是继承：因此，如果我们有一个名为 FrozenFood 的基类和一个名为 FrozenPizza 的派生类，那么该派生类是 FrozenFood 中成员与额外 FrozenPizza 成员的组合。然而，只有 FrozenPizza 中属于 FrozenFood 部分的方法才能访问 FrozenFood 部分的私有成员。尽管如此，FrozenPizza 自身部分中的方法以及 FrozenFood 的私有成员都是派生类的一部分。

当您以公有方式派生类时，派生类中基类部分保持不变：原本私有的项仍留在基类部分中；因此，派生类无法访问它们。原本受保护的仍为受保护，原本公有的仍为公有。

但当您以受保护方式派生类时，基类部分与原始基类不同：其公有成员现在成为此派生类的受保护成员。（但请记住：实际基类本身并未改变。我们只讨论派生类的基类部分。）因此，那些在基类中为公有、但现在在派生类中为受保护的成员，无法被其他函数和类访问：它们现在是受保护的。

最后，如果您以私有方式派生类，基类部分又不同于原始基类：其所有成员现在都是私有的。由于其成员是私有的，您从此新派生类派生的任何类都无法访问这些成员：它们是私有的。不过，和之前一样，原始基类本身并未改变；我们仍然在讨论派生类的基类部分。

所有这些派生方式可能很复杂。请记住，当您派生类时，您是在指定继承的公有成员和受保护成员在派生类中将具有什么访问级别。

在 C++ 中，您在派生类的头行中指定所需的继承类型。请看清单 1-1 中所示的 InheritedMembers 示例。请注意清单顶部的三个类：FrozenFood、FrozenPizza 和 DeepDishPizza。FrozenFood 是 FrozenPizza 的基类，FrozenPizza 是 DeepDishPizza 的基类。图 1-4 使用称为 UML 的特殊表示法（参见上一节）展示了这一点，其中箭头指向基类。

![](img/6ba99460b0feb3585671a4612ff5fabb_280_0.png)

![](img/6ba99460b0feb3585671a4612ff5fabb_280_1.png)

### 清单 1-1：指定继承成员的访问级别

```cpp
#include <iostream>

using namespace std;

class FrozenFood
{
private:
    int Price;

protected:
    int Weight;

public:
    FrozenFood(int APrice, int AWeight);
    int GetPrice();
    int GetWeight();
};

class FrozenPizza : public FrozenFood
{
protected:
    int Diameter;

public:
    FrozenPizza(int APrice, int AWeight, int ADiameter);
    void DumpInfo();
};

class DeepDishPizza : public FrozenPizza
{
private:
    int Height;

public:
    DeepDishPizza(int APrice, int AWeight, int ADiameter, int AHeight);
    void DumpDensity();
};

FrozenFood::FrozenFood(int APrice, int AWeight)
{
    Price = APrice;
    Weight = AWeight;
}

int FrozenFood::GetPrice()
{
    return Price;
}

int FrozenFood::GetWeight()
{
    return Weight;
}

FrozenPizza::FrozenPizza(int APrice, int AWeight, int ADiameter) :
FrozenFood(APrice, AWeight)
{
    Diameter = ADiameter;
}

void FrozenPizza::DumpInfo()
{
    cout << "\tFrozen pizza info:" << endl;
    cout << "\t\tWeight: " << Weight << " ounces" << endl;
    cout << "\t\tDiameter: " << Diameter << " inches" << endl;
}

DeepDishPizza::DeepDishPizza(int APrice, int AWeight,
int ADiameter, int AHeight) :
FrozenPizza(APrice, AWeight, ADiameter)
{
    Height = AHeight;
}

void DeepDishPizza::DumpDensity()
{
    // Calculate pounds per cubic foot of deep-dish pizza
    cout << "\tDensity: ";
    cout << Weight * 12 * 12 * 12 / (Height * Diameter * 22 * 16);
    cout << " pounds per cubic foot" << endl;
}

int main(int argc, char *argv[])
{
    cout << "Thin crust pepperoni" << endl;
    FrozenPizza pepperoni(450, 12, 14);
    pepperoni.DumpInfo();
    cout << "\tPrice: " << pepperoni.GetPrice() << " cents" << endl;
}
```

