
上述程序打印

first object checking in.
object 0 checking in.
object 0 checking out.
object 1 checking in.
object 1 checking out.
object 2 checking in.
object 2 checking out.
last object checking in.
last object checking out.
first object checking out.

如预期，第一个创建的对象是最后一个被析构的对象。循环在每次通过时退出作用域。你可以通过调用 `clear(obj)` 显式调用 struct 对象的析构函数。我们在 187 页了解过 `clear` 函数。对于类对象，`clear` 用于将其重置为状态。对于 struct 对象，`clear` 调用析构函数然后拷贝对象的位。结果是一个有效的对象，不持有任何状态。

## 7.1.4 静态构造函数与析构函数

struct 可以定义任意数量的静态构造函数和析构函数。这一功能与第 188 页 6.3 为类引入的功能完全相同。

```d
import std.stdio;

struct A {

    static ~this() {

        writeln("First static destructor");

    }

    ...

    static this() {

        writeln("First static constructor");

    }

    ...

    static this() {

        writeln("Second static constructor");

    }

    ...

    static ~this() {

        writeln("Second static destructor");

    }

}

void main() {

    writeln("This is speaking");

}
```

静态构造函数和析构函数之间不需要配。在评估 `main` 之前，运行时支持按照定义的顺序执行所有静态构造函数。`main` 结束后，运行时支持按照定义的相反顺序执行所有析构函数。上述程序写入

First static constructor
Second static constructor
This is speaking
Second static destructor
First static destructor

模块内部静态构造函数和析构函数的执行顺序是有定义的（如上），但跨模块并不总是如此。跨模块的静态构造函数和析构函数的执行顺序定义在第 189 页。

## 7.1.5 方法

struct 定义成员函数。由于 struct 没有继承和重写，struct 方法比普通函数简单。

对于 struct 类型 `S`，非静态方法通过引用获取隐藏参数（相当于 `ref S`）。在方法内部，名称查找过程与类相同：参数隐藏成员名，成员名隐藏模块级名称。

```d
void fun(int x) {

  assert(x != 0);

}

// 演示名称查找

struct S {

  int x = 1;

  static int y = 324;

  void fun(int x) {

    assert(x == 0); // 获取参数 x

    assert(this.x == 1); // 获取成员 x

  }

  void gun() {

    fun(0); // 调用方法 fun

    fun(1); // 调用模块级 fun

  }

}

// unittest 可以是 struct成员

unittest {

  S obj;

  obj.gun();

  assert(y == 324); // “成员” unittest 查看静态数据

}
```

上面还展示了在 struct 内部定义的 unittest。这种 unittest 没有特殊状态，但插入到每个方法定义之后非常方便。成员 unittest 内部的代码享有与普通方法相同的可见性——例如，上面的 unittest 不需要像静态方法那样为静态成员以前缀 `S`。有几个特殊的值得进一步研究。它们是用于 `=` 的运算符 `opAssign`，用于 `==` 和 `!=` 的相等运算符 `=`；以及用于 `<`, `>=` 的排序运算符 `=`。这个主题实际上属于第 12 章，因为它涉及运算符重载，但这些运算符是特殊的，因为编译器可能会带有特定的行为自动生成它们。

## 7.15.1 赋值运算符

默认情况下，如果你说

```d
Widget { ... } // 定义如第 25 页 § 7.1.3.4

Widget w1, w2;

...

w1 = w2;
```

那么赋值是按成员完成的。这可能会给第 25 页 § 7.1.3.4 中讨论的 `Widget` 类型带来麻烦。记得 `Widget` 持有一个指向字段成员的指针，该字段应该是每个 `Widget` 对象独立的。将 `w2` 赋值给 `w1` 字段是将 `w2.array` 赋值给 `w1.array`——只是简单的数组边界赋值，而没有实际数组内容。这需要修复，因为我们需要的是拷贝源 Widget 中的数组并赋值给目标-Widget。

用户代码可以通过定义方法 `opAssign` 来拦截赋值。本质上，如果 `rhs` 定义了签名兼容的 `opAssign`，赋值 `rhs` 将被转换为 `lhs.opAssign(rhs)`（否则，如果 lhs 和 rhs 类型相同，则执行默认的逐字段赋值）。让我们定义 `Widget.opAssign`：

