

ML 判定此列表的类型为 **int list**。ML 的强类型特性决定了列表只能包含类型完全相同的元素。下面这个示例结构就违反了这一限制，它在列表中混合了不同类型的元素：

```
```text
> [1,2,3.1];
Error: operator and operand don't agree [literal]
   operator domain: int * int list
   operand:        int * real list
   in expression:
      2 :: 3.1 :: nil
```
```

如果我们要混合不同类型的数据，就必须使用**元组**：

```
```text
> (1,2,3.1);
val it = (1,2,3.1) : int * int * real
```
```

前面示例中产生的错误信息也为我们提示了 ML 构造列表的方式，这与 Scheme 构造列表的方式类似。也就是说，运算符 `::` 对应于 Scheme 中的 cons，它由一个元素（成为列表的头部）和一个已构造好的列表（成为列表的尾部）构造出一个新列表。例如：

```
```text
> op :: ;
val it = fn : 'a * 'a list -> 'a list
> 2 :: [3,4];
val it = [2,3,4] : int list
```
```

请注意，`::` 运算符的类型中包含一个**类型变量** `'a`，因为 `::` 可以应用于包含任意类型值的列表。因此，`::` 是一个从任意类型 `'a` 和任意相同类型 `'a` 的列表到相同类型 `'a` 的列表的函数。

在 ML 中，每个列表都是由一系列 `::` 运算符的应用构造而成的：

```
```text
> 1 :: 2 :: 3 :: [];
val it = [1,2,3] : int list
```
```

这里的 `[]` 是空列表，也可以写作关键字 **nil**。

ML 也有与 Scheme 的 car 和 cdr 运算符对应的操作，只不过它们被称为 **hd** 和 **tl**（分别代表**头**和**尾**）。例如：

```
```text
> hd [1,2,3];
val it = 1 : int
> tl [1,2,3];
val it = [2,3] : int list
```
```

事实上，这些函数在 ML 中的使用频率远低于它们在 Scheme 中的对应版本，因为 ML 的模式匹配能力使它们变得不再必要。在 ML 中，如果我们想识别列表 L 的头部和尾部，只需将列表写成 h :: t 的形式。ML 会通过将模式与列表 L 进行匹配，从而将 h 提取为头部，将 t 提取为尾部。如果 L 为空，则该模式无法匹配，并会产生如下警告：

```
> val h::t = [1,2,3]:
Warning: binding not exhaustive
      h :: t = ...
val h = 1 : int
val t = [2,3] : int list
```

模式匹配更常用于函数定义和 case 表达式中。例如，ML 中的列表追加函数可以如下定义：⁸

```
> fun append ([], L) = L
  | append (h :: t , L) = h :: append (t , L);
val append = fn : 'a list * 'a list -> 'a list
```

这等价于下面使用 case 表达式的定义：

```
> fun append (x,y) =
    case x of
      []      => y |
      (h::t) => h :: append (t,y);
```

模式匹配几乎可以用于所有需要进行情况分析的函数定义中，并且它可以消除大多数 if 表达式的使用。例如，前面定义的递归阶乘函数也可以用模式匹配来编写：

```
fun fact 0 = 1 | fact n = n * fact (n - 1);
```

这里的第二个模式——变量 n——可以匹配任何内容，但作为第二个模式的位置意味着它不能为零；如果它是零，第一个模式（整数常量 0）就会匹配成功。

ML 中的模式还可以包含通配符，写作下划线字符。通配符是可以匹配任何内容的模式，但我们不关心其具体值。例如，我们可以定义自己的 hd 函数版本，如下所示：

```
fun hd (h::_) = h;
```

实际上，这个定义会产生一条警告信息（“match nonexhaustive”），因为我们没有定义 hd 在空列表情况下应该做什么。更好的定义如下，它与预定义的 hd 所做的事情本质上完全相同：

```
fun hd (h::_) = h | hd [] = raise Empty;
```

> ⁸实际上，ML 有一个内置的中缀追加运算符 @：[1,2,3] @ [4,5,6] = [1,2,3,4,5,6]。

ML 的强类型虽然安全且灵活，但对可接受的程序施加了重要的限制。一个典型的例子是平方函数，下面我们为实数（浮点）类型定义它：

```
> fun square x: real = x * x;
val square = fn : real -> real
```

现在，如果我们尝试用整数来调用此函数，就会产生错误，因为 ML（与 ADA 一样）不会自动将整数转换为实数：

```
> square 2;
Error: operator and operand don’t agree [literal]
operator domain: real
operand:          int
in expression:
    square 2
```

相反，我们需要使用转换函数手动转换整数。在下面的示例中，该函数与我们要转换到的数据类型同名：

```
> square (real 2);
val it = 4.0 : real
```

我们可能会想，可以为整数定义一个同名函数：

```
> fun square x: int = x * x;
val square = fn : int -> int
```

但 ML 不允许重载。因此，这个定义只会替换掉前一个定义。我们还可以尝试不指定参数类型来定义一个泛化版本的 square：

```
> fun square x = x * x;
val square = fn : int -> int
```

然而，在这种情况下，ML 只是假定我们想让 x 是整数。⁹ 问题在于，虽然内置算术函数对 int 和 real 等算术类型进行了重载，但我们不能利用这一点来定义任何用户自定义的重载函数。在 Haskell 语言中，这在大多数情况下不是问题（本章后面会说明）。

一个相关的问题是，ML 中的某些值包含的类型信息不足以让 ML 在表达式求值之前正确地进行类型检查。主要例子是空列表 []，它的类型是 'a list。如果 ML 要对空列表求值一个多态函数，在某些情况下，ML 会指出关于 [] 的类型信息不足：

```
> rev [];
type vars not generalized because of value
restriction are instantiated to dummy types (X1,X2,...)
val it = [] : ?X1 list
```

⁹旧版本的 ML 会将此函数定义视为错误。

```
> open TextIO; (* 解引用 TextIO 结构 *)
... (* ML 解释器列出 TextIO 的内容 *)
> output(stdout,inputLine(stdin));
        (* 读取并写入一行文本 *)
Hello, world!
Hello, world!
val it = () : unit
>
```

请注意，输出操作的返回值是值 ()，它的类型是 unit。这类似于 C 语言中的 void 类型，但在 ML 中每个函数都必须返回某个值，因此 unit 类型恰好有一个值 () 来表示“没有实际值”。¹

现在，这两个 I/O 函数只能读写字符串。要在字符串和数字之间进行转换，我们必须使用相应类型的工具结构中的 toString 和 fromString 函数（例如，int 类型的 Int 结构）：

```
> Int.toString;
val it = fn : int -> string
> Int.fromString;
val it = fn : string -> int option
```

这又带来了一个小障碍。fromString 函数可能无法提取任何数字，在这种情况下它会返回一个 option 类型的值。其定义如下：

```
datatype 'a option = NONE | SOME of 'a;
```

最后，当执行一系列输入输出操作时，将这些操作收集在表达式序列中会很方便（类似于 Scheme 的 begin 结构），这是一个由分号分隔的表达式序列，用括号括起来，其值是最后一个表达式的值：

```
> fun printstuff () =
    ( output(stdout,"Hello\n");
      output(stdout,"World!\n")
    );
val printstuff = fn : unit -> unit
> printstuff ();
Hello
World!
val it = () : unit
```

¹Unit 还可以用来模拟 ML 中的无参数函数，因为 ML 要求每个函数至少有一个参数。

