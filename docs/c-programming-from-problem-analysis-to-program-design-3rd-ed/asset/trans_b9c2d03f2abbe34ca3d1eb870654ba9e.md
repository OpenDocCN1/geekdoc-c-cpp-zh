
![](img/e33ae760e23d89eac66541252ad65de8_221_0.png)

**图 4-3** 由 Student 类图自动生成的代码

在 Visual Studio 中使用类图工具，还能获得以图形方式查看类的额外好处。你可以像前一个应用程序那样，仅使用代码编辑器来定义该类的类模板。但是，如果使用类图工具，还可以在类图和代码窗口之间来回切换。二者各有一个单独的选项卡。你会注意到，在图 4-2 中，保存类图的文件具有 .cd 扩展名。

图 4-3 说明了字段或数据成员（实例变量）的声明位置。如示例 4-1 和 4-2 所示，数据字段通常首先在**类**定义的主体内部声明。在接下来的示例中，将使用面向对象的方法重新审视第 3 章中的 CarpetCalculator。

### 示例 4-2

```
public class CarpetCalculator
{
    private double pricePerSqYard;
    private double noOfSqYards;
    :   // The : indicates other lines follow.
```

## 编写自己的实例方法

定义类的方法时，你就是在编写实例方法。实例方法不在其方法头中使用 static 关键字。但是，要调用实例方法，必须先实例化一个对象，并将该对象与方法关联起来。有几种特殊类型的方法。接下来的各节将对此进行描述。

### 构造函数

构造函数是用于创建对象的特殊类型方法。应用程序的面向对象设计有助于代码复用。定义类之后，你要创建该类的实例（或称示例）。这称为实例化该类。类的实例称为对象。实例化类时，你实际上创建了该类的一个实例，即一个占用空间并存在的对象。正是通过这种称为构造函数的特殊方法，你才能创建类的实例。构造函数与其他方法有两点不同：

- 构造函数不返回值，但不包含关键字 void。如果在构造函数的方法头中键入 void，就会收到错误消息。
- 构造函数使用与类名相同的标识符（名称）。
- 构造函数也是方法。与其他方法一样，它们可以被重载。

构造函数总是带有 public 访问修饰符，以便其他类可以实例化其类型的对象。编写类时，如果没有显式定义构造函数，系统会自动为你创建一个构造函数。这个构造函数称为默认构造函数。除了可用于创建类的实例之外，它没有任何功能。如果使用默认构造函数创建该类的对象，则会为每个成员数据字段分配默认值。默认构造函数不包含参数。它没有方法体，只有一对花括号。对于名为 Student 的类，默认构造函数如下所示：

```
public Student ( )
{
}
```

构造函数用于为对象的数据成员提供初始值。这些初始值可以作为参数发送给构造函数方法，也可以在构造函数的方法体中硬编码。为了让类具备完整功能，通常要为所有将实例化对象的类编写多个构造函数。只要为类显式编写了一个构造函数，就会失去自动创建的默认构造函数。编写构造函数时，请考虑将如何创建该类的对象。如果有一个 Student 类，你可能希望有一个构造函数，可以在给定 studentNumber 时创建 Student 对象。你可能还希望有另一个构造函数，可以在给定 studentNumber 和 name 时创建 Student 对象。如果你拥有所有数据（studentNumber、name、score1、score2、score3 和 major），那么另一个构造函数可能很有用。因此，对于 Student 类，可能至少需要设计四个构造函数，如示例 4-3 所示。

### 示例 4-3

```
//Default constructor
public Student ( )
{
}

//Constructor with one parameter
public Student (int sID )
{
    studentNumber = sID;
}

//Constructor with two parameters
public Student (int sID, string name)
{
    studentNumber = sID;
    studentName = name;
}

//Constructor with all data members
public Student (int sID, string name, int s1, int s2, int s3,
    string maj)
{
    studentNumber = sID;
    studentName = name;
    score1 = s1;
    score2 = s2;
    score3 = s3;
    major = maj;
}
```

![](img/e33ae760e23d89eac66541252ad65de8_223_0.png)

