
```csharp
        else
        {
            bits[index >> 5] &= ~(1 << index);
        }
    }
}
```

`BitArray` 类的实例消耗的内存远少于相应的 `bool[]`（因为前者的每个值只占用一位，而不是后者的一个字节），但它允许与 `bool[]` 相同的操作。

以下 `CountPrimes` 类使用 `BitArray` 和经典的“筛法”算法来计算 2 到给定最大值之间的素数个数：

```csharp
class CountPrimes
{
    static int Count(int max)
    {
        BitArray flags = new BitArray(max + 1);
        int count = 0;
        for (int i = 2; i <= max; i++)
        {
            if (!flags[i])
            {
                for (int j = i * 2; j <= max; j += i)
                {
                    flags[j] = true;
                }
                count++;
            }
        }
        return count;
    }

    static void Main(string[] args)
    {
        int max = int.Parse(args[0]);
        int count = Count(max);
        Console.WriteLine($"Found {count} primes between 2 and {max}");
    }
}
```

注意，访问 `BitArray` 元素的语法与访问 `bool[]` 元素的语法完全相同。

以下示例展示了一个 26×10 网格类，它有一个带两个参数的索引器。第一个参数要求是 A–Z 范围内的大写或小写字母，第二个参数要求是 0–9 范围内的整数。

```csharp
class Grid
{
    const int NumRows = 26;
    const int NumCols = 10;
    int[,] cells = new int[NumRows, NumCols];

    public int this[char row, int col]
    {
        get
        {
            row = Char.ToUpper(row);
            if (row < 'A' || row > 'Z')
            {
                throw new ArgumentOutOfRangeException("row");
            }
            if (col < 0 || col >= NumCols)
            {
                throw new ArgumentOutOfRangeException ("col");
            }
            return cells[row - 'A', col];
        }
        set
        {
            row = Char.ToUpper(row);
            if (row < 'A' || row > 'Z')
            {
                throw new ArgumentOutOfRangeException ("row");
            }
            if (col < 0 || col >= NumCols)
            {
                throw new ArgumentOutOfRangeException ("col");
            }
            cells[row - 'A', col] = value;
        }
    }
}
*end example*
```

## 15.9.2 索引器与属性的差异

索引器和属性在概念上非常相似，但在以下方面有所不同：

- 属性通过其名称标识，而索引器通过其签名标识。
- 属性通过 simple_name（§12.8.4）或 member_access（§12.8.7）访问，而索引器元素通过 element_access（§12.8.11.3）访问。
- 属性可以是静态成员，而索引器始终是实例成员。
- 属性的 get 访问器对应于无参数的方法，而索引器的 get 访问器对应于与索引器具有相同形参列表的方法。
- 属性的 set 访问器对应于具有名为 value 的单个参数的方法，而索引器的 set 访问器对应于与索引器具有相同形参列表并外加一个名为 value 的参数的方法。
- 如果索引器访问器声明的局部变量或局部常量与索引器参数同名，则属于编译时错误。
- 在重写属性声明中，继承的属性使用语法 base.P 访问，其中 P 是属性名。在重写索引器声明中，继承的索引器使用语法 base[E] 访问，其中 E 是以逗号分隔的表达式列表。

- 不存在“自动实现的索引器”的概念。具有分号访问器的非抽象、非外部索引器是错误的。

除这些差异外，§15.7.3、§15.7.5 和 §15.7.6 中定义的所有规则也适用于索引器访问器以及属性访问器。

> 注意：在阅读 §15.7.3、§15.7.5 和 §15.7.6 时，将 property/properties 替换为 indexer/indexers 的做法同样适用于已定义术语。例如，read-write property 变为 read-write-indexer。结束注意

## 15.10 运算符

### 15.10.1 概述

运算符是一种成员，它定义可应用于类实例的表达式运算符的含义。运算符使用 operator_declarations 声明：

```csharp
operator_declaration
  : attributes? operator_modifier+ operator_declarator operator_body
  ;

operator_modifier
  : 'public'
  | 'static'
  | 'extern'
  | unsafe_modifier  // unsafe code support
  ;

operator_declarator
  : unary_operator_declarator
  | binary_operator_declarator
  | conversion_operator_declarator
  ;

unary_operator_declarator
  : type 'operator' overloadable_unary_operator '(' fixed_parameter ')'
  ;

overloadable_unary_operator
  : '+' | '-' | '!' | '~' | '++' | '--' | 'true' | 'false'
  ;

binary_operator_declarator
  : type 'operator' overloadable_binary_operator
    '(' fixed_parameter ',' fixed_parameter ')'
  ;

overloadable_binary_operator
  : '+' | '-' | '*' | '/' | '%' | '&' | '|' | '^' | '<<'
  | right_shift | '==' | '!=' | '>' | '<' | '>=' | '<='
  ;

conversion_operator_declarator
  : 'implicit' 'operator' type '(' fixed_parameter ')'
  | 'explicit' 'operator' type '(' fixed_parameter ')'
```

