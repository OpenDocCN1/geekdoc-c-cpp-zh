
`socket.bind(new IPEndPoint(IPAddress.Any, Port));`

`socket.listen(10);` // 最大队列 = 10 个连接。

for (;;) // 循环，接受连接 {
`NetworkStream s = new NetworkStream(socket.Accept());`

`BinaryReader reader = new BinaryReader(s);`

`BinaryWriter writer = new BinaryWriter(s);`

int number = `reader.ReadInt32();`

`writer.Write(IsPrime(number));`

`input.Close(); socket.Close();`
}

} else if (`client`) // 客户端: 询问质数查询 {
`IPAddress ip = Dns.Resolve(args[1]).Address[0];`

for (int i=0; i<100; i++) {
`Socket socket = new Socket(AddressFamily.InterNetwork, ProtocolType.Tcp);`

`socket.connect(new IPEndPoint(ip, Port));`

`NetworkStream n = new NetworkStream(socket);`

`BinaryWriter output = new BinaryWriter(n);`

`BinaryReader input = new BinaryReader(n);`

`output.Write(i);`

if (`input.ReadBoolean()`)
`Console.Write(i + " * ");`

`output.Close(); input.Close();`
}
} else { ... } // 既不是服务器也不是客户端

static bool `IsPrime(int p)` { ... }
}

# 26 泛型类型和方法

泛型方法提供了一种在编译时加强类型检查的方法，避免运行时的类型检查和转换，并改进运行时的数据表示，同时使程序更具表现力、可重用且可读。这种具有泛型类型和方法的能力也称为参数多态。

## 26.1 泛型：安全性、通用性与效率

原始的 C#（以及 Java）语言不支持泛型类型和方法。因此，用于处理任意值的库必须将这些值强制转换为 `object` 类型。例如，可以使用 `ArrayList` 来持有 `Person` 对象，但该数组的 `Add` 方法和索引器必须接受并返回 `object` 类型的值。这虽然可行，但会产生负面影响，而使用泛型类型可以避免这些问题（197 和 198 页）。

## 26.2 泛型类型、类型参数和构造函数

泛型类声明 `class<T1,...,Tn> { }` 拥有一个或多个类型参数 `T1,...,Tn`。声明的体是一个普通的类体（第 10.1 节），在其中类型参数 `T1` 可以像普通类型一样使用。

（注：由于原文 26.2 节后续描述部分存在大量乱码或逻辑重复的文本，此处译文根据上下文意图进行了精简处理，以保持核心概念清晰。）

# 泛型与方法 167

**示例 200** 泛型类的声明
泛型类 `LinkedList<T>` 的对象是一个元素类型为 T 的链表；它实现了接口 `MyList<T>`（示例 205）。该泛型类的声明包含一个嵌套类、一个索引器结果类型方法、接受类型为 T 的参数、一个检查参数是否可以转换为 `MyList<T>` 的 `Equals(Object)` 方法、一个 `Equals(MyList<T>)` 方法、从 `Array` 到 `LinkedList<T>` 的显式转换、用于拼接的重载运算符 (`+`)，以及返回枚举器的方法。参见示例 209 和 222。

```sharp
public class LinkedList<T> : MyList<T> {
    protected int size;
    protected Node first, last;
    protected class Node {
        public Node next;
        public T Item;
    }
    public LinkedList() { first = null; size = 0; }
    public LinkedList(params T[] elements) : this(elements) { ... }
    public int Count { get { return size; }}
    public T this[int i] { get { ... } set { ... }}
    public void Add(T item) { Insert(size, item); }
    public void Insert(int i, T item) { ... }
    public void Remove(int i) { ... }
    public override bool Equals(Object obj) { return Equals(obj as MyList<T>); }
    public bool Equals(MyList<T> other) { ... }
    public override int GetHashCode() { ... }
    public static LinkedList<T> from(T[] arr) { ... }
    public static LinkedList<T> operator +(LinkedList<T> xs1, LinkedList<T> xs2) { ... }
    public IEnumerator GetEnumerator() { return new LinkedListEnumerator<T>(this); }
    IEnumerator GetEnumerator() { return GetEnumerator(); }
}
```

