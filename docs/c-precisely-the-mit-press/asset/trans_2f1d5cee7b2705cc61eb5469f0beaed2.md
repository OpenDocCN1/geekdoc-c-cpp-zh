

# 接口

## 15 接口

### 15.1 接口声明

接口描述了方法、属性、索引器和事件，但并不实现它们。接口声明可以包含方法描述、索引器描述和事件描述。接口中的描述可以以任何顺序出现：

```c
interface-modifiers interface I base-interfaces {
  method-descriptions
  property-descriptions
  indexer-descriptions
  event-descriptions
}
```

接口可以在顶层声明，也可以在命名空间、类或结构体内部声明。在命名空间的顶层，接口修饰符可以是 `public` 或 `internal`（即内部）。在类或结构体内部，接口修饰符可以是任何成员修饰符（第 10.3 节）。在类中，它还可以用于隐藏继承自基类的接口。

接口声明由一个或多个部分类型声明组成（第 30 节）。`base-interfaces` 子句不存在。否则，接口声明格式如下：

```
interface-modifiers interface I : I1, I2, ... { }
```

其中 I1, I2,... 是一个非空的接口列表。如果存在 `base-interfaces` 子句，则接口 I 描述了由 I1, I2,..., 描述的所有成员，并且是 I1, I2.... 的子接口。接口 I 可以描述基接口 I1, I2.... 中未被描述的额外方法、属性、索引器和事件，并且可以通过描述新成员来隐藏继承的成员。方法 M 的方法描述必须具有：

```
description-modifier returntype M(format-list);
```

其中，如果该描述隐藏了继承自基接口（如 I1）的成员，则 `description-modifier` 应该是 `new`（否则将传递给编译器）。不能给出任何访问修饰符；所有接口隐式为 `public`。对于属性 P 的属性描述必须具有：

```
description-modifier returntype P {
  get;
  set;
}
```

其中 `get` 和 `set` 任意一个可以省略。索引器描述必须具有：

```
description-modifier returntype this[format-list] {
  get;
  set;
}
```

其中 `get` 和 `set` 任意一个可以省略。对于事件 E 的事件描述必须具有：

```
description-modifier event delegate-type E;
```

## 示例 146 三个接口声明

`Colored` 接口描述属性 `GetColor`，`Drawable` 接口描述方法 `Draw`，而 `ColoredDrawable` 则同时描述两者。这些方法隐式为 `public`。

```csharp
// System.Drawing; Graphics, SolidBrush, Pen, ...
interface IColored { Color GetColor(); get; }
interface IDrawable { void Draw(Graphics g); }
interface IColoredDrawable : IColored, IDrawable { }
```

## 示例 147 实现接口的类

属性 `GetColor` 和方法 `Draw` 必须是 `public`，如示例 146 中的接口所示。

```csharp
class ColoredPoint : Point, IColored {
    protected Color c;
    public ColoredPoint(int x, int y, Color c) : base(x, y) { this.c = c; }
    public Color GetColor() { get { return c; } }
}
class ColoredDrawablePoint : ColoredPoint, IDrawable {
    public DrawablePoint(int x, int y, Color c) : base(x, y, c) { }
    public void Draw(Graphics g) {
        g.FillRectangle(new SolidBrush(c), x, y, 2, 2); 
    }
}
class ColoredRectangle : IDrawable {
    private int x1, x2, y1, y2; // (x1, y1) 左上角,(x2, y2) 右下角
    protected Color c;
    public ColoredRectangle(int x1, int y1, int x2, int y2, Color c) {
        this.x1 = x1; this.y1 = y1; this.x2 = x2; this.y2 = y2; this.c = c; 
    }
    public Color GetColor() { get { return c; }
    public void Draw(Graphics g) { g.DrawRectangle(new Pen(c), x1, y1, x2, y2); }
}
```

## 示例 148 接口是一种类型

`Colored` 值具有 `GetColor` 属性；`Drawable` 值还额外有一个 `Draw` 方法。

```csharp
static void PrintColors(IColored[] cs) {
    for (int i=0; i<cs.Length; i++) {
        Console.WriteLine(cs[i].GetColor());
    }
}
static void Draw(Graphics g, IDDrawable[] cs) {
    for (int i=0; i<cs.Length; i++) {
        cs[i].Draw(g);
    }
}
```