```
;
operator_body
: block
| '=>' expression ';'
| ';'
;
```

unsafe_modifier（§23.2）仅在 unsafe 代码（§23）中可用。

可重载运算符分为三类：一元运算符（§15.10.2）、二元运算符（§15.10.3）和转换运算符（§15.10.4）。

operator_body 是分号、块体（§15.6.1）或表达式体（§15.6.1）。块体由一个块组成，该块指定调用运算符时要执行的语句。该块应符合 §15.6.11 中所述的返回值方法规则。表达式体由 => 后跟一个表达式和分号组成，表示调用运算符时要执行的单个表达式。

对于 extern 运算符，operator_body 仅由分号组成。对于所有其他运算符，operator_body 是块体或表达式体。

以下规则适用于所有运算符声明：

- 运算符声明应同时包含 public 和 static 修饰符。
- 运算符的参数除 in 外不得带有其他修饰符。
- 运算符的签名（§15.10.2、§15.10.3、§15.10.4）应不同于同一类中声明的所有其他运算符的签名。
- 运算符声明中引用的所有类型应至少与运算符本身一样可访问（§7.5.5）。
- 同一修饰符在运算符声明中多次出现是错误的。

每个运算符类别都施加额外限制，如以下子条款所述。

与其他成员一样，基类中声明的运算符由派生类继承。由于运算符声明始终要求声明该运算符的类或结构参与运算符的签名，因此派生类中声明的运算符不可能隐藏基类中声明的运算符。因此，new 修饰符从不需要，也从不允许出现在运算符声明中。

有关一元运算符和二元运算符的更多信息，请参见 §12.4。

有关转换运算符的更多信息，请参见 §10.5。

### 15.10.2 一元运算符

以下规则适用于一元运算符声明，其中 T 表示包含该运算符声明的类或结构的实例类型：

- 一元 +、-、! 或 ~ 运算符应接受一个类型为 T 或 T? 的单个参数，并且可以返回任何类型。
- 一元 ++ 或 -- 运算符应接受一个类型为 T 或 T? 的单个参数，并且应返回该相同类型或由其派生的类型。
- 一元 true 或 false 运算符应接受一个类型为 T 或 T? 的单个参数，并且应返回 bool 类型。

一元运算符的签名由运算符标记（+、-、!、~、++、--、true 或 false）和单个形参的类型组成。返回类型不是一元运算符签名的一部分，形参名称也不是。

true 和 false 一元运算符要求成对声明。如果类声明了其中一个运算符而未同时声明另一个，则发生编译时错误。true 和 false 运算符在 §12.24 中进一步描述。

示例：以下示例展示了一个整数向量类的 operator++ 的实现及后续用法：

```csharp
public class IntVector
{
    public IntVector(int length) {...}
    public int Length { get { ... } }                     // Read-only property
    public int this[int index] { get { ... } set { ... } } // Read-write indexer

    public static IntVector operator++(IntVector iv)
    {
        IntVector temp = new IntVector(iv.Length);
        for (int i = 0; i < iv.Length; i++)
        {
            temp[i] = iv[i] + 1;
        }
        return temp;
    }
}

class Test
{
    static void Main()
    {
        IntVector iv1 = new IntVector(4); // Vector of 4 x 0
        IntVector iv2;
        iv2 = iv1++;                     // iv2 contains 4 x 0, iv1 contains 4 x 1
        iv2 = ++iv1;                     // iv2 contains 4 x 2, iv1 contains 4 x 2
    }
}
```

请注意，该运算符方法如何返回将操作数加 1 后产生的值，就像后缀递增和递减运算符（§12.8.15）以及前缀递增和递减运算符（§12.9.6）一样。与 C++ 不同，此方法不应直接修改其操作数的值，因为这会违反后缀递增运算符（§12.8.15）的标准语义。

*示例结束*

### 15.10.3 二元运算符

以下规则适用于二元运算符声明，其中 T 表示包含该运算符声明的类或结构的实例类型：

- 二元非移位运算符应接受两个参数，其中至少一个参数的类型应为 T 或 T?，并且可以返回任何类型。
- 二元 << 或 >> 运算符（§12.11）应接受两个参数，其中第一个参数的类型应为 T 或 T?，第二个参数的类型应为 int 或 int?，并且可以返回任何类型。一个……的签名
