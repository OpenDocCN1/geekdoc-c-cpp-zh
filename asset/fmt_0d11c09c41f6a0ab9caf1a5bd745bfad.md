
## 10.2 类修饰符 `abstract`, `sealed`, `static`

如果一个类 `C` 被声明为 `sealed`（密封），则它不能实例化，但 `C` 的非抽象子类可以实例化。抽象类可以拥有构造函数，在实例化非抽象子类时，可以通过 `base(...)` 调用从子类的构造函数中调用。抽象类可以声明 `abstract`（抽象）方法和非抽象方法，而非抽象类不能声明抽象方法。

如果一个类被声明为 `sealed`，则它不能声明 `C` 的子类，因此不能重写或隐藏 `C` 中声明的任何方法。这对于防止通过违反数据表示不变性来创建“恶意子类”很有用。

一个类不能既是抽象的又是密封的，因此无法创建该类的对象。然而，一个类可以声明为 `static`（静态），在这种情况下，它只有静态成员，且无法从它创建实例。这被用于声明工具类，如 `System.Math`，以及用于声明扩展方法（第 10.9 节）。

## 10.3 成员访问修饰符 `private`, `protected`, `internal`, `public`

成员（数据、函数或类型）在声明它的类中是可访问的，除非被成员的变量或参数、或者嵌套类或结构体的成员所遮蔽。可以使用以下访问修饰符使成员在其他地方可访问。以下访问修饰符（在类声明或结构体类型声明中）是有效的：

| 成员修饰符 | 访问权限 | 范围 |
| --- | --- | --- |
| `private` 或缺失 | 此类或结构体 | `private` |
| `internal` | 此程序集 | `internal` |
| `protected` | 此类 + 子类 | `C-protected` |
| `protected internal` | 此程序集 + 此类 | `protected internal` |
| `public` | 处处 | `public` |

`protected` 和 `internal` 修饰符可以用于类的成员，但不能用于结构体的成员（第 14 节），因为后者不能有子类。接口（第 15 节）的所有成员都是隐式的 `public`，且只有可以使用 `public` 访问修饰符，但并非必须是。

- 如果成员在类 `C` 中被声明为 `private`，则它在 `C` 及其嵌套类和结构体类型中可访问，但在其子类或其他类中不可访问。
- 没有显式访问修饰符的成员是 `private` 的。
- 如果成员被声明为 `internal`，则它在 `C` 所在的地方可访问，但仅在 `C` 的同一程序集内（第 1.1 节）。
- 如果成员被声明为 `protected`，则它在 `C` 的子类中可访问。
- 如果成员被声明为 `protected internal`，则它在 `C` 所在的地方可访问，但在 `C` 的同一程序集内，以及在 `C` 的子类中访问。（这类似于 Java 的保护 成员的概念）。
- 如果成员被声明为 `public`，则它在 `C` 所在的地方可访问，在其他程序集中也可以访问。

# 类 37

**示例 45** 类、子类和重写
抽象类 `Vessel` 定义了盛装液体容器的概念：其字段 `contents` 代表其实际内容，抽象方法 `Capacity` 计算其最大容量，方法 `Fill` 填充更多内容，但仅限于其容量；抽象类还包括 `Tank`（矩形容器）、`Cube`（立方体容器，`Tank` 的子类）和 `Barrel`（圆柱形容器）。子类实现 `Capacity` 方法；它们从基类继承字段和 `Fill` 方法，并重写 `toString` 方法（继承自 `Object` 类）来格式化每个容器对象。

```sharp
public abstract class Vessel {
    private double contents;
    public abstract double Capacity();
    public void Fill(double amount) {
        if (amount <= Capacity()) contents += amount;
        else contents = Capacity();
    }
    public override String toString() { return "(" + contents + ")"; }
}
public class Tank : Vessel {
    protected double length, width, height;
    public Tank(double length, double width, double height) {
        this.length = length;
        this.width = width;
        this.height = height;
    }
    public override double Capacity() { return length * width * height; }
    public override String toString() { return "tank(" + base.toString() + ")"; }
}
public class Cube : Tank {
    private double side;
    public Cube(double side) : base(side, side, side) {
        this.side = side;
    }
    public override double Capacity() { return side * side * side; }
    public override String toString() { return "cube(" + base.toString() + ")"; }
}
public class Barrel : Vessel {
    private protected double radius, height;
    public Barrel(double radius, double height) {
        this.radius = radius;
        this.height = height;
    }
    public override double Capacity() { return Math.PI * radius * radius * height; }
    public override String toString() { return "barrel(" + base.toString() + ")"; }
}
```