```d
Widget {

  private int[] array;

  .. // this(uint), this(this), 等

  ref Widget opAssign(ref Widget rhs) {

    array = rhs.array.dup;

    return this;

  }

}
```

## 7.1. 结构

赋值运算符返回 `this` 的引用以允许链式赋值 `$w1 = w2 = w3$`，编译器将其重写为 `$w1.opAssign(w2.opAssign(w3))$`。仍然存在一个问题。考虑赋值：

```d
Widget w;

...

w = Widget(50); // 错误！// 无法将 Widget 类型的右值绑定到 ref Widget
```

问题在于定义的 `opAssign` 需要一个 `ref Widget`，即 Widget 类型的左值。为了接受从右值到左值的赋值，`Widget` 必须定义两个赋值运算符：

```d
import std.algorithm;

struct Widget {

  private int[] array;

  ... // this(uint), this(this), 等。

  ref Widget opAssign(ref Widget rhs) {

    array = rhs.array.dup;

    return this;

  }

  ref Widget opAssign(Widget rhs) {

    swap(array, rhs.array);

    return this;

  }

}
```

接收右值的版本中没有 `.dup`。为什么？因为该右值（带有数组）实际上由第二个 `opAssign` 拥有；它在进入函数之前被复制，并在函数返回之前被销毁。这意味着不需要复制 `rhs.array`，因为没有人会需要它。将 `rhs.array` 与 `this` 交换即可。当 `opAssign` 返回时，`rhs` 随着旧数组消失，而 `this` 保留了 `rhs` 的旧数组——状态的完美保存。我们可以完全移除 `opAssign` 的第一个重载：按值接收 `rhs` 的版本处理一切（左值会自动转换为右值）。但保留左值版本可以实现一种实用的优化：`opAssign` 不需要复制源，而是检查当前数组是否有空间容纳新内容，在这种情况下，直接覆盖即可。

```d
// Widget 内部 ...

ref Widget opAssign(ref Widget rhs) {

  if (array.length < rhs.array.length) {

    array = rhs.array.dup;

  } else {

    // 调整长度

    array.length = rhs.array.length;

    // 复制内容（第100页的 4.1.7）

    array[] = rhs.array;

  }

  return this;

}
```

### 7.1.5.2. 结构体的相等性

结构体对象可以使用 `==` 和 `!=` 进行相等性比较。比较通过成员进行，如果比较对象的至少两个对应成员不相等，则返回 false，否则返回 true。

```d
struct Point {

  int x, y;

}

unittest {

  Point a, b;

  assert(a == b);

  a.x = 1;

  assert(a != b);

}
```

要定义自定义比较程序，请定义 `opEquals` 方法：

```d
import std.math, std.stdio;

struct Point {

  float x = 0, y = 0;

  // 添加

  bool opEquals(ref const Point rhs) const {

    // 执行近似比较

    return approxEqual(x, rhs.x) && approxEqual(y, rhs.y);

  }

}
```

```d
unittest {

  Point a, b;

}
```

```d
assert(a == b);
a.x = 1e-8;
assert(a == b);
a.y = 1e-1;
assert(a != b);
```

与类的 `opEquals`（第 205 页的 6.8.3）相比，结构体的 `opEquals` 要简单得多，因为不需要担心继承存在时的正确性。编译器将结构对象的比较重写为对 `opEquals` 的调用。当然，结构体仍然必须定义有意义的 `opEquals`：自反射、、性和传递性。必须说，尽管 `opEquals` 看起来很大，但它未能通过传递性测试。更好的测试是比较截断到最高有效位的两个 `Point`；该测试可以更容易转换。

当结构体包含定义了 `opEquals` 的成员但自身没有定义 `opEquals` 时，比较仍然会调用其定义成员的 `opEquals`。继续 `Point` 示例：

```d
struct Rectangle {

  Point leftBottom, rightTop;

}
```

```d
unittest {

  Rectangle a, b;

  assert(a.leftBottom.x == 1e-8);

  assert(a == b);

  a.rightTop.y = 5;

  assert(a != b);

}
```

给定两个 `Rectangle` `$a$` 和 `$b$`，评估 `a == b` 等同于评估：

