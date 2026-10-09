
Value of b before call: 10

Value of b after call: 10

## 注意事项

输出参数和参数由 `out` 修饰符定义。

列表 7.5 所示的 `OutParameter.cs` 程序演示了如何在方法中使用输出参数。

### 列表 7.5 OutParameter.cs 文件中的程序代码

```sharp
using System;
class Passing {
    int a,b;
    public int AddMult(int x, int y, out int z) {
        a=x;
        b=y;
        z=a*b;
        return a+b;
    }
}
class OutParameter {
    static void Main() {
        Passing p = new Passing();
        int u,v,add,mult;
        u=10;
        v=20;
        add=p.AddMult(u,v, out mult);
        Console.WriteLine("The addition of the values (0) and (1) equals (2), and the multiplication of those values equals (3)", u,v,add,mult);
    }
}
```

### 输出：

值 10 和 20 的相加等于 30，这些值的乘积等于 200

你可以看到创建了 `Passing` 类的对象 `p`。然后参数 `u`、`v` 和 `mult` 被传递给方法 `AddMult`，它们分别被赋值给参数 `x`、`y` 和 `z`。参数 `mult` 带有 `out` 修饰符传递，这意味着赋值给 `AddMult` 中参数 `z` 的值也会赋值给参数 `mult`。参数 `x` 和 `y` 中的值用于初始化 `Passing` 类的数据成员 `a` 和 `b`。对于输出参数 `z`，被赋值了前两个参数的乘积。赋值给参数 `z` 的值也会赋值给参数 `mult`。当程序控制返回调用者时，通过 `mult` 参数显示了前两个参数 `u` 和 `v` 的乘积。

## 方法重载

当一个类具有两个或多个同名但参数数量和类型不同（称为签名）的方法时，就会发生方法重载。重载的方法也可能具有不同的返回类型。当调用重载方法时，系统会根据使用的参数数量和类型来查找并执行匹配的方法。

列表 7.6 所示的 `MethodOverload1.cs` 程序通过计算不同数量和类型参数的和来演示了方法重载。

### 列表 7.6 MethodOverload1.cs 文件中的程序代码

```sharp
using System;
class AddVal {
    public void compute_sum(int x) {
        Console.WriteLine("Sum is (0)", x);
    }
    public void compute_sum(int x, int y) {
        Console.WriteLine("Sum is (0)", x+y);
    }
    public void compute_sum(int x, double y) {
        Console.WriteLine("Sum is (0)", x+y);
    }
    public void compute_sum(double x, double y) {
        Console.WriteLine("Sum is (0)", x+y);
    }
}
class MethodOverload1 {
    static void Main() {
        AddVal av = new AddVal();
        av.compute_sum(5);
        av.compute_sum(5,8);
        av.compute_sum(5, 9.17);
        av.compute_sum(3.782, 9.17);
    }
}
```

### 输出：

Sum is 5

Sum is 13

Sum is 14.17

Sum is 12.952

你可以看到创建了一个名为 `av` 的 `AddVal` 类对象。该类的 `compute_sum` 方法被重载了。它被设置为接收以下内容：

- 单个 `int` 类型参数
- 两个 `int` 类型参数
- 一个 `int` 类型参数和一个第二个 `double` 类型参数
- 两个参数均为 `double` 类型

因此，通过在对象 `av` 上调用 `compute_sum` 方法来计算并显示不同类型参数的和。该方法显示了单个 `int` 类型参数、两个 `int` 类型参数、一个 `int` 类型参数和一个 `double` 类型参数的和，以及两个 `double` 类型参数的和。

## 封装

面向对象编程（OOP）另一个重要特性是封装，它是隐藏数据或将其从外部隔离的过程。只有通过类中关联的方法，才能访问和操作数据。对象通过方法定义了关联数据上可以进行的所有操作。因此，通过对象调用相应的方法来访问和更新数据。通过封装，你可以使类更加安全和可靠。封装还简化了调试和程序维护任务。

通过实现以下点确保封装：

- 将数据成员定义为 `private`（私有），从而确保类的数据成员无法从对象实例直接访问。
- 通过类方法或使用属性访问私有数据成员。属性使用一对公共访问器方法（`get`）和修改方法（`set`）来操作类的私有成员。