**示例 46** 成员修饰符
抽象类 `Vessel` 定义了盛装容器的概念：其字段 `contents` 代表其实际内容，抽象方法 `Capacity` 计算其最大容量，方法 `Fill` 填充更多内容，但仅限于其容量；抽象类包括 `Tank`（矩形容器）、`Cube`（立方体容器，`Tank` 的子类）和 `Barrel`（圆柱形容器）。子类实现 `Capacity` 方法；它们从基类继承字段和 `Fill` 方法，并重写 `toString` 方法（继承自 `Object` 类）来格式化每个容器对象。

## 10.4 子类、基类、继承和遮蔽

类 `C` 的声明可以显式声明其基类 `B`，使用 `base` 子句：其中 `B` 是一个类。这时说 `C` 自 `B`。如果类 `C` 没有显式声明其基类，它是 `Object` 的子类。类 `C` 继承除构造函数以外的所有非私有成员（第 15.2 节）。一个类最多有一个直接基类。预定义的类 `Object` 没有基类。子类 `C` 中的构造函数（第 10.11 节）可以声明显式调用基类中的特定构造函数，使用此语法：

```sharp
constructor-modifier C(formal-list) : base(actual-list)
constructor-body
```

如果子类 `C` 中的构造函数没有以这种方式显式声明 `base(...)`，则它会隐式调用基类中的默认构造函数 `B()` 作为其第一个操作。在这种情况下，`B` 必须有一个无参数构造函数 `B()`。相反，如果 `B` 没有无参数构造函数，那么 `C` 中的构造函数 必须使用 `base(...)` 显式调用 `B` 的另一个构造函数。`C` 中的方法声明可以重写从 `B` 继承的非密封虚方法 `M`，通过声明具有完全相同签名的方法 `M`。重写的方法 `M` 在 `C` 的实例构造函数和实例方法内部可以通过 `base.M` 引用。`C` 中重写方法 `M` 的权限至少要与重写方法相同。

然而，类 `C` 的声明不能重新声明从 `B` 继承的字段 `f`，只能将其遮蔽并声明一个同名的字段（第 10.5 节）。隐藏的字段 `B` 在 `C` 的实例构造函数和实例方法内部可以通过 `base.f` 引用。

`C` 中的声明可以隐藏从基类 `B` 继承的成员。示例 55 举了方法重写和隐藏之间的区别。`C` 中的隐藏方法应该具有 `new` 修饰符，否则编译器会给出警告。

### 示例 45 使用示例 45 中的容器层次结构

调用 `vs[i].Capacity()` 是合法的，因为 `Capacity` 是在抽象类 `Vessel`（示例 45）中声明的。

```csharp
public static void Main(String[] args) {
    Vessel v1 = new Barrel(3, 10);
    Vessel v2 = new Tank(10, 20, 12);
    Vessel v3 = new Cube(4);
    Vessel[] vs = { v1, v2, v3 };
    v1.Fill(90); v2.Fill(100); v3.Fill(80);
    double sum = 0;
    for (int i=0; i<vs.Length; i++) {
        sum += vs[i].Capacity();
    }
    Console.WriteLine("Total capacity is " + sum);
    sum = 0;
    for (int i=0; i<vs.Length; i++) {
        Console.WriteLine("Total contents is " + sum);
    }
    for (int i=0; i<vs.Length; i++) {
        Console.WriteLine("vessel number " + i + ": " + vs[i]);
    }
}
```

### 示例 48 访问基构造函数、字段、方法、属性和索引器

类 `C` 使用 `base` 关键字来访问其基类 `B` 的实例成员：一个构造函数、一个字段、一个属性（第 10.15 节）、一个索引器（第 10.16 节）以及非虚方法作为虚方法。

```csharp
class B {
    public int f;
    public B(int f) { this.f = f; }
    public void M1() { Console.Write("B.M1 "); }
    public virtual void M2() { Console.Write("B.M2 "); }
    public int Fval { get { return f; } }
    public int this[int i] { get { return f+i; } }
}
class C : B {
    public new int f;
    public C(int f) : base(f/2) {
        this.f = f;
        Console.WriteLine("{0} ({1}) ({2})", base.f, base.Fval, base[5]);
        Console.WriteLine("{0} ({1}) ({2})", f, Fval, this[5]);
    }
    public new void M1() { base.M1(); Console.Write("C.M1 "); }
    public override void M2() { base.M2(); Console.Write("C.M2 "); }
    public new int Fval { get { return f; } }
    public new int this[int i] { get { return f+i; } }
}
C c = new C(22);
c.M1(); c.M2();
```

