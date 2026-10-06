
# 示例 45 使用示例 45 中的容器层次结构

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

# 示例 48 访问基构造函数、字段、方法、属性和索引器

类 C 使用 `base` 关键字来访问其基类 B 的实例成员：一个构造函数、一个字段、一个属性（第 10.15 节）、一个索引器（第 10.16 节）以及非虚方法作为虚方法。

```csharp
class B {
    public int f;
    public B(int f) { this.f = f; }
    public void M1() { Console.Write("B.M1 "); } // 非虚实例方法
    public virtual void M2() { Console.Write("B.M2 "); } // 虚实例方法
    public int Fval { get { return f; } // // 属性
    public int this[int i] { get { return f+i; } // 索引器
}
class C : B {
    public new int f;
    public C(int f) : base(f/2) {
        this.f = f;
        Console.WriteLine("{0} ({1}) ({2})", base.f, base.Fval, base[5]); // 11 11 16
        Console.WriteLine("{0} ({1}) ({2})", f, Fval, this[5]); // 22 22 27
    }

    public new void M1() { base.M1(); Console.Write("C.M1 "); }
    public override void M2() { base.M2(); Console.Write("C.M2 "); }
    public new int Fval { get { return f; } }
    public new int this[int i] { get { return f+i; } }
}
C c = new C(22);
c.M1(); c.M2();
```

# 10.5 类中的字段声明

字段的目的是在对象（非静态）或类（静态）内部存储值。字段必须在类声明中声明。字段声明具有以下形式之一：

```
field-modifiers type fieldname1, fieldname2, ...
field-modifiers type fieldname1 = initializer1, ...
```

`field-modifiers` 是 `static`、`readonly`、`new` 和一个成员访问修饰符的列表（第 10.3 节）。

如果类 C 中的 `f` 被声明为 `static`，则 `f` 与类 C 关联，可以独立于类 C 或其子类的任何对象进行引用。如果类 C 中的 `f` 未声明为 `static`，则 `f` 是与类 C 对象关联的实例字段，并拥有其字段的独立实例。可以通过 `o` 引用字段，其中 `o` 是 C 及其子类声明内部的表达式或非静态代码，形式为 `f`。

如果 `f` 被声明为 `readonly`，则可以在其他地方赋值，但不能作为 `out` 或 `ref` 参数（可能赋值多次）。它可以在构造函数的其他地方赋值。如果 `f` 是引用类型并指向一个对象或数组，则该对象的字段或数组的元素可以被修改。如果 `f` 是 `static`，则允许对 `f.x` 赋值，但此类赋值以及方法调用 `f(M)` 作用于 `f` 的临时副本，对 `f` 没有影响。

字段初始化器可以是表达式或数组初始化（第 9.1 节）。任何字段初始化器都不能引用 C 的字段或当前引用 `this`。静态字段初始化器只能引用 C 的静态成员。因此，字段初始化器是静态代码（第 10.1 节）。

字段的默认值取决于类型 `t`。如果 `t` 是简单类型，则字段初始化为 0（当 `t` 为整数时）、0.0（当 `t` 为 `float` 或 `decimal` 时）或在当 `t` 是一个字段具有默认初始值的结构体时（当 `t` 为 `struct` 时）。如果 `t` 是引用类型，默认值为 `null`。

静态字段在类加载时初始化。所有静态字段首先被赋予默认值，然后按照在类声明中出现的顺序执行静态初始化器，最后执行静态构造函数（第 10.12 节）（如果有）。

实例字段在构造实例时初始化，此时所有静态字段都已初始化（第 10.1 节）。

如果类 C 声明了一个实例字段 `f`，且 C 是具有实例字段 `f` 的类 B 的子类，则 `f` 的声明应该带有 `new` 修饰符。C 的每个对象有两个字段，一个是基类中声明的 B `f`，另一个是 C 中静态声明的 C `f`。字段访问 `o, f` 引用的是哪个字段取决于 `o` 的类型（第 12.15 节）。

# 10.6 类中的常量声明

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
此示例中的类 C 对象有两个实例字段 `nf`：一个在基类 B 中声明，另一个在 C 自身声明。同样，类 D 对象有三个实例字段 `nf`。类 B 和类 C 都有一个静态字段 `sf`。类 D 没有声明静态 `sf`，因此在类 D 中名称 `sf` 引用的是基类 C 中的静态字段 `sf`。

# 10.7 方法声明

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

`params` 必须在 `formal-list` 中只出现一次，且不能与 `ref` 或 `out` 修饰符一起。`parameter-modifier` 可以是 `out` 或缺失。既不是 `out` 也不是 `ref` 参数的是值参数。类型是任何类型表达式。`parametername` 是任何名称，但 `formal-list` 中没有两个参数名称相同。参数的作用域是 `method-body`。

值参数类似于局部变量。

`params` 修饰符用于声明可以接受数量参数的方法。方法声明中的形式参数必须是数组类型；在方法调用中，它将绑定一个包含零或多个参数值的数组，而不受前面的参数限制（见第 12.17.3 节）。参数数组不能与匿名方法一起。

方法名 `M` 以及 `formal-list` 中声明参数的列表 `t1,...,tn` 决定了方法签名 `M(t1,...,tn)`。签名包括任何 `ref` 和 `out` 修饰符，但不包括 `params` 修饰符（如果有）以及返回类型。

一个类可以声明多个具有相同名称 `M` 的方法，这些方法具有不同的签名。这被称为重载。重载方法可能有不同的返回类型。

`method-body` 是一个块语句（第 13.2 节）。特别是，如果返回类型为 `void`，则 `method-body` 不返回值，且 `method-body` 中的任何 `return` 语句不能有表达式参数。如果返回类型不是 `void`，方法必须返回一个值；在不执行 `return` 语句的情况下到达 `method-body` 的结尾。此外，每个 `return` 语句必须有一个可以隐式转换为返回类型的表达式参数。

合法的 `method-modifiers` 由一个成员访问修饰符（第 10.3 节）和一个方法修饰符（第 10.8 节）组成。

在一个基类句包含接口 `I` 的类中，方法声明中的方法名可以写为 `I.M`，以显式说明它实现了接口 `I` 中的方法；在这种情况下，可以没有方法修饰符（第 15.3 节）。

