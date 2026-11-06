
受保护的。用户不能访问受保护的成员，但派生类可以访问受保护成员。访问级别最低的是 private。用户不能访问私有成员，派生类也不能。

![](img/128ab511de4e7360e167e3b15cdd5dd0_344_0.png)

为了正确理解继承过程中的保护机制，可以考虑 FrozenFood 类及其子类。使用 FrozenPizza 派生类时，你会看到 FrozenFood 中的成员与额外的 FrozenPizza 成员的组合。然而，只有 FrozenPizza 中属于 FrozenFood 部分的方法才能访问 FrozenFood 部分的私有成员。尽管如此，FrozenPizza 中属于 FrozenFood 部分的方法以及 FrozenFood 的私有成员都是派生类的一部分。

以公有方式派生一个类时，派生类的基类部分保持不变：那些原本私有的项仍留在基类部分中；因此，派生类不能访问它们。原本受保护的项仍然受保护，原本公有的项仍然公有。

但是，以受保护方式派生一个类时，基类部分与原来的基类不同：它的公有成员现在成为这个派生类的受保护成员。实际基类本身并没有改变；只是派生类的基类部分变为受保护。因此，基类中原本为公有、现在在派生类中为受保护的成员，不能被其他方法和类访问。

最后，如果以私有方式派生一个类，基类部分同样与原来的基类不同：它的所有成员现在都是私有的。由于这些成员是私有的，你从这个新派生类继续派生的任何类都不能访问这些成员：它们是私有的。不过，和之前一样，原始基类本身并没有改变。

在 C++ 中，要在派生类的类头中指定所需的继承类型。请看代码清单 3-2 中展示的 InheritedMembers 示例。注意清单顶部的三个类：FrozenFood、FrozenPizza 和 DeepDishPizza。FrozenFood 是 FrozenPizza 的基类，而 FrozenPizza 是 DeepDishPizza 的基类。图 3-4 用箭头指向基类来表示这种关系。

![](img/128ab511de4e7360e167e3b15cdd5dd0_345_0.png)

**图 3-4：** 此 UML 图中的箭头指向基类。

## 代码清单 3-2：指定继承成员的访问级别

```cpp
#include <iostream>

using namespace std;

class FrozenFood {
private:
    int Price;
protected:
    int Weight;
public:
    FrozenFood(int APrice, int AWeight);
    int GetPrice();
    int GetWeight();
};

class FrozenPizza : public FrozenFood {
protected:
    int Diameter;
public:
    FrozenPizza(int APrice, int AWeight, int ADiameter);
    void DumpInfo();
};

class DeepDishPizza : public FrozenPizza {
private:
    int Height;
public:
    DeepDishPizza(int APrice, int AWeight, int ADiameter,
                  int AHeight);
    void DumpDensity();
};

FrozenFood::FrozenFood(int APrice, int AWeight) {
    Price = APrice;
    Weight = AWeight;
}

int FrozenFood::GetPrice() {
    return Price;
}

int FrozenFood::GetWeight() {
    return Weight;
}

FrozenPizza::FrozenPizza(int APrice, int AWeight,
                         int ADiameter) :
                         FrozenFood(APrice, AWeight) {
    Diameter = ADiameter;
}

void FrozenPizza::DumpInfo() {
    cout << "\tFrozen pizza info:" << endl;
    cout << "\t\tWeight: " << Weight << " ounces" << endl;
    cout << "\t\tDiameter: " << Diameter << " inches"
         << endl;
}

DeepDishPizza::DeepDishPizza(int APrice, int AWeight,
                             int ADiameter, int AHeight) :
                             FrozenPizza(APrice, AWeight,
                                         ADiameter) {
    Height = AHeight;
}

void DeepDishPizza::DumpDensity() {
    // Calculate pounds per cubic foot of deep-dish pizza
    cout << "\tDensity: ";
    cout << Weight * 12 * 12 * 12 * 14 /
         (Height * Diameter * 22 * 16);
    cout << " pounds per cubic foot" << endl;
}
```

## 代码清单 3-2：（续）

```cpp
int main() {
    cout << "Thin crust pepperoni" << endl;
    FrozenPizza pepperoni(450, 12, 14);
    pepperoni.DumpInfo();
    cout << "\tPrice: " << pepperoni.GetPrice()
         << " cents" << endl;

    cout << "Deep dish extra-cheese" << endl;
    DeepDishPizza extracheese(650, 21592, 14, 3);
    extracheese.DumpInfo();
    extracheese.DumpDensity();
    cout << "\tPrice: " << extracheese.GetPrice()
         << " cents" << endl;
    return 0;
}
```

运行代码清单 3-2 时，会看到以下输出：