## 10.5 类中的字段声明

字段的目的是在对象（非静态）或类（静态）内部存储值。字段必须在类声明中声明。字段声明具有以下形式之一：

```
field-modifiers type fieldname1, fieldname2, ...
field-modifiers type fieldname1 = initializer1, ...
```

`field-modifiers` 是 `static`、`readonly`、`new` 和一个成员访问修饰符的列表（第 10.3 节）。

如果类 `C` 中的 `f` 被声明为 `static`，则 `f` 与类 `C` 关联，可以独立于类 `C` 或其子类的任何对象进行引用。如果类 `C` 中的 `f` 未声明为 `static`，则 `f` 是与类 `C` 对象关联的实例字段，并拥有其字段的独立实例。可以通过 `o` 引用字段，其中 `o` 是 `C` 及其子类声明内部的表达式或非静态代码，形式为 `f`。

如果 `f` 被声明为 `readonly`，则可以在其他地方赋值，但不能作为 `out` 或 `ref` 参数（可能赋值多次）。它可以在构造函数的其他地方赋值。如果 `f` 是引用类型并指向一个对象或数组，则该对象的字段或数组的元素可以被修改。如果 `f` 是 `static`，则允许对 `f.x` 赋值，但此类赋值以及方法调用 `f(M)` 作用于 `f` 的临时副本，对 `f` 没有影响。

字段初始化器可以是表达式或数组初始化（第 9.1 节）。任何字段初始化器都不能引用 `C` 的字段或当前引用 `this`。静态字段初始化器只能引用 `C` 的静态成员。因此，字段初始化器是静态代码（第 10.1 节）。

字段的默认值取决于类型 `t`。如果 `t` 是简单类型，则字段初始化为 0（当 `t` 为整数时）、0.0（当 `t` 为 `float` 或 `decimal` 时）或在当 `t` 是一个字段具有默认初始值的结构体时（当 `t` 为 `struct` 时）。如果 `t` 是引用类型，默认值为 `null`。

静态字段在类加载时初始化。所有静态字段首先被赋予默认值，然后按照在类声明中出现的顺序执行静态初始化器，最后执行静态构造函数（第 10.12 节）（如果有）。

实例字段在构造实例时初始化，此时所有静态字段都已初始化（第 10.1 节）。

如果类 `C` 声明了一个实例字段 `f`，且 `C` 是具有实例字段 `f` 的类 `B` 的子类，则 `f` 的声明应该带有 `new` 修饰符。`C` 的每个对象有两个字段，一个是基类中声明的 `B` `f`，另一个是 `C` 中静态声明的 `C` `f`。字段访问 `o, f` 引用的是哪个字段取决于 `o` 的类型（第 12.15 节）。

## 10.6 类中的常量声明

类中的常量类似于静态 `readonly` 字段，但它的值是在编译时计算的：

```
const-modifier const type fieldname = initializer1, ...
```

常量是隐式 `static` 的。`const-modifier` 必须是成员访问修饰符之一（第 10.3 节）。类型必须是简单类型（第 5.1 节）或 `String` 或引用。初始化器表达式必须是编译时常量表达式；除了 `String` 外，唯一可能的值是 `null`。

# 类 41

### 示例 49 字段声明
`APoint` 类（示例 44）声明了一个静态字段 `allpoints` 和两个实例字段 `x` 和 `y`。

示例 56 声明了一个类型为 `double[]` 的静态字段 `ps`。其字段初始化器分配了一个数组并将其绑定到 `ps`。

`Barrel` 类（示例 45）声明了两个实例字段 `radius` 和 `height`。字段是只读的，因此必须在构造函数中初始化。

### 示例 50 同名的字段
此示例中的类 `C` 对象有两个实例字段 `nf`：一个在基类 `B` 中声明，另一个在 `C` 自身声明。同样，类 `D` 对象有三个实例字段 `nf`。类 `B` 和类 `C` 都有一个静态字段 `sf`。类 `D` 没有声明静态 `sf`，因此在类 `D` 中名称 `sf` 引用的是基类 `C` 中的静态字段 `sf`。

## 10.7 方法声明

方法必须在类（或结构体）内部声明（见第 14 节）。相应方法的声明形式如下：

```
method-modifiers returntype M(formal-list)
method-body
```

`formal-list` 是一个由逗号分隔的参数声明列表，每个具有以下形式之一：

```
parameter-modifier type parametername
type[] parametername
type parametername = constant
```
