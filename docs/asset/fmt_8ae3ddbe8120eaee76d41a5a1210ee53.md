
`Final` 的目的是一种特殊的类引用，它绑定到某些对象并永远不释放它。“忠实”的引用在许多设计中都是非常有用的。

第一步是消除赋值。问题是，如果缺失赋值运算符，编译器会自动生成它，因此 `Final` 必须礼貌地指示编译器不要这样做。为了实现这一点，请使用 `@disable` 属性：

```d
struct Final(T) {
    // 禁用赋值
    @disable void opAssign(Final);
    ...
}
```

你可以使用 `@disable` 来移除其他生成的函数，例如比较。到目前为止一切良好。为了实现 `Final!`，我们需要确保该类型通过 `alias this` 成为 `T` 的子类型，但不提供左值（lvalue）。一个错误的设计如下所示：

```rust
// 错误的设计
struct Final(T) {
    private T payload;
    this(T) bindTo() {
        payload = bindTo;
    }
    // 禁用赋值
    @disable void opAssign(Final);
    // 子类 T
    alias payload this;
}
```

`Final` 在 `payload` 成员中持有其值并在构造函数中初始化它。它还通过声明 `opAssign` 但从不定义它，有效地禁用了赋值。这样，尝试给 `Final!T` 类型对象赋值的客户端要么无法访问（因为是 `private` 的），要么会遇到链接时错误。

`Final` 的错误在于引入了 `alias payload this`。这里有一个完成了不该执行的任务的单元测试：

```rust
class A {
    int value = 42;
    this(int x) { value = x; }
}
utittest {
    auto v = Final!A(new A(42));
    void sneaky(ref A ra) {
        ra = new A(4242);
    }
    sneaky(v); // 嗯mmm...
    assert(v.value == 4242); // 通过了？？
}
```

`payload this` 的工作原理非常简单。每当类型为 `Final!T` 的值 `obj` 在一个对其类型非法的上下文中使用时，编译器就会将其重写为 `obj.payload`（换句话说，它让 `obj.payload` 成为 `obj` 的别名，这就是该功能的名称和语法来源）。但 `obj.payload` 是对 `obj` 字段的直接访问，并且是一个右值。该值绑定到 `sneaky` 的 `ref` 参数，因此允许直接覆盖 `v` 的字段。

为了修复这个问题，我们需要将对象别名为一个右值。这样我们就获得了完整的功能，但存储返回右值的引用是无法触碰的。使用一个按值返回 `payload` 的 `@property` 来绑定到右值非常简单：

```rust
struct Final!T {
    private T payload;
    this(T) bindTo() {
        payload = bindTo;
    }
    // 禁用赋值
    @disable void opAssign(Final);
    // 子类 T，允许重绑定
    @property T get() { return payload; }
    alias this;
}
```

```d
import std.stdio;
```

```d
struct A {
    char a;
    int b;
    char c;
}
```

```d
void main() {
    A x;
    writeln("%s %s %s", x.a.offsetof, x.b.offsetof, x.c.offsetof);
}
```

参考实现输出了 0 4 8，揭示了上一页图 7.2 中的的布局。你需要创建一个 `A` 类型的对象来访问它的某些静态信息，这显得有点别扭，而且 `A.a.offsetof` 语法无法编译。然而，可以使用的一个技巧是使用 `A.init.offsetof`，这足以获取与每个成员相关的偏移量并作为编译时常量。

```d
import std.stdio;
```

```d
struct A {
    char a;
    int b;
    char c;
}
```

```d
void main() {
    // 无需对象访问字段偏移
    writeln("%s %s %s", A.init.offsetof, A.init.b.offsetof, A.init.c.offsetof);
}
```

D 保证所有的填充字节都会一致地填充为零。

## 7.11.1 align 属性

如果你想覆盖编译器对对齐的选择（这会影响插入的填充字节），你可以在字段声明中使用 `align` 修饰符。当你想要与指定了特定对齐的硬件或二进制协议交互时，可能会出现这种需求。以下是 `align` 指定符的样式：

```d
class A {
```

## 7.11 structs

```d
char a;
align(1) int b;
char c;
```

根据上面的规范，A 的字段布局之间没有间隔。（在对象末尾可能会有一个间隔。）`align` 的参数是字段的最大对齐方式，因此有效对齐可能不会超过字段类型的自然对齐。要获取类型 `T` 的自然对齐，请使用编译器定义的属性 `T.alignof`。因此，如果你你指定 `align(200)` 而不是 `align(1)`，得到的有效对齐是 4，与 `int.alignof` 相同。

你可以在整个类定义中使用 `align`：

```d
align(1) struct A {
char a;
int b;
char c;
```

在指定 `struct` 时，`align` 将默认对齐设置为特定值。你可以通过 `struct` 定义内部的单个 `align` 属性来覆盖它。如果你对类型为 `T` 的字段仅指定不带数字的 `align`，它被视为 `align(T.alignof)`——换句话说，它将该字段的对齐重置为自然对齐。