```text
Thin crust pepperoni
              Frozen pizza info:
                    Weight: 12 ounces
                  Diameter: 14 inches
             Price: 450 cents
Deep dish extra-cheese
              Frozen pizza info:
                    Weight: 21592 ounces
                  Diameter: 14 inches
                 Density: 35332 pounds per cubic foot
             Price: 650 cents
```

前五行显示的是 FrozenPizza 类对象的信息。其余行显示的是 DeepDishPizza 类对象的信息，包括它重 21,592 盎司（恰好是 1349.5 磅）这一事实。它的密度为 35,332 磅/立方英尺。

这些派生都是公有的。因此，在 FrozenFood 中为公有的项，在 FrozenPizza 和 DeepDishPizza 中仍然为公有。请注意输出中不同信息的来源。Frozen pizza info: 这一行以及随后的两行（Weight: 和 Diameter:）来自公有方法 DumpInfo()，它是 FrozenPizza 的成员。DumpInfo() 在 FrozenPizza 类中是公有的。由于 DeepDishPizza 以公有方式从 FrozenPizza 派生，因此 DumpInfo() 也是 DeepDishPizza 的公有成员。

尝试将 `DeepDishPizza` 的类头从

```cpp
class DeepDishPizza : public FrozenPizza
```

改为

```cpp
class DeepDishPizza : protected FrozenPizza
```

你要把 `public` 一词改为 `protected`。请确保修改的是正确的行。编译并运行应用程序。你会看到类似下面的错误：

```text
In function 'int main()':
error: 'void FrozenPizza::DumpInfo()' is inaccessible
error: within this context
error: 'FrozenPizza' is not an accessible base of
  'DeepDishPizza'
error: 'int FrozenFood::GetPrice()' is inaccessible
error: within this context
error: 'FrozenFood' is not an accessible base of 'DeepDishPizza'
```

这条消息指的是 `main()` 中的 `extracheese.DumpInfo();` 行。由于类头中的 `protected` 一词，`DumpInfo()` 现在是 `DeepDishPizza` 的受保护成员。通过在类定义中写入 `protected` 一词，你表示当前为公有的继承成员将改为受保护。由于 `DumpInfo()` 成员是受保护的，因此不能从 `main()` 中调用它。不过，`DumpInfo()` 在 `FrozenPizza` 类中仍然是公有的，所以下面这个调用没有问题：

```cpp
pepperoni.DumpInfo();
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_348_0.png)

请注意，你可以双击 `error: within this context` 行，直接跳转到试图访问隐藏成员的代码，而不必查看最初的错误。使用这种技巧可以节省查找出错代码的时间。

将该行改回公有继承，就像代码清单 3-2 中那样：`class DeepDishPizza : public FrozenPizza`。

现在将 `FrozenPizza` 的类头改成这样：

```cpp
class FrozenPizza : private FrozenFood
```

同样，请确保修改正确的行。编译并运行应用程序，会看到以下错误：

```text
In function 'int main()':
error: 'void FrozenPizza::DumpInfo()' is inaccessible
error: within this context
error: 'FrozenPizza' is not an accessible base of
    'DeepDishPizza'
error: 'int FrozenFood::GetPrice()' is inaccessible
error: within this context
error: 'FrozenFood' is not an accessible base of 'DeepDishPizza'
```

这个错误指的是 DeepDishPizza::DumpDensity() 中的一行，其中代码试图访问 Weight 成员。编译器现在不允许访问，因为该成员原本在 FrozenFood 类中是公有的，当它成为 FrozenPizza 的一部分时变成了私有。又因为它在 FrozenPizza 中是私有的，派生类 DeepDishPizza 不能在自己的方法中访问它。请确保将 FrozenPizza 的类头改回这样：`class FrozenPizza : public FrozenFood`。

## 重写方法

类的一个很酷的特性是，你可以在一个类中声明一个方法，然后在派生新类时，为该类提供同一方法的不同版本。这称为重写方法。例如，如果你有一个 FrozenFood 类和一个派生类 FrozenPizza，你可能希望在 FrozenFood 中包含一个名为 BakeChemistry() 的方法，该方法在食物被烘焙时改变食物。由于所有食物都不同，对于从 FrozenFood 派生的每个类，BakeChemistry() 方法都会有所不同。

在 C++ 中，可以通过在基类声明中于方法名之前添加 virtual 一词，为不同的派生类提供该方法的不同版本，如下行代码所示：

```cpp
virtual void BakeChemistry();
```

这一行是类定义内部的原型。稍后，你会提供该方法的代码。在派生类的类中，你只需放入方法原型，不写 virtual 一词：

```cpp
void BakeChemistry();
```
