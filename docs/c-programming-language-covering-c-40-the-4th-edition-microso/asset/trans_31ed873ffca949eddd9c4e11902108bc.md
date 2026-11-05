

indexer-declaration:
    attributes_opt indexer-modifiers_opt indexer-declarator { accessor-declarations }

indexer-modifiers:
    indexer-modifier
    indexer-modifiers indexer-modifier

indexer-modifier:
    new
    public
    protected
    internal
    private
    virtual
    sealed
    override
    abstract
    extern

indexer-declarator:
    type this [ formal-parameter-list ]
    type interface-type . this [ formal-parameter-list ]

索引器声明可以包含一组特性（§17）、四个访问修饰符的有效组合（§10.3.5），以及 new（§10.3.4）、virtual（§10.6.3）、override（§10.6.4）、sealed（§10.6.5）、abstract（§10.6.6）和 extern（§10.6.7）修饰符。

索引器声明在修饰符的有效组合方面遵循与方法声明（§10.6）相同的规则，唯一例外是索引器声明中不允许使用 static 修饰符。

修饰符 virtual、override 和 abstract 互斥，但有一种情况例外。abstract 和 override 修饰符可以一起使用，以便抽象索引器可以重写虚拟索引器。

索引器声明的类型指定该声明所引入索引器的元素类型。除非索引器是显式接口成员实现，否则类型后面跟关键字 this。对于显式接口成员实现，类型后面跟一个接口类型、一个“.”以及关键字 this。与其他成员不同，索引器没有用户定义的名称。

形参列表指定索引器的参数。索引器的形参列表与方法（§10.6.1）的形参列表对应，但必须至少指定一个参数，并且不允许使用 ref 和 out 参数修饰符。

索引器的*类型*以及*形参列表*中引用的每个类型，其可访问性必须至少与索引器本身相同（§3.5.4）。

*访问器声明*（§10.7.2）必须括在“{”和“}”标记中，它们声明索引器的访问器。访问器指定与读取和写入索引器元素相关联的可执行语句。

尽管访问索引器元素的语法与访问数组元素的语法相同，但索引器元素不被归类为变量。因此，不能将索引器元素作为 `ref` 或 `out` 实参传递。

索引器的形参列表定义索引器的签名（§3.6）。具体而言，索引器的签名由其形参的数量和类型组成。元素类型和形参名称不属于索引器签名的一部分。

索引器的签名必须不同于同一类中声明的所有其他索引器的签名。

索引器和属性在概念上非常相似，但有以下不同之处：

- 属性由其名称标识，而索引器由其签名标识。
- 属性通过*简单名*（§7.6.2）或*成员访问*（§7.6.4）访问，而索引器元素通过*元素访问*（§7.6.6.2）访问。
- 属性可以是 `static` 成员，而索引器始终是实例成员。
- 属性的 get 访问器对应于无参数的方法，而索引器的 get 访问器对应于与索引器具有相同形参列表的方法。
- 属性的 set 访问器对应于带有一个名为 `value` 的参数的方法，而索引器的 set 访问器对应于与索引器具有相同形参列表的方法，再加上一个名为 `value` 的附加参数。
- 索引器访问器声明与索引器参数同名的局部变量属于编译时错误。
- 在重写属性声明中，使用语法 `base.P` 访问继承的属性，其中 `P` 是属性名。在重写索引器声明中，使用语法 `base[E]` 访问继承的索引器，其中 `E` 是以逗号分隔的表达式列表。

除这些差异外，§10.7.2 和 §10.7.3 中定义的所有规则既适用于属性访问器，也适用于索引器访问器。

> > **JON SKEET** 我觉得很奇怪：事件可以是 static（但几乎从不如此），而索引器却不可以。例如，Encoding.GetEncoding(string) 若作为静态索引器存在，也许是有意义的。实际上，我期望静态索引器主要充当其声明类型的工厂成员。在大多数地方，方法完全足以作为替代方案，但禁止静态索引器有点奇怪。

当索引器声明包含 extern 修饰符时，该索引器称为外部索引器。由于外部索引器声明不提供实际实现，其每个访问器声明都由一个分号组成。

下面的示例声明一个 BitArray 类，该类实现一个用于访问位数组中各个位的索引器。

```csharp
using System;
class BitArray
{
    int[] bits;
    int length;

    public BitArray(int length) {
        if (length < 0) throw new ArgumentException();
        bits = new int[((length - 1) >> 5) + 1];
        this.length = length;
    }

    public int Length {
        get { return length; }
    }

    public bool this[int index] {
        get {
            if (index < 0 || index >= length) {
                throw new IndexOutOfRangeException();
            }
            return (bits[index >> 5] & (1 << (index & 31))) != 0;
        }
        set {
            if (index < 0 || index >= length) {
                throw new IndexOutOfRangeException();
            }
            if (value) {
                bits[index >> 5] |= 1 << (index & 31);
            }
            else {
                bits[index >> 5] &= ~(1 << (index & 31));
            }
        }
    }
}
```

BitArray 类的实例消耗的内存远少于相应的 bool[]（因为前者的每个值只占一位，而不是后者的一个字节），但它允许与 bool[] 相同的操作。

下面的 CountPrimes 类使用 BitArray 和经典的“筛法”算法计算 1 与给定最大值之间的素数个数：

```csharp
class CountPrimes
{
    static int Count(int max) {
        BitArray flags = new BitArray(max + 1);
        int count = 1;
        for (int i = 2; i <= max; i++) {
            if (!flags[i]) {
                for (int j = i * 2; j <= max; j += i) flags[j] = true;
                count++;
            }
        }
        return count;
    }

    static void Main(string[] args) {
        int max = int.Parse(args[0]);
        int count = Count(max);
        Console.WriteLine("Found {0} primes between 1 and {1}", count, max);
    }
}
```

请注意，访问 BitArray 元素的语法与访问 bool[] 的语法完全相同。

下面的示例展示一个 26 × 10 的网格类，它有一个带两个参数的索引器。第一个参数必须是 A–Z 范围内的大写或小写字母，第二个参数必须是 0–9 范围内的整数。

```csharp
using System;

class Grid
{
    const int NumRows = 26;
    const int NumCols = 10;

    int[,] cells = new int[NumRows, NumCols];

    public int this[char c, int col] {
        get {
            c = Char.ToUpper(c);
            if (c < 'A' || c > 'Z') {
                throw new ArgumentException();
            }
            if (col < 0 || col >= NumCols) {
                throw new IndexOutOfRangeException();
            }
            return cells[c - 'A', col];
        }
        set {
            c = Char.ToUpper(c);
            if (c < 'A' || c > 'Z') {
                throw new ArgumentException();
            }
            if (col < 0 || col >= NumCols) {
                throw new IndexOutOfRangeException();
            }
            cells[c - 'A', col] = value;
        }
    }
}
```

## 10.9.1 索引器重载

索引器重载解析规则在 §7.5.2 中描述。

## 10.10 运算符

*运算符*是一种成员，它定义可应用于类实例的表达式运算符的含义。运算符使用*运算符声明*来声明：

*operator-declaration:*
    *attributes*ₒₚₜ *operator-modifiers* *operator-declarator* *operator-body*

*operator-modifiers:*
    *operator-modifier*
    *operator-modifiers* *operator-modifier*

*operator-modifier:*
    public
    static
    extern

*operator-declarator:*
    *unary-operator-declarator*
    *binary-operator-declarator*
    *conversion-operator-declarator*