`align` 不应该用于指针和引用。垃圾回收器假设所有引用和指针都对齐到大小 `t`。编译器不强制执行这一限制，因为通常你可能有不被垃圾回收的指针和引用。因此，这种定义是非常危险的，因为它可以无错编译。

```d
struct Node {
short value;
align(2) Node* next; // 避免
```

如果上述代码 `obj.next = new Node`（即为 `obj.next` 填充一个可垃圾回收的引用），那么混乱不可避免：未对齐的引用将逃过垃圾回收器的检测，内存会被回收，而 `obj.next` 将变成一个悬空引用。

## 7.2 unions

D 也接受 C 风格的联合（union），但应该提到，它们应该极少使用并要极其小心。

`union` 类似于 `struct`，其中所有成员从相同的地址开始。这使得它们的存储重叠，这意味着作为 `union` 的用户，你有责任始终读取你写入的精确类型。在任何给定时刻，`union` 值中只有一个成员是有效的。

```d
union IntOrFloat {
  int _int;
  float _float;
}
unittest() {
  IntOrFloat iof;
  iof._int = 5;
  // 只读取 iof._int，不读取 iof._float
  assert(iof._int == 5);
  iof._float = 5.5;
  // 只读取 iof._float，不读取 iof._int
  assert(iof._float == 5.5);
}
```

由于 `int` 和 `float` 的大小相同（4 字节），它们在 `IntOrFloat` 内部会精确重叠。然而，它们的布局细节并未指定——例如，`int` 和 `float` 可能会使用不同的字节序：`_int` 的最高字节可能位于最低地址，而 `_float` 的最高字节（包含符号位指数的字节）可能位于最高地址。

`union` 不是带标记的（tagged），这意味着 `union` 对象本身不包含一个“标记”来指示哪个成员是正确的。正确性的责任完全落在用户的肩上，这使得 `union` 成为构建任何类型大型抽象的一种并不愉手段。

在未进行初始化的情况下定义，`union` 对象的第一个字段用其 `.init` 值初始化，因此在构造后第一个成员是可读的。要用 `.init` 以外的值初始化第一个字段，请在括号中指定初始化器：

```d
unittest() {
  IntOrFloat iof = { 5 };
  assert(iof._int == 5);
}
```

静态 `union` 对象可以使用以下语法初始化另一个字段：

```d
unittest() {
    static IntOrFloat iof = { 5 };
    assert(iof._float == 5);
}
```

正因如此，许多 `union` 的用户实际上将其作为标记联合（tagged union），例如所示：

```d
unittest {
    IntOrFloat iof;
    iof._float = 1;
    assert(iof._float == 1);
}
```

上面的示例是 `union` 的经典用法，用于定义所谓的判别联合、标记联合或代数类型。`TaggedUnion` 封装了一个不安全的 `union`，在一个安全的盒子里并跟踪最后赋值的值。

## 7.3 枚举值

那些只能取少数离散值的类型被证明非常有用——事实上，它们如此有用，以至于 Java 在多年努力尝试用一种惯用法模拟它们 [8] 之后，最终将枚举添加到核心语言中。定义良好的枚举也不容易——`enum` 在 C++ 和（特别是 C）中有很多奇之处。D 试图利用后见之明的优势来定义一种简单且实用的枚举功能。

让我们从开始。`enum` 最简单的用法是“让我列举符号值”，而不与新类型关联：

```d
enum
```

## 7.3. 枚举值

```d
mega = 1024 * 1024,
pi = 3.14,
euler = 2.72,
greet = "Hello";
```

枚举的类型推导规则与 `auto` 相同，因此在示例中 `pi` 和 `euler` 的类型为 `double`，`greet` 的类型为 `string`。如果你想定义一个或多个特定类型的枚举，可以在 `enum` 关键字之后指定类型：

```d
enum float verySmall = 0.0001, veryBig = 10000;
enum dstring wideMsg = "Wide load";
```

枚举值是常量；使用它们本质等同于使用字面量。特别是，支持的操作是相同的——例如，你不能取 `pi` 的地址，就像不能取 `3.14` 的地址一样：

```d
auto x = pi;               // OK，x 类型为 double
auto y = pi * euler;     // OK，y 类型为 double
euler = 2.73;             // 错误！
                          // 不能修改枚举值！
```

```d
void f(double x) {
...
}
fun(pi);                  // 错误！
                          // 不能取 3.14 的地址！
```

如所示，枚举值的类型不仅限于 `int`，还涵盖 `double` 和 `string`。哪些类型可以用于 `enum`？答案很简单：任何原始类型和 `struct` 类型都可以可用于 `enum`。枚举值初始化器只有两个要求：

- 初始化器必须在编译期间是可计算的。
- 初始化器的类型必须允许拷贝，即不是 `@disable this(§ 7.1.3.4)`。