列表 7.7 所示的 `ClassDemo3.cs` 程序显示了工人类的代码、名称和基本薪资。所有三个数据成员都被定义为 `private` 以确保封装。你只能通过类方法访问这些数据成员，而不能通过实例直接访问。此外，该程序的重点是让你理解字符串是如何传递给类方法的。

### 列表 7.7 ClassDemo3.File 中的程序代码

```sharp
using System;
class Worker {
    private int code,basicSalary;
    private string name;

    public void setWorker(int x, string y, int z) {
        code=x;
        name=y;
        basicSalary=z;
    }
    public void showWorker() {
        Console.WriteLine("Code: (0), Name: (1), Salary: (2)", code,name,basicSalary);
    }
}
class ClassDemo3 {
    static void Main() {
        Worker w = new Worker();
        w.setWorker(101, "John", 5000);
        w.showWorker();
    }
}
```

### 输出：

Code: 101, Name: John, Salary: 5000

## 属性的使用

```csharp
r.bread=20;
Console.WriteLine("Length={0}, Bread={1} and Area of rectangle is ({2})",
r.length, r.bread, r.length*r.bread);
```

### 输出：

length 和 bread 的初始值为 0 和 0

Length=5, Bread=8 and Area of rectangle is 40

Length=5, Bread=20 and Area of rectangle is 100

在前面的示例中，创建了一个 `rect` 类的对象。默认构造函数将数据成员 `l` 和 `b` 的值初始化为 0。之后，使用 `length` 和 `bread` 属性将值 5 和 8 赋值给对象 `r`的数据成员 `l` 和 `b`。通过 `get` 方法访问数据成员 `l` 和 `b` 中的值并相乘以计算矩形的面积。通过属性向数据成员 `l` 和 `b` 赋值时，会调用 `set` 方法，该方法确保在初始化数据成员之前提供的值值为正数。如果提供了负值，它将被简单地丢弃。

列表 7.10 显示的 `SetGet.cs` 程序是关于属性的另一个示例。该程序定义了一个 `Worker` 类，它使用属性为工人对象分配代码、名称和基础数据，并使用相应的访问器（accessors）和修改器（mutators）显示类的不同数据成员。

### 列表 7.10 SetGet.cs 文件中的程序代码

```csharp
using System;
class Worker {
    private int code, basicSalary;
    private string name;
    public int Code {
        get { return code; }
        set { code=value; }
    }
    public string Name {
        get { return name; }
        set { name=value; }
    }
    public int Salary {
        get { return basicSalary; }
        set { basicSalary=value; }
    }
}
```

```csharp
public void showWorker() {
    Console.WriteLine("Code: {0}, Name: {1}, Basic Salary: {2}", Code, Name, Salary);
}
class SetGet {
    static void Main() {
        Worker w = new Worker();
        w.Code="101";
        w.Name="Kelly";
        w.Salary=5000;
        w.showWorker();
    }
}
```

### 输出：

Code: 101, Name: Kelly, Basic Salary: 5000

创建了一个 `Worker` 类的实例。定义了三个属性：`Code`、`Name` 和 `Salary`，带有相应的访问器和修改器。使用 `set` 方法（修改器），将值 101、Kelly 和 5000 赋值给实例 `w` 的数据成员 `code`、`name` 和 `basicSalary`。在 `w` 对象上调用了 `showWorker` 方法，该方法通过访问来获取数据成员 `code`、`name` 和 `basicSalary` 中的数据并将其显示在屏幕上。

## this 关键字

`this` 关键字指的是当前被引用的对象或当前实例。例如，当通过对象调用类的方法时，对象的引用会自动传递给被调用的方法。传递给被调用方法的对象引用被称为 `this`。它是隐式存在的。

列表 7.11 显示的 `thisExample.cs` 程序演示了 `this` 关键字如何表示被引用的类实例。该程序计算矩形的面积。

### 列表 7.11 thisExample.cs 文件中的程序代码

```csharp
using System;
class RectArea {
    private int l,b;
    public void setData(int l1, int b) {
        this.l=l1;
        this.b=b;
    }
```

