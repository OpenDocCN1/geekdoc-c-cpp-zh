
查看演示

## 现在，如果我们用参数调用 Dog 的构造函数会怎样？

```
Dog dog = new Dog("Rex");
```

你知道父类中非私有的成员会被子类继承，这意味着 Dog 也会拥有 name 字段。

在这个例子中，我们向构造函数传递了一个参数。它反过来将该参数传递给父类的带参数构造函数，由父类构造函数初始化 name 字段。

输出将是

```
Animal's constructor with 1 parameter
Rex
Dog's constructor with 1 parameter
Rex
```

## 总结：

每个对象的创建都从基类开始。在继承中，层次结构中的类被链接在一起。由于所有类都派生自 Object，因此创建任何对象时调用的第一个构造函数是 Object 类构造函数；然后调用链中的下一个构造函数，只有在所有这些构造函数都被调用之后，对象才被创建

## base 关键字

- base 关键字用于在派生类内部访问基类的成员：
- 调用基类上已被另一个方法重写的方法。指定在创建派生类实例时应调用哪个基类构造函数。

## 第 58.2 节：从基类继承

为了避免重复代码，在一个通用类中定义公共方法和属性作为基类：

```
public class Animal
{
    public string Name { get; set; }
    // Methods and attributes common to all animals
    public void Eat(Object dinner)
    {
        // ...
    }
    public void Stare()
    {
        // ...
    }
    public void Roll()
    {
        // ...
    }
}
```

既然已经有了一个表示一般 Animal 的类，你就可以定义一个描述特定动物特性的类：

```
public class Cat : Animal
{
    public Cat()
    {
        Name = "Cat";
    }
    // Methods for scratching furniture and ignoring owner
    public void Scratch(Object furniture)
    {
        // ...
    }
}
```

Cat 类不仅可以访问其定义中显式描述的方法，还可以访问一般 Animal 基类中定义的所有方法。任何 Animal（无论它是不是 Cat）都可以 Eat、Stare 或 Roll。但是，除非它也是 Cat，否则 Animal 不能 Scratch。然后你可以定义描述其他动物的其他类。（例如 Gopher 有一个破坏花园的方法，而 Sloth 完全没有额外方法。）

## 第 58.3 节：从类继承并实现接口

```
public class Animal
{
    public string Name { get; set; }
}

public interface INoiseMaker
{
    string MakeNoise();
}

//Note that in C#, the base class name must come before the interface names
public class Cat : Animal, INoiseMaker
{
    public Cat()
    {
        Name = "Cat";
    }

    public string MakeNoise()
    {
        return "Nyan";
    }
}
```

## 第 58.4 节：从类继承并实现多个接口

```
public class LivingBeing
{
    string Name { get; set; }
}

public interface IAnimal
{
    bool HasHair { get; set; }
}
```

```
public interface INoiseMaker
{
    string MakeNoise();
}

//Note that in C#, the base class name must come before the interface names
public class Cat : LivingBeing, IAnimal, INoiseMaker
{
    public Cat()
    {
        Name = "Cat";
        HasHair = true;
    }

    public bool HasHair { get; set; }

    public string Name { get; set; }

    public string MakeNoise()
    {
        return "Nyan";
    }
}
```

## 第 58.5 节：子类中的构造函数

当你创建基类的子类时，可以在子类构造函数的参数之后使用 : base 来构造基类。

```
class Instrument
{
    string type;
    bool clean;

    public Instrument (string type, bool clean)
    {
        this.type = type;
        this.clean = clean;
    }
}

class Trumpet : Instrument
{
    bool oiled;

    public Trumpet(string type, bool clean, bool oiled) : base(type, clean)
    {
        this.oiled = oiled;
    }
}
```

## 第 58.6 节：继承反模式

### 不恰当的继承

假设有 2 个类：Foo 类和 Bar 类。Foo 有两个功能 Do1 和 Do2。Bar 需要使用 Foo 中的 Do1，但它不需要 Do2，或者需要一个等同于 Do2 但做完全不同事情的功能。

坏方式：将 Foo 上的 Do2() 设为 virtual，然后在 Bar 中重写它，或者干脆在 Bar 中为 Do2() 抛出 Exception

```csharp
public class Bar : Foo
{
    public override void Do2()
    {
        //Does something completely different that you would expect Foo to do
        //or simply throws new Exception
    }
}
```

### 好方式

从 Foo 中取出 Do1() 并放入新类 Baz，然后让 Foo 和 Bar 都继承 Baz，并分别实现 Do2()

```csharp
public class Baz
{
    public void Do1()
    {
        // magic
    }
}

public class Foo : Baz
{
    public void Do2()
    {
        // foo way
    }
}

public class Bar : Baz
{
    public void Do2()
    {
        // bar way or not have Do2 at all
    }
}
```

现在说明为什么第一个示例不好而第二个示例好：当第 2 位开发者必须修改 Foo 时，他很可能会破坏 Bar 的实现，因为 Bar 现在与 Foo 不可分割。而采用后一个示例时，Foo 和 Bar 的共性已被移到 Baz，它们互不影响（本来就不应该互相影响）。

## 第 58.7 节：扩展抽象基类

与可描述为实现契约的接口不同，抽象类充当扩展契约。

抽象类不能被实例化，必须被扩展，然后生成的类（或派生类）才能被实例化。

抽象类用于提供通用实现

```csharp
public abstract class Car
{
    public void HonkHorn() {
        // Implementation of horn being honked
    }
}
```

```
public class Mustang : Car
{
    // Simply by extending the abstract class Car, the Mustang can HonkHorn()
    // If Car were an interface, the HonkHorn method would need to be included
    // in every class that implemented it.
}
```

上面的示例展示了任何扩展 Car 的类都将获得带有实现的 HonkHorn 方法。这意味着任何创建新 Car 的开发者都不需要担心它如何鸣喇叭。

## 第 58.8 节：测试和导航继承关系

```
interface BaseInterface {}
class BaseClass : BaseInterface {}

interface DerivedInterface {}
class DerivedClass : BaseClass, DerivedInterface {}

var baseInterfaceType = typeof(BaseInterface);
var derivedInterfaceType = typeof(DerivedInterface);
var baseType = typeof(BaseClass);
var derivedType = typeof(DerivedClass);

var baseInstance = new BaseClass();
var derivedInstance = new DerivedClass();

Console.WriteLine(derivedInstance is DerivedClass); //True
Console.WriteLine(derivedInstance is DerivedInterface); //True
Console.WriteLine(derivedInstance is BaseClass); //True
Console.WriteLine(derivedInstance is BaseInterface); //True
Console.WriteLine(derivedInstance is object); //True

Console.WriteLine(derivedType.BaseType.Name); //BaseClass
Console.WriteLine(baseType.BaseType.Name); //Object
Console.WriteLine(typeof(object).BaseType); //null

Console.WriteLine(baseType.IsInstanceOfType(derivedInstance)); //True
Console.WriteLine(derivedType.IsInstanceOfType(baseInstance)); //False

Console.WriteLine(
    string.Join(",",
        derivedType.GetInterfaces().Select(t => t.Name).ToArray()));
//BaseInterface,DerivedInterface

Console.WriteLine(baseInterfaceType.IsAssignableFrom(derivedType)); //True
Console.WriteLine(derivedInterfaceType.IsAssignableFrom(derivedType)); //True
Console.WriteLine(derivedInterfaceType.IsAssignableFrom(baseType)); //False
```

## 第 58.9 节：继承方法

方法有几种继承方式

```
public abstract class Car
{
    public void HonkHorn() {
        // Implementation of horn being honked
    }
}
```