第一个要求确保枚举值不依赖于任何运行时参数。第二个要求确保你实际上可以创建该值的副本；每当你使用枚举时都会创建一个副本。
你不能定义类类型的枚举值，因为类对象总是通过 `new` 创建的（除了无趣的空值外），而 `new` 在编译期间是不可计算的。如果未来这一限制被解除或放宽，也不意外。

让我们创建一个并使用一个结构体类型的枚举：

```d
struct Color {
  ubyte r, g, b;
}
```

```d
enum
  red = Color(255, 0, 0),
  green = Color(0, 255, 0),
  blue = Color(0, 0, 255);
```

每当你使用时，例如，代码的行为就像你粘贴了 `Color(0, 255, 0)` 而不是符号名称。

### 7.3.1 枚举类型

你可以为一组枚举值赋予一个命名的类型以：

```d
enum OddWord { acini, alembicated, prolegomena, aprosexia }
```

一旦为一组枚举分配了名称，它们就不可以是不同的类型：所有必须共享相同的类型，因为集合的用户随后可能会定义并使用该类型的值。例如：

```d
OddWord w;
assert(w == OddWord.acini); // 默认初始化器
// 是集合中的第一个值：acini
w = OddWord.aprosexia; // 始终使用类型名来限定
// 值名
// （顺便说一下，这不是你想象的）
int x = w; // OddWord 可以转换为 int
// 但反之不然
assert(x == 3); // 值标记为 0, 1, 2, ...
```

命名枚举的类型是自动推导的。分配不同的类型如下所示：

```d
enum OddWord : byte { acini, alembicated, prolegomena, aprosexia }
```

使用新定义（`byte` 称为 `OddWord` 的基类型），枚举符号具有相同的值，只是存储方式不同。你也可以将类型设置为 `double` 或 `real`，而赋予符号的值仍然是 0、1 等等。但如果你将 `OddWord` 的基类型设置为非数值类型（如 `string`），则你必须为所有变量指定初始化器，因为编译器没有自然的后续顺序可以遵循。

## 7.3. 枚举值

回到数值枚举，如果你为任何值分配一个特定值，这将重置枚举使用的内部步计数器。例如：

```d
enum E { a = 10, b, c = 20, d }
```

在这种情况下，`a` 是 10，`b` 是 11，`c` 是 20，`d` 是 21。如果你为成员指定一个值，计数器将重置为该值：

```d
enum E { a = 10, b, c = 20, d }
```

在这种情况下，`a` 是 10，`b` 是 11，`c` 是 20，`d` 是 21。如果你为多个成员指定值，计数器会为每个成员重置一次：

```d
enum E { a = 10, b = 20, c = 30, d }
```

在这种情况下，`a` 是 10，`b` 是 20，`c` 是 30，`d` 是 31。

你也可以为你的枚举成员使用负值：

```d
enum E { a = -10, b, c = -20, d }
```

在这种情况下，`a` 是 -10，`b` 是 -9，`c` 是 -20，`d` 是 -19。

枚举的值可以用任何任何允许基类型的表达式中：

```d
enum E { a = 10, b }
int x = E.a;
int y = E.b + E.a;
```

你还可以将枚举成员作为 `switch` 语句中的 `case` 情况：

```d
enum E { a, b, c }
E e = E.b;
switch (e) {
  case E.a:
    break;
  case E.b:
    break;
  case E.c:
    break;
}
```

枚举值的类型不仅限于 `int`，还涵盖 `double` 和 `string`。哪些类型可以用于 `enum`？答案很简单：任何原始类型和 `struct` 类型都可以可用于 `enum`。枚举值初始化器只有两个要求：

- 初始化器必须在编译期间是可计算的。
- 初始化器的类型必须允许拷贝，即不是 `@disable this(§ 7.1.3.4)`。

第一个要求确保枚举值不依赖于任何运行时参数。第二个要求确保你实际上可以创建该值的副本；每当你使用枚举时都会创建一个副本。
你不能定义类类型的枚举值，因为类对象总是通过 `new` 创建的（除了无趣的空值外），而 `new` 在编译期间是不可计算的。如果未来这一限制被解除或放宽，也不意外。

让我们创建一个并使用一个结构体类型的枚举：

```d
struct Color {
  ubyte r, g, b;
}
```

```d
enum
  red = Color(255, 0, 0),
  green = Color(0, 255, 0),
  blue = Color(0, 0, 255);
```

每当你使用时，例如，代码的行为就像你粘贴了 `Color(0, 255, 0)` 而不是符号名称。

### 7.3.1 枚举类型

你可以为一组枚举值赋予一个命名的类型以：

```d
enum OddWord { acini, alembicated, prolegomena, aprosexia }
```

一旦为一组枚举分配了名称，它们就不可以是不同的类型：所有必须共享相同的类型，因为集合的用户随后可能会定义并使用该类型的值。例如：

```d
OddWord w;
```