> 应该将类设计得尽可能灵活且功能完整。实现这一点的一种方法是包含多个构造函数。但是，仅仅试图为数据成员的每一种可能组合都定义一个构造函数并不合适。应根据其他类可能如何需要并实例化该类的对象，来确定并设计适当数量的构造函数。

请注意，示例 4-3 中显示的第一个构造函数不接受任何参数。这就是默认构造函数。如前所述，当你开始编写自己的构造函数时，就会失去自动生成的默认构造函数。但是，你通常希望提供灵活性，允许在没有任何参数的情况下实例化类的对象。这正是需要默认构造函数的地方。因此，你需要创建一个默认构造函数。

构造函数的方法体主要由赋值语句组成。请注意，私有数据成员标识符出现在等号左侧。参数标识符使用了与数据成员不同的名称。这样做是为了避免使用 this 关键字来引用数据成员。你将在后续章节中了解更多相关内容。

查看示例 4-3 中的第二个构造函数。数据成员 studentNumber 被赋值为 sID 中存储的值。使用该构造函数实例化类的对象时，数据将通过 sID 传入构造函数。

可以设计第五个构造函数，其第一个参数为 name，随后是表示 sID 的 int。它的签名将与首先列出 int 参数的构造函数不同。与重载方法一样，构造函数的签名必须不同。你不能让一个构造函数具有 firstName 和 lastName 两个 string 参数，然后又定义另一个接受 lastName 和 firstName 两个 string 参数的构造函数。它们的签名将相同。两者的参数列表都会包含两个 string。

![](img/e33ae760e23d89eac66541252ad65de8_224_0.png)

编写自己的默认构造函数时，方法体不必为空。默认构造函数通常没有参数。无参数构造函数可用于为数据成员分配默认值。

示例 4-4 展示了 CarpetCalculator 类的三个构造函数。

### 示例 4-4

```
// Constructor with no parameters--Default constructor
public CarpetCalculator( )
{
    //empty body
}
// Constructor with one parameter
public CarpetCalculator(double price)
{
    pricePerSqYard = price;
}
// Constructor with two parameters
public CarpetCalculator(double amountNeeded, double price)
{
    noOfSqYards = amountNeeded;
    pricePerSqYard = price;
}
```

一种标准命名约定是在实例变量标识符前面加上“Get”，并将该名称用作检索数据项的访问器方法名。示例 4-5 展示了一个用于 noOfSqYards 的访问器方法。该访问器的标识符是 GetNoOfSqYards()。

### 修改器

要更改对象成员数据的当前状态或值，可以使用称为修改器的特殊方法。修改器有时称为设置器。修改器通常编写为包含一个参数，该参数表示数据成员应具有的新值。与访问器一样，由于实例变量具有私有可访问性，因此需要修改器。示例 4-6 展示了两个重载的修改器。第一个示例是编写修改器的更常见方式。该方法体由单条赋值语句组成。

### 示例 4-6

```
public void SetNoOfSqYards(double squareYards)
{
    noOfSqYards = squareYards;
}
public void SetNoOfSqYards(double length,
    double width)
{
    const int SQ_FT_PER_SQ_YARD = 9;
    noOfSqYards = length * width / SQ_FT_PER_SQ_YARD;
}
```

![](img/e33ae760e23d89eac66541252ad65de8_226_0.png)

> 属性成员还能减少所需的修改器数量。

一种标准命名约定是在实例变量标识符前面加上“Set”；该名称将成为修改器方法名。在示例 4-6 中，被更改的实例变量是 noOfSqYards；该修改器的标识符是 SetNoOfSqYards()。

### 其他实例方法

你在第 3 章编写了类方法。类方法通过参数将信息作为实参传入来操作数据。对于实例方法，则不需要这样做。类的实例方法成员可以直接访问同一类的私有数据成员。正是通过实例方法才能操作私有数据。查看示例 4-7 中所示的实例方法 CalculateAverage()。请注意，该方法没有参数。CalculateAverage() 可以使用 score1、score2 和 score3，因为它们属于同一个类。