### this 关键字 211

```csharp
public int getRect() {
    return this.l*this.b;
}

class thisExample {
    static void Main() {
        RectArea rect = new RectArea();
        rect.setData(5,8);
        Console.WriteLine("Area of rectangle is {0}", rect.getRect());
    }
}
```

### 输出：

Rectangle area is 40

在前面的代码中，你看到创建了一个名为 `rect` 的 `RectArea` 类对象或实例。调用了 `rect` 对象上的 `setData` 方法，并将参数 5 和 8 传递给它。在调用 `setData` 方法时，对象本身（`rect`）也被传递给方法。通过使用 `this` 关键字，可以在 `setData` 方法中引用并使用 `rect` 对象。传递的参数被赋值给 `setData` 方法的参数 `x` 和 `y`。语句 `this.l=x` 将参数 `x` 中的值赋值给 `rect` 对象的数据成员 `l`。换句话说，也存在语句 `this.l=x`。之前的示例没有使用 `this` 关键字，因为它是隐式存在的。它的作用相同：将参数 `x` 中的值赋值给调用方法的对象（即 `rect` 对象）的数据成员 `l`。因此，`setData` 方法初始化了 `rect` 对象的数据成员 `l` 和 `b`。最后，在 `rect` 对象上调用 `getRect` 方法来计算并返回矩形的面积。

从前面的讨论可以清楚看出，以下两个语句在功能上是相同的：

```csharp
l=x;
this.l=x;
```

`this` 关键字还有助于解决数据成员名称和参数名称匹配时的歧义问题，如 `setData` 方法所示：

```csharp
class RectArea {
    private int l, b;
    public void setData(int l, int b) {
        this.l=l;
        this.b=b;
    }
}
```

## 第7章 类与对象

你可以看到类的成员成员与参数的名称匹配。以下语句会导致歧义：

```csharp
l=l;
b=b;
```

会出现警告信息，提示赋值给了同一个变量（见图 7.1）。

![](img/3ca47f8f6f556f07650d3563e2f205_230_0) 图7.1 类成员名称匹配时出现警告。来源：Visual Studio。

可以通过使用 `this` 关键字来消除歧义，如下方法所示：

```csharp
class RectArea {
    private int l1,b;
    public void setData(int l1, int b) {
        this.l1=l1;
        this.b=b;
    }
}
```

前面代码中的语句 `this.l1=l1` 表示将 `l1` 赋值给 `rect` 对象的数据成员 `l1`。

## 构造函数

构造函数是用于初始化类的特殊方法。它在创建类实例时自动调用。构造函数的名称与类相同，且没有返回类型。

### 语法

```csharp
class classname(parameter list) {
    // 构造函数体
}
```

构造函数的访问修符通常是 `public`，因为它在类外部被调用。如果标记为 `private`，则无法在外部访问。构造函数分为以下类型：

- 默认构造函数——没有参数的构造函数
- 参数构造函数——带有参数的构造函数

如前所述，默认构造函数初始化实例变量。列表 7.12 中的 `Constructor1.cs` 程序演示了如何使用默认构造函数。

### 列表 7.12 Constructor1.cs 文件中的程序代码

```csharp
using System;
class RectArea {
    private int l,b;
    public RectArea() {
        l=5;
        b=8;
    }
    public int getRect() {
        return l*b;
    }
}
```

```csharp
class Constructor1 {
    static void Main() {
        RectArea rect = new RectArea();
        Console.WriteLine("Area of rectangle is {0}", rect.getRect());
    }
}
```

### 输出：

Rectangle area is 40

# 构造函数 215

```csharp
public void showWorker() {
    Console.WriteLine("Code: (0), Name: (1), Basic Salary: (2)", code,name, basicSalary);
    Console.WriteLine("Household allowance: (0), Child allowance: (1), Gross Salary: (2)", houseAllowance,childAllowance,grossSalary);
}

class DefConstructWorker {
    static void Main() {
        Worker w = new Worker();
        w.computeSal();
        w.showWorker();
    }
}
```

### 输出：

Code: 101, Name: Kelly, Basic Salary: 5000

Household allowance: 300, Child allowance: 250, Gross salary: 5550
