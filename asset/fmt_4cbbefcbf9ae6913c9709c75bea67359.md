
正如我们在流浪动物收容所示例中所示，我们可以使用语言提供的此功能来声明引用动物的，而不是特定的 `Dog` 类型：

```csharp
private T[] animalList;
```

假设当我们创建类对象时，设置特定类型（例如 `Dog`），在程序执行期间，未知类型 `T` 将替换为上述类型。如果我们选择为狗创建一个收容所，可以认为我们的字段声明为：

```csharp
private Dog[] animalList;
```

相应地，当我们在类的构造函数中初始化特定字段时，我们应该像往常一样创建数组，使用未知类型的替换项：

```csharp
public AnimalShelter(int placesNumber)
{
    animalList = new T[placesNumber]; // 初始化
    usedPlaces = 0;
}
```

### 在方法声明中使用未知类型

泛型类声明中使用的未知类型在类体的大括号范围内可见，因此它可以用于方法声明，即：

作为方法参数列表中的参数：

| `<return_type> MethodWithParamsOfT(T param)` |
| - 作为方法实现的结果： |
| `TWithReturnTypeOfT(<params>)` |

正如我们预料的，使用我们的示例，我们可以分别适配 `Shelter(...)` 和 `Release(...)` 方法：

- 作为未知类型参数 `T` 的方法：

```csharp
public void Shelter(T newAnimal)
{
    // 方法体在此处 ...
}
```

- 返回未知类型结果 `T` 的方法：

```csharp
public T Release(int i)
{
    // 方法体在此处 ...
}
```

正如我们所知道的，当我们从类创建对象并将未知类型替换为特定类型（例如 `Cat`）时，在程序执行期间，上述方法将具有以下形式：

`Shelter` 方法的参数将是 `Cat` 类型：

#### 第 14 章 定义类

```csharp
public void Shelter(Cat newAnimal)
{
    // 方法体在此处 ...
}
```

- 方法 `Release` 将返回类型为 `Cat` 的结果：

```csharp
public Cat Release(int i)
{
    // 方法体在此处 ...
}
```

### 类型化（泛型）—— 幕后机制

在继续之前，让我们解释一下当我们处理泛型类时，计算机内存中发生了什么。

| `MyClass<T>` | `MyClass<concrete_type>` | `MyClass<concrete_type>` 实例 |
|---|---|---|
| 泛型类描述 | 具体类型类描述 | 具体类型类实例 |

通过一个示例，我们可以创建一个 `AnimalShelter<T>` 类型的对象，它只适用于 `Dog` 类型的对象。如果我们尝试添加一个 `Cat` 对象，这将导致编译错误，该错误与尝试在“无浪动物收容所 – 示例”章节中创建的 `AnimalShelter` 类型对象中添加 `Cat` 对象时产生的错误几乎相同：

```csharp
static void Main()
{
    AnimalShelter<Dog> dogsShelter = new AnimalShelter<Dog>(10);
    Cat cat1 = new Cat();
    dogsShelter.Shelter(cat1);
}
```

如所预期，我们收到了以下编译错误信息：

`The best overloaded method match for 'AnimalShelter<Dog>.Shelter(Dog)' has some invalid arguments`

`Argument 1: cannot convert from 'Cat' to 'Dog'`

#### 泛型方法

与类一样，当方法参数的类型无法指定时，我们可以对方法进行参数化（类型化）。相应的，特定类型的指示将在方法调用时发生，将未知类型替换为特定类型，正如我们在类中中所做的那样。

方法的类型化是在方法名称之后、左括号之前添加 `<K>` 来完成的，其中 `K` 是稍后将使用的类型替换符：

```csharp
<return_type>methods_name<K>(<params>)
```

因此，我们可以在方法参数列表 `<params>` 中未使用未知类型 `K`（其类型未知），也可以用于返回值或在方法体中声明类型为替换类型 `K` 的变量。

例如，考虑一个交换两个变量值的方法：

```csharp
public void Swap<K>(ref K a, ref K b)
{
    K oldA = a;
    a = b;
    b = oldA;
}
```