## 15.2 实现接口的类和结构体类型

类 C（第 10.1 节）可以通过类子句声明为实现一个或多个接口。同样，结构体类型 S（第 4 节）可以通过结构体子句声明为实现一个或多个接口。两者都具有：

```: I1, I2, ...
```

如果这应用于类 C 的声明，则意味着类 C 的引用可以通过引用转换（第 5.2 节）隐式转换为类型 I1、I2 等。如果应用于结构体 S 的声明，则意味着类型 S 的值可以通过装箱转换（第 5.3 节）隐式转换为类型 I1、I2 等。接口 I1、I2 等类或结构体类型的基接口。编译器将检查 C 是否声明（或继承自）I1、I2 描述的每个函数成员，且具有完全相同的签名，包括 `ref` 和 `out` 修饰符以及指定的返回类型。只有类或结构体中的公共实例方法、属性、索引器和事件可以实现接口描述的成员；静态或非公共成员则不行。

## 15.3 显式接口实现

当类实现接口 I 时，它可以对任何方法、属性、索引器或事件声明显式接口实现。此类实现具有以下形式：

returntype I.M(format-list) method-body
returntype I.P { get-body set-body }
returntype I.this[format-list] { get-body set-body }
delegate-type I.E { add-body remove-body }

显式接口实现无法访问成员，但隐式为 `public`。一个成员不能实现多个接口。由显式接口实现声明的成员是实例成员，可以通过 `o.M(...)` 或 `o.P` 访问，其中 `o` 是该类型的表达式，可能通过显式转换获得（第 150 节）。当类必须同时实现泛型接口如 `IEnumerator<T>` 和旧版非泛型接口 `IEnumerator`（第 2.2 节）时，显式接口实现非常有用。这些接口都描述了一个只读属性 `Current`，但类型不同。使用显式接口实现，可以如下声明：

```csharp
T IEnumerator<T>.Current { get { ... } }
object IEnumerator.Current { get { ... } }
```

命名空间 `System.Collections` 简写为 SC。参见示例 6 和 4。

## 示例 149 接口属性和索引器

`ISeq` 接口 `IEnumerable<int>`（可以作为 int 枚举）描述了一个只读属性 `Count`，用于给出序列长度，以及两个返回序列成员的索引器。当添加了属性和索引器后，结构体 `Seq` 实现 `ISeq`。

```csharp
interface ISeq : IEnumerable<int> {
    int Count { get; }
    int this[int i] { get; }
    int[] this[params int ii] { get; }
}
struct Seq : ISeq {
    ...
    public int Count { get; return n; }
    public int this[int i] { get { return b + k * i; }
    public int[] this[params int ii] { ... this[ii] }
}
```

## 示例 150 显式接口成员实现

显式接口实现允许类 C按照 I2 的指定通过 I1 实现方法 M0，尽管后者隐藏了前者。它还允许类 C 实现方法签名 `M1()`，尽管 I2 和 I3 对该方法有不同的返回类型。D 的子类继承 C 的显式接口成员实现。

```csharp
interface I1 { void M0(); }
interface I2 : I1 {
    new void M0();
    int M1();
}
interface I3 : I1 {
    void M1();
    int P { get; }
    int this[int i] { get; }
}
class C : I1, I2, I3 {
    public void M0() { Console.Write("C.M0 "); }
    void I1.M0() { Console.Write("C:I1.M0 "); }
    void I2.M0() { Console.Write("C:I2.M0 "); }
    int I2.M1() { Console.Write("C:I2.M1 "); return 1; }
    void I3.M1() { Console.Write("C:I3.M1 "); }
    int I3.P { get { return i+((I3)this).P; } }
    void I3.M0() { // Illegal: M0 在 I3 中未显式声明 }
}
class D : C {
    C c = new C();
    // C.M0 C:I1.M0 C:I2.M0 C:I2.M1 C:I3.M1
    c.M0(); ((I1)c.M0()); ((I2)c.M0()); ((I2)c.M1()); ((I3)c.M1());
}
```
```
