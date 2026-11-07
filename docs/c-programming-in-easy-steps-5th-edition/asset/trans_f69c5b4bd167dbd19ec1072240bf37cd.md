

## 重载方法

正如 C++ 允许函数重载一样，类方法也可以重载——包括构造函数方法。重载的构造函数方法很有用，可以在创建对象时未向构造函数传递值的情况下，为成员变量分配默认值。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_123_0.png)

overloaded.cpp

- 1. 将上一个示例“constructor.cpp”的副本重命名为新程序“overloaded.cpp”。

- 2. 在 Dog 类声明的 public 部分中，内联添加一个重载的 bark 方法——在调用时输出传入的字符串参数。

```cpp
void bark(string noise) { cout << noise << endl; }
```

- 3. 现在，声明一个不接受参数的构造函数方法原型（默认构造函数方法），以及一个接受两个参数的重载构造函数方法原型。

```cpp
Dog();
Dog(int, int);
```

- 4. 在 Dog 类声明之后，添加默认构造函数方法的定义——在创建对象时未传递任何参数的情况下，为类变量分配默认值。

```cpp
Dog::Dog()
{
    age = 1;
    weight = 2;
    color = "black";
}
```

- 5. 现在，添加重载构造函数方法的定义——在创建对象时传递两个参数的情况下，为类变量分配默认值。

```cpp
Dog::Dog(int age, int weight)
{
    this->age = age;
    this->weight = weight;
    color = "white";
}
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_123_1.png)

当参数与成员同名时，`this->` 指针用于显式标识类成员。

- 6. 在 main 方法中，插入一条语句以创建不传递任何参数的 Dog 对象——调用默认构造函数。

```cpp
Dog rex;
```

- 7. 添加语句，调用每个 getter 方法以获取由默认构造函数方法设置的默认值。

```cpp
cout << "Rex is a " << rex.getAge();
cout << " year old " << rex.getColor();
cout << " dog who weighs " << rex.getWeight();
cout << " pounds.";
```

- 8. 现在，添加对重载输出方法的调用。

```cpp
rex.bark("GRRR!");
```

- 9. 插入一条语句，创建传递两个参数的 Dog 对象——以调用重载构造函数。

```cpp
Dog sammy(2, 6);
```

- 10. 添加语句以获取由重载构造函数方法设置的值，并调用重载输出方法。

```cpp
cout << "Sammy is a " << sammy.getAge();
cout << " year old " << sammy.getColor();
cout << " dog who weighs " << sammy.getWeight();
cout << " pounds.";
sammy.bark("BOWWOW!");
```

- 11. 保存、编译并运行程序。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_124_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_124_1.png)

在不传递参数创建对象时，不要在对象名后添加括号——注意是 **Dog rex**；而不是 **Dog rex()**。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_124_2.png)

这是 Dog 类的最终版本。在继续之前，请确保你能轻松识别它的公有和私有成员。

## 继承类属性

C++ 类可以像前面示例中那样作为全新类创建，也可以从现有类“派生”而来。重要的是，派生类除了拥有自己的成员外，还继承其派生自的父类（基类）的成员。

从基类继承成员的能力允许创建共享某些公共属性的派生类，这些属性已在基类中定义。例如，“Polygon”基类可以定义所有多边形共有的 width 和 height 属性。“Rectangle”和“Triangle”类可以从 Polygon 类派生——除了定义它们各自独有特性的自身成员之外。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_125_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_125_1.png)

继承的优点极其强大，并且是面向对象编程（OOP）的第二项原则。

派生类声明在其类名后添加一个冒号 `:`，后跟访问说明符以及它派生自的类。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_125_2.png)

derived.cpp

- 1. 通过指定要包含的 C++ 库类和要使用的命名空间前缀来开始一个新程序。

```cpp
#include <iostream>
using namespace std;
```

- 2. 声明一个名为“Polygon”的类，其中包含两个 protected 变量（仅可由此类的成员及派生自该类的类访问），以及一个用于为这些变量赋值的 public 方法。

```cpp
class Polygon
{
    protected:
        int width, height;
    public:
        void setValues(int w, int h) { width = w; height = h; }
};
```

- 3. 在 Polygon 类之后，声明一个派生自 Polygon 类并添加一个独有方法的 Rectangle 类。

```cpp
class Rectangle : public Polygon
{
    public:
        int area() { return (width * height); }
};
```

- 4. 在 Rectangle 类之后，声明一个派生自 Polygon 类并添加一个独有方法的 Triangle 类。

```cpp
class Triangle : public Polygon
{
public:
    int area() { return ((width * height) / 2); }
};
```

- 5. 在 Triangle 类之后，添加一个 main 方法，其中包含最后的 `return` 语句，并创建每个派生类的实例。

```cpp
int main()
{
    Rectangle rect; Triangle trgl;
    return 0;
}
```

- 6. 插入对从 Polygon 基类继承的方法的调用——以初始化继承的变量。

```cpp
rect.setValues(4, 5);
trgl.setValues(4, 5);
```

- 7. 输出每个派生类的独有方法返回的值。

```cpp
cout << "Rectangle area : " << rect.area() << endl;
cout << "Triangle area : " << trgl.area() << endl;
```

- 8. 保存、编译并运行程序以查看输出。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_126_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_126_1.png)

不要混淆类实例和派生类——实例是类的一个副本，而派生类是一个新类，它继承其派生自的基类的属性。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_126_2.png)

一个类声明可以从多个类派生。例如，**class Box : public A, public B, public C { };** 

## 调用基类构造函数

尽管派生类继承其父基类的成员，但它们不继承其构造函数和析构函数。然而，应当注意，当创建派生类的新对象时，总是会调用基类的默认构造函数——而当对象被销毁时，会调用基类析构函数。这些调用是在对派生类的构造函数和析构函数方法的调用之外额外进行的。

基类的默认构造函数没有参数——但该类也可能有带参数的重载构造函数。如果你希望在创建派生类的新对象时调用基类的重载构造函数，可以在派生类中创建一个匹配的重载构造函数——具有相同数量和类型的参数。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_127_0.png)

- 1. 通过指定要包含的 C++ 库类和要使用的命名空间前缀来开始一个新程序。

```cpp
#include <iostream>
using namespace std;
```

- 2. 声明一个名为“Parent”的类，它将作为基类。

```cpp
class Parent
{
    // Class members go here.
};
```

- 3. 在 Parent 类声明的大括号之间，插入一个 public 访问说明符，并添加一个默认构造函数以输出文本——标识它何时被调用。

```cpp
public:
    Parent()
    { cout << "Default Parent constructor called."; }
```

- 4. 添加一个重载构造函数，它接受单个整数参数，并且也输出标识文本。

```cpp
Parent(int a)
{ cout << endl <<
    "Overloaded Parent constructor called."; }
```

- 5. 在 Parent 类之后，声明一个派生的“Daughter”类。

```cpp
class Daughter : public Parent
{

};
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_127_1.png)

- 6. 在 Daughter 类声明中，插入一个 public 访问说明符，并添加一个默认构造函数以输出文本——标识它何时被调用。

```cpp
public:
    Daughter()
    { cout << endl <<
        "Derived Daughter class default constructor called."; }
```

- 7. 在 Daughter 类之后，声明一个派生的“Son”类。