这是一个交换两个变量值的方法，而不携带它们的类型。这就是为什么我们将其定义为泛型，以便我们可以将其用于所有类型的变量。

因此，如果我们想交换两个整数的值，然后是两个字符串变量，我们应该使用我们的方法：

```csharp
int num1 = 3;
int num2 = 5;
Console.WriteLine("Before swap: {0} {1}", num1, num2);
// 使用具体类型 (int) 调用方法
Swap<int>(ref num1, ref num2);
Console.WriteLine("After swap: {0} {1}\n", num1, num2);
string str1 = "Hello";
string str2 = "There";
Console.WriteLine("Before swap: {0} {1!", str1, str2);
// 使用具体类型 (string) 调用方法
Swap<string>(ref str1, ref str2);
Console.WriteLine("After swap: {0} {1}!", str1, str2);
```

当你运行此代码时，结果如预期所示：

```
Before swap: 3 5
After swap: 5 3
Before swap: Hello There!
After swap: There Hello!
```

我们注意到在参数列表中我们也使用了 `ref` 关键字。这涉及到方法的规范——即交换两个引用的值。通过使用 `ref` 关键字，该方法将使用由调用方法提供的相同引用。这样，我们的方法对该变量进行的所有更改在方法退出后都将保留。

我们知道，通过调用泛型方法，我们可以省略特定类型的声明（在我们的示例中为 `<int>`），因为编译器会自动检测它，通过识别给定的参数的类型来实现。换句话说，可以使用以下调用来简化我们的代码：

```csharp
Swap(ref num1, ref num2); // 调用方法 Swap<int>
Swap(ref str1, ref str2); // 调用方法 Swap<string>
```

我们知道，只有当类型在参数列表中时，编译器才能识别出什么是特定类型。编译器无法通过返回值或在没有参数的情况下识别泛型方法的特定类型。在两种情况下，都必须显式给出此特定类型。在我们的示例中，将类似于原始方法调用，或者通过添加 `<int>` 或 `<string>`。

应该注意的是，静态方法也可以类型化，与类的属性和构造函数不同。

> 静态方法也可以类型化，但类的属性和构造函数不能类型化。

### 在泛型类中声明泛型方法的特性

正如我们在“在方法声明中使用未知类型”部分所看到的，非泛型方法可以使用泛型类声明中描述的未知类型（例如“无浪动物收容所”示例中的 `Shelter()` 和 `Release()` 方法）：

#### AnimalShelter.cs

```csharp
public class AnimalShelter<T>
{
    // ... 代码的其余 ...
    public void Shelter(T newAnimal)
    {
        // 方法体在此处
    }
    public T Release(int i)
    {
        // 方法体在此处
    }
}
```

如果我们尝试重用标记泛型类未知类型的变量（例如作为 `T`）在泛型方法的声明中，那么当我们尝试编译该类时，我们将得到警告 `CS0693`。发生这种情况是因为是因为在方法声明中定义的未知类型 `T` 的作用范围与类声明中未知类型 `T` 的作用范围重叠了：

#### CommonOperations.cs

```csharp
public class CommonOperations<T>
{
    // CS0693
    public void Swap<T>(ref T a, ref T b)
    {
        T oldA = a;
        a = b;
        b = oldA;
    }
}
```

当你尝试编译此类时，你会收到以下消息：

`Type parameter 'T' has the same name as the type parameter from outer type 'CommonOperations<T>'`

如果我们希望我们的代码是灵活的，并且我们的泛型方法能够安全地通过特定类型调用，我们只需要将泛型方法声明中的未知类型替换为与类不同的类型，如下所示：

#### CommonOperations.cs

```csharp
public class CommonOperations<T>
{
    // 无警告
    public void Swap<K>(ref K a, ref K b)
    {
        K oldA = a;
        a = b;
        b = oldA;
    }
}
```

因此，始终确保方法和类的未知类型替换不会发生重叠。

### 在泛型源码中使用 "default" 关键字

一旦我们引入了泛类型的基础知识，让我们重新设计本节中的第一个示例（无浪动物收容所）。我们只需要将类型 `Dog` 替换为参数 `T`：