```d
a.leftBottom == b.leftBottom && a.rightTop == b.rightTop
```

这又被重写为：

```d
a.leftBottom.opEquals(b.leftBottom) &&
a.rightTop.opEquals(b.rightTop)
```

示例还揭示了比较按字段声明顺序进行的（即 `leftBottom` 在 `rightTop` 之前），如果两个字段不相等，则提前停止，由于 `&&` 的短路求值。

## 7.1.6 静态成员

结构体可以定义静态数据和静态成员函数。考虑到作用域可见性和访问规则（第 100 页的 7.1.7），静态成员函数与普通函数具有相同的机制。没有隐藏的 `this` 参数，也没有调用其他机制。

同样，静态数据成员有...（实际上，提供的文本有跳转。让我们严格遵循提供的文本顺序）。

### 7.1.7 访问修饰符

结构类型...与类相同。在这里，让我们总结每个修饰符的含义：

```d
struct S {

    // 内部访问

    private int a;      // S 内部访问

    package int b;      // 从应用程序访问

    public int c;      // 应用程序外部

    export int d;       // 应用

}
```

### 7.1.8 嵌套结构体和类

通常，结构体内部定义结构体或类是方便的。例如，树容器可能选择暴露一个简单接口的结构体，但在内部使用多态来定义节点。

```d
struct Tree {

  private:

    class Node {

        int value;

        abstract Node left();

        abstract Node right();

    }

    class NonLeaf : Node {

        Node _left, _right;

        override Node left() { return _left; }

        override Node right() { return _right; }

    }

    class Leaf : Node {

        override Node left() { return null; }

        override Node right() { return null; }

    }

    // 数据

    Node root;

}
```

### 7.1.9 在函数内部嵌套结构体

回想第 223 页的 6.11.1，嵌套类享有特殊的属性。嵌套类可以访问闭包参数。如果你返回一个嵌套类对象，编译器甚至创建一个动态分配的函数帧，函数的局部变量和参数在函数结束时仍然存在。

为了符合性和一致性，D 为嵌套在函数中的结构体提供了类似的便利。嵌套结构体可以访问闭包函数的参数和局部变量：

```d
void fun(int a) {

    int b;

    struct Local {

        int c;

        int sum(){

            // 访问参数、变量以及 Local 自身的成员

            return a + b + c;

        }

    }

    Local obj;

    int x = obj.sum();

    assert(Local.size() == 2 * size_t());

}
```

```d
unittest {

    fun(5);

}
```

嵌套结构体嵌入了魔法的“帧指针”，这允许它们访问上述示例中的外部值（如 a 和 b）。由于存在额外的状态，`Local` 对象的尺寸为 4，而不是人们可能预期的那样（在 32 位机器上），这是为了给帧指针留空间。如果你想定义一个没有负担的嵌套结构体，可以在 `Local` 的定义中在 struct 前加上 `static`，这使得 `Local` 成为一个普通的结构体并防止它访问 a 和 b。

除了与嵌套类相比可以避免不必要的限制外，嵌套结构体的用处并不大。嵌套对象无法从函数返回，因为调用者无法访问它们的类型。如果一个设计需要复杂的嵌套结构体，它隐含地助长了复杂的函数，而这些函数从一开始就应该被避免。

### 7.1.10 结构体的子类型。@disable 属性

虽然结构体不支持继承和多态，但它们仍然支持 `alias this` 功能，该功能首次在第 230 页的 § 6.13 中引入。通过使用 `alias this`，你可以让结构体成为任何其他类型的子类型。例如，让我们定义一个名为 Final 的简单类型，它的行为非常像类引用——除了你永远无法重新绑定它！这里有一个使用 `Final` 的示例：

```d
import std.stdio;

class Widget {

    void print() {

        writeln("Hi, I'm a Widget. Well, that's about it.");

    }

}
```

```d
unittest {

    auto a = Final!Widget(new Widget);

    a.print();               // 正常，只需打印 a

    auto b = a;             // 正常，且 b 和 a 绑定到同一个 Widget

    a = b;                 // 错误！

                            // opAssign(Final!Widget) 已禁用；

    a = new Widget;      // 错误！

                                // 无法向 get(!) 返回的右值赋值

}
```
