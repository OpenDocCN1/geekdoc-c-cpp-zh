

我们将这种类型命名为 IntBits。IntBits 将包含一个 `int` 值（在构造函数中初始化），但其核心思想是将 IntBits 作为 `bool` 变量数组来使用。

> 提示
> IntBits 类型很小且轻量，因此将其创建为结构（struct）而不是类（class）是合理的。

点击此处查看代码

```
struct IntBits
{
    private int bits;
    // 简单的构造函数，实现为表达式体方法
    public IntBits(int initialBitValue) => bits = initialBitValue;
    // 在此处编写索引器
}
```

要定义索引器，你使用一种介介于属性和数组之间的语法。你通过 `this` 关键字引入索引器，指定索引器返回的值的类型，并在方括号之间指定作为索引器索引的值的类型。IntBits 结构体的索引器使用整数作为索引类型，并返回一个布尔值。它看起来如下：

点击此处查看代码

```
struct IntBits
{
    ...
    public bool this [ int index ]
{
        get => (bits & (1 << index)) != 0;
        set
{
          if (value) // 如果 value 为 true 则开启位；
          否则，将其关闭
            bits |= (1 << index);
          else
            bits &= ~(1 << index);
        }
}
}
```

注意以下几点：

- 索引器不是方法。它没有包含参数的括号，但有指定索引的方括号。此索引用于指定正在访问哪个元素。

- 所有索引器都使用 `this` 关键字。一个类或结构最多定义一个索引器（尽管你可以对其进行重载并有多个实现），但它的名称始终为 `this`。

- 索引器像属性一样包含 `get` 和 `set` 访问器。在本文示例中，`get` 和 `set` 访问器包含了之前讨论过的复杂位运算表达式。

- 索引器声明中指定的索引在调用索引器时会被填充。`get` 和 `set` 访问器方法可以读取此参数以确定应该访问哪个元素。

> 注意
> 你应该对索引器中的索引值进行范围检查，以防止你的索引器代码中发生任何意外异常。

提供一种显示此结构中数据的方法也是一种良好的做法。你可以通过重写 `ToString` 方法并将结构中持有的值转换为包含二进制表示的字符串来实现，如下：

点击此处查看代码

```
struct IntBits
{
    ...
    public override string ToString()
    {
        return Convert.ToString(bits, 2);
    }
}
```

创建索引器后，你可以使用 `IntBits` 类型的变量代替 `int`，并应用方括号符号，如下一个示例所示：

点击此处查看代码

```
int adapted = 0b0_01111110;
IntBits bits = new IntBits(adapted);
bool peek = bits[6]; // 获取索引 6 处的 bool；peek 应该是 true (1)
bits[0] = true; // 将索引 0 处的位设置为 true (1)
bits[3] = false; // 将索引 3 处的位设为 false (0)
Console.WriteLine($"{bits}"); // 显示 1110111 (0b0_01110111)
```

这种语法更容易理解。它直接且简洁地捕捉了问题的本质。

# 理解索引器访问

当你读取索引器时，编译器会自动将你的类数组形式的代码翻译为对该索引器 `get` 访问器的调用。考虑以下示例：

```
bool peek = bits[6];
```

该语句被转换为对 `bits` 的 `get` 访问器的调用，并且索引参数被设置为 6。

同样，如果你向索引器写入内容，编译器会自动将你的类数组形式的代码翻译为对该索引器 `set` 访问器的调用，并将索引参数设置为方括号内的值，如下所示：

```
bits[3] = true;
```

该语句被转换为对 `bits` 的 `set` 访问器的调用，其中 `index` 为 3。与普通属性一样，你写入索引器的数据（在本例中为 `true`）将通过 `value` 关键字在 `set` 访问器内部可用。`value` 的类型与索引器本身的类型相同（在本例中为 `bool`）。

在组合读写上下文中也可以使用索引器。在这种情况下，`get` 和 `set` 访问器都会被使用。查看以下语句，它使用异或运算符 (`^`) 反转 `bits` 变量中索引 6 处位的值：

```
bits[6] ^= true;
```

这段代码被自动翻译为：

```
bits[6] = bits[6] ^ true;
```

这段代码之所以有效，是因为索引器同时声明了 `get` 和 `set` 访问器。

> 注意
> 你可以声明只包含 `get` 访问器（只读索引器）或只包含 `set` 访问器（只写索引器）的索引器。

# 索引器与数组

当你使用索引器时，语法刻意设计得很像数组。然而，索引器和数组之间存在一些重要的区别：

- 索引器可以使用数字下标，例如字符串（如下例示例所示），而数组只能使用整数下标。

点击此处查看代码

```
public int this [ string name ] { ... } // OK
```

- 索引器可以重载（就像方法一样），而数组不能。

点击此处查看代码

```
public Name this [ PhoneNumber number ] { ... }
public PhoneNumber this [ Name name ] { ... }
```

- 索引器不能用 `ref` 或 `out` 参数，而数组元素可以。

点击此处查看代码

```
IntBits bits; // bits 包含一个索引器
Method(ref bits[1]); // 编译错误
```

# 属性、数组和索引器

属性可以返回数组，但请记住数组是引用类型，将数组暴露为属性会产生意外覆盖大量数据的可能性。查看以下暴露了名为 `Data` 的数组属性的结构：

点击此处查看代码

```
struct Wrapper {
    private int[] data;
    ...
    public int[] Data
    {
        get => this.data;
        set => this.data = value;
    }
}
```

现在考虑使用该属性的以下代码：

点击此处查看代码

```
Wrapper wrap = new Wrapper();
...
int[] myData = wrap.Data;
myData[0]++;
myData[1]++;
```

这个序列看起来很无害。但由于数组是引用类型，`myData` 指向与 `data` 变量相同的对象。你对 `myData` 元素所任何更改都作用于 `data` 数组；`myData[0]++` 的效果与 `data[0]++` 完全相同。

如果这不是你的意图，你应该在 `Data` 属性的 `get` 和 `set` 中使用 `Clone` 方法返回数组的副本，或对设置的值进行拷贝，如下所示。（第8章“理解值和引用”讨论了 `Clone` 方法）。注意 `Clone` 方法返回一个 `object`，你必须将其转换为整数数组。

点击此处查看代码

```
struct Wrapper {
    private int[] data;
    ...
    public int[] Data
    {
        get { return this.data.Clone() as int[]; }
        set { this.data = value.Clone() as int[]; }
    }
}
```

这种方法可能会变得混乱且浪费内存。也就是说，不要将整个数组暴露为属性；只需通过索引器公开其单个元素：

点击此处查看代码

```
struct Wrapper {
    private int[] data;
    ...
    public int this[int i]
    {
        get => this.data[i];
        set => this.data[i] = value;
    }
}
```

```
interface IRawInt
{
  bool this { int index } { get; set; }
}
struct RawInt : IRawInt
{
  ...
  public bool this [ int index ]
  {
    get { ... }
    set { ... }
  }
}
```

如果你在类中实现接口索引器，可以将索引器实现声明为 `virtual`。这允许进一步的派生类重写 `get` 和 `set` 访问器，如下所示：

点击此处查看代码

```
class RawInt : IRawInt
{
    public virtual bool this { int index }
    {
        get { ... }
        set { ... }
    }
}
```

你也可以通过第13章“创建接口和定义抽象类”涵盖的显式接口语法来实现索引器。索引器的显式实现是非公共的且非虚拟的（因此无法重写），如示例所示：

```
struct RawInt : IRawInt
{
    bool IRawInt.this { int index }
    {
        get { ... }
        set { ... }
    }
...}
```

# 在 Windows 应用程序中使用索引器