#### AnimalShelter.cs

```csharp
public class AnimalShelter<T>
{
    private const int DefaultPlacesCount = 20;
    private T[] animalList;
    private int usedPlaces;
    public AnimalShelter() : this(DefaultPlacesCount)
    {
    }
    public AnimalShelter(int placesCount)
    {
        this.animalList = new T[placesCount];
        this.usedPlaces = 0;
    }
    public void Shelter(T newAnimal)
    {
        if (this.usedPlaces >= this.animalList.Length)
        {
            throw new InvalidOperationException("收容所已满.");
        }
        this.animalList[this.usedPlaces] = newAnimal;
        this.usedPlaces++;
    }
    public T Release(int index)
    {
        if (index < 0 || index >= this.usedPlaces)
        {
            throw new ArgumentOutOfRangeException("无效索引: " + index);
        }
        T releasedAnimal = this.animalList[index];
        for (int i = index; i < this.usedPlaces - 1; i++)
        {
            this.animalList[i] = this.animalList[i + 1];
        }
        this.animalList[this.usedPlaces - 1] = null;
        this.usedPlaces--;
        return releasedAnimal;
    }
}
```

一切看起来运行正常，直到我们尝试编译该类。这时，我们收到了以下错误：

#### 第 14 章. 定义类

无法将 `null` 转换为类型参数 `'T'`，因为它可能是一个不可空类型。请考虑使用 `default(T)` 代替。

错误位于 `Release()` 方法内部，它与在避难所（shelter）最后一个释放（最右侧）单元格中记录空值有关。我们正尝试使用引用类型的默认值，但不确定它是引用类型还是原始值类型。因此，编译器显示了上述错误。如果 `AnimalShelter` 是由结构体而非类实例化的，那么空值是无效的。

为了处理这个问题，在我们的代码中，必须使用 `default(T)` 代替 `null`，它会返回特定类型的默认值，并替代 `T`。正如我们所知，引用类型的默认值为 `null`，数值类型为零。我们可以进行以下操作：

```cs
// this.animalList[this.usedPlaces - 1] = null;
this.animalList[this.usedPlaces - 1] = default(T);
```

最后，编译顺利运行，`AnimalShelter<T>` 类运行正常。我们可以按照如下进行测试：

```cs
static void Main() {
AnimalShelter<Dog> shelter = new AnimalShelter<Dog>();
shelter.Shelter(new Dog());
shelter.Shelter(new Dog());
shelter.Shelter(new Dog());
Dog d = shelter.Release(1); // 释放第二只狗
Console.WriteLine(d);
d = shelter.Release(0); // 释放第一只狗
Console.WriteLine(d);
d = shelter.Release(0); // 释放第三只狗
Console.WriteLine(d);
d = shelter.Release(0); // 异常：无效的单元索引
}
```

### 泛型的优缺点

与其他非泛型替代方案相比，泛型类和方法增加了代码的重用性、安全性和性能。

作为一个一般原则，只要有可能，程序员都应该努力创建和使用泛型类。使用的泛型类型越多，程序的抽象层次就越高，源代码变得越灵活且越可重用。然而，我们应该记住，过度使用泛型可能会导致过度泛化，代码可能会变得难以访问且难以其他程序员理解。

### 泛型类型参数的命名

在结束泛型这个主题之前，让我们就如何在泛型类中处理未知类型的替代符（参数）为您提供一些指导：

- 如果泛型中只有一个未知类型，通常使用字母 `T` 作为未知类型的替代符。例如，我们可以将类声明为 `AnimalShelter<T>`，这是我们到目前为止一直在使用的写法。
- 替代符应该赋予最具描述性的名称，除非字母不是一个足够描述性且选择良好的名称，否则这不会提高源代码的可读性。例如，我们可以修改我们的代码，将字母 `T` 替换为更具描述性的替代符 `Animal`：

```cs
public class AnimalShelter<Animal>
{
    // 代码的其他部分 ...
    public void Shelter(Animal newAnimal)
    {
        // 方法体在此
    }
    public Animal Release(int i)
    {
        // 方法体在此
    }
}
```