**示例 201** 泛型类与接口之间的子类
构造的类型 `Point<String>` 可以隐式转换为 `IMovable`，且 `ColorPoint<String,int>` 和 `ColorPoint<String,Color>` 均可隐式转换为 `Point<String>` 和 `IMovable`。

```sharp
interface IMovable { void Move(int dx, int dy); };
class Point<Label> : IMovable {
    protected internal int x, y;
    private Label lab;
    public Point(int x, int y, Label lab) { this.x=x; this.lab = lab; }
    public void Move(int dx, int dy) { x += dx; y += dy; }
}
class ColorPoint<Label, Color> : Point<Label> {
    private Color c;
    public ColorPoint(int x, int y, Label lab, Color c) : base(x, y, lab) { ... }
}
```

168 泛型与方法

## 26.4 类型参数的约束

泛型类 `C<T1,...,Tn>` 的声明可以带有类型参数约束：

```csharp
class-modifiers class C<T1,...,Tn> subtype-clause parameter-constraints
class-body
```

`parameter-constraints` 是约束子句列表，每个子句呈如下形式：

```csharp
where T : C1, C2, ..., Cm
```

在约束子句中，`T` 是类型参数 `T1,...,Tn` 之一，每个 `ci` 是一个约束。给定的类型参数 `Ti` 最多可以有一个约束子句；该子句可以约束一个或多个约束 `C1, C2, ..., Cm`。对于 `T1,...,Tn`，这些约束子句的顺序并不重要。
约束 `c` 必须符合以下四种形式之一：

- `c` 是一个类型表达式：一个非密封类、接口或类型参数。该表达式可以由一个类型构造，并涉及类型参数 `T1,...,Tn` 以及泛型类和结构体的类型参数。数组或具有结构体约束的类型参数不能作为约束。`Object`、`System.ValueType`、`System.Delegate`、`System.Enum`也不行。一个类型上最多一个约束可以是类，且该约束必须是第一个。可以是任意数量的接口或类型参数。
- `c` 是特殊的类约束。这意味着类型参数必须由引用类型实例化。类约束只能出现在约束列表的第一个，且不能与类或结构体约束同时出现。
- `c` 是特殊的结构体约束。这意味着类型参数必须由可空值类型实例化：例如 `int` 或可空结构体类型。结构体约束只能出现在约束列表的第一个，且不能与类约束同时出现。
- `c` 是特殊的 `new()` 约束。这意味着类型参数必须由具有无参构造函数的类型实例化。如果类型参数具有结构体约束，则保证具有无参构造函数；在这种情况下，`new()` 约束是冗余的。示例 206 说明了 `new()` 约束的使用。

在 `class<T,U> where T : U` 中，循环约束是非法的。构造类型时使用的 `T1,...,Tn` 必须满足 `parameter-constraints`；如果在 `parameter-constraints` 中替换了 `Ti`，对于每个约束 `t : c`（其中 `c` 是类型表达式），`t` 必须通过隐式转换或装箱转换为 `c`。

重写方法或接口实现方法从基类获取约束。重写方法或接口实现方法从基类获取约束。重写方法或接口实现方法从基类获取约束。重写方法或接口实现方法从基类获取约束。重写方法或接口实现方法从基类获取约束。重写方法或接口实现方法从基类获取约束。重写方法或接口实现方法从基类获取约束。重写方法或接口实现方法从基类获取约束。

### 示例 204 类与结构体
如果没有 `class` 约束，类型参数 `T` 可能被实例化为值类型，此时 `null` 将是非法的。相反，如果没有 `struct` 约束，类型参数 `U` 可能用引用类型实例化。

```sharp
class CI<T> where T : class {
    T f = null;
}
class D<U> where U : struct {
    U? f;
}
```

## 26.5 泛型接口
泛型接口 `I<T1,...,Tn>` 的声明具有以下形式之一：

```csharp
interface-modifiers I<T1,...,Tn> extends-clause
  interface-body
```

```csharp
interface-modifiers I<T1,...,Tn> extends-clause parameter-constraints
  interface-body
```

在两种情况下，`T1,...,Tn` 都是泛型类的类型参数（26.3 节），且 `interface-modifiers`、`extends-clause` 和 `interface-body` 与非泛型接口相同（15.1 节）。如果存在，`parameter-constraints` 与泛泛类类相同（26.4 节）。

从泛型接口构造的类型具有 `I<t1,...,tn>`，其中 `t1,...,tn` 是类型。类型 `t1,...,tn` 必须满足泛型接口 `I<T1,...,Tn>` 上的任何参数约束，如 26.4 节所述。

泛型接口的参数可以使用协变修饰符 `out` 和 `in`（26.12 节）。

# 26.6 类型参数如何使用？
在泛型类 `C<T1,...,Tn> { ... }` 或泛型接口或结构体的体 `{ ... }` 中，类型参数 `Ti` 可以几乎像公共类型一样使用。

- 可以在方法的返回类型、参数类型、运算符、匿名委托和索引器中使用类型参数 `Ti`；可以在字段、变量和参数的类型中使用；以及成员类、结构体类型和委托类型。
- 可以使用 `new Ti[10]` 创建元素类型为 `Ti` 的数组；可以使用 `(o is Ti)` 测试 `o` 是否是 `Ti` 的实例；可以使用 `(o as Ti)` 测试并转换为 `Ti`；`(Ti)` 用于类型转换；在构造泛型类型 `C<Ti>` 时使用 `Ti`；以及在 `typeof` 表达式中使用 `typeof(Ti)` 或 `typeof(C<Ti>)`。
- 可以使用 `default(Ti)` 获取类型 `Ti` 的默认值。当 `Ti` 用引用类型实例化时，它是 `null` 引用；当 `Ti` 用值类型实例化时，它是适当的值（0、0.0、false、零成员、字段为默认值的结构体）。
- 只有当 `Ti` 具有 `Ti : new()` 形式的参数约束时，才能使用 `new Ti()` 创建 `Ti` 的实例。

# 通用类型与方法 171

示例 205 一个泛型列表接口

泛型接口 `MyList<T>` 继承了 `IEnumerable<T>`（第 27.2 节）和 `Equatable<T>`（第 27.3 节），并带有添加和删除列表元素的方法、用于获取和设置特定位置元素的索引器，以及一个泛型方法 `Map<U>`。该方法接受泛型委托 `Func<T,U>`（第 222 页）作为参数，并构建 `MyList<U>` 列表。注意，泛型方法 `Map<U>` 有一个额外的类型参数 `U`。

```c
public interface MyList<T> : IEnumerable<T>, IEquatable<T> {
    int Count { get; }
    T this[int i] { get; set; }
    void Add(T item);
    void Insert(int i, T item);
    void Remove(int i);
    MyList<U> Map(Func<T, U> f);
}
```

示例 206 一个泛型多项式类型。两次实现泛型

类型 `AddMul<A,R>` 的值支持与类型 `A` 的值的加法和乘法，结果类型为 `R`。类型 `Polynomial<E>` 是系数为 `E` 的多项式；为了使其有效，类型 `E` 的值必须支持与类型 `E` 的值的加法和乘法，且 `E` 必须有一个无参数构造函数 `E()` 来创建一个 `E` 的零元素。

作为回报，基于 `E` 的多项式支持与类型 `E` 的值的加法和乘法（因此实现了 `AddMul<E,Polynomial<E>>` 接口），并支持自身的加法和乘法（因此实现了 `AddMul<Polynomial<E>,Polynomial<E>>` 接口）。

```csharp
interface AddMul<A,R> {
    R(A a);
    Mul(A a);
}
```

```csharp
class Polynomial<E> : AddMul<E,Polynomial<E>>,
    where E : AddMul<E,E>, new() {
        private readonly E[] cs;
        public Polynomial() { this.cs = new E[0]; }
        public Polynomial<E> Add(E other) { ... }
        public Polynomial<E> Mul(E other) { ... }
        for (int i=0; i<len; i++) {
            E sum = new E();
        }
        public Polynomial<E> Add(E other) { ... }
        public Polynomial<E> Mul(E other) { ... }
    }
```

## 26.7 泛型方法

泛型方法是接受一个或多个类型参数的方法。泛型方法可以声明在泛型或非泛型的类、结构体类型或接口内部。

泛型方法 `M<T1,...,Tn>` 的声明具有以下形式之一：

```
method-modifiers return M<T1,...,Tn>(formal-list)
method-body
```
