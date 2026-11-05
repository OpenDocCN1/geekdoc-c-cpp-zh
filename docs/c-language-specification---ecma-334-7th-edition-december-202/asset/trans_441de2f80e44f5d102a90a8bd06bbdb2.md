
```
explicit_anonymous_function_signature
: '(' explicit_anonymous_function_parameter_list? ')'
;

explicit_anonymous_function_parameter_list
: explicit_anonymous_function_parameter
(',' explicit_anonymous_function_parameter)*
;

explicit_anonymous_function_parameter
: anonymous_function_parameter_modifier? type identifier
;

anonymous_function_parameter_modifier
: 'ref'
| 'out'
| 'in'
;

implicit_anonymous_function_signature
: '(' implicit_anonymous_function_parameter_list? ')'
| implicit_anonymous_function_parameter
;

implicit_anonymous_function_parameter_list
: implicit_anonymous_function_parameter
(',' implicit_anonymous_function_parameter)*
;

implicit_anonymous_function_parameter
: identifier
;

anonymous_function_body
: null_conditional_invocation_expression
| expression
| 'ref' variable_reference
| block
;
```

在识别*匿名函数体*时，如果*空条件调用表达式*和*表达式*这两个备选形式都适用，则应选择前者。

注意：此处各备选形式之间的重叠和优先级仅出于描述上的便利；语法规则可以进一步细化以消除重叠。ANTLR 及其他语法系统采用同样的便利做法，因此*匿名函数体*会自动具有所指定的语义。注意结束

注意：当被视为*表达式*时，如果 M 的结果类型为 void，那么诸如 x?.M() 这样的语法形式将是错误（§12.8.12）。但当被视为*空条件调用表达式*时，结果类型允许为 void。注意结束

示例：List<T>.Reverse 的结果类型为 void。在以下代码中，匿名表达式的主体是*空条件调用表达式*，因此不是错误。

```
Action<List<int>> a = x => x?.Reverse();
```

示例结束

=> 运算符与赋值（=）具有相同的优先级，并且是右结合的。

带有 async 修饰符的匿名函数是异步函数，并遵循 §15.15 中描述的规则。

以 *lambda 表达式*形式表示的匿名函数的参数可以显式或隐式类型化。在显式类型化参数列表中，每个参数的类型都显式声明。在隐式类型化参数列表中，参数类型从匿名函数出现的上下文中推断——具体而言，当匿名函数转换为兼容的委托类型或表达式树类型时，该类型提供参数类型（§10.7）。

在具有单个隐式类型化参数的 *lambda 表达式*中，参数列表中的括号可以省略。换言之，以下形式的匿名函数

```
( «param» ) => «expr»
```

可以缩写为

```
«param» => «expr»
```

以 *匿名方法表达式*形式表示的匿名函数的参数列表是可选的。如果给出，参数应显式类型化。如果未给出，则匿名函数可转换为具有任何不包含 out 参数的参数列表的委托。

匿名函数的块体始终是可到达的（§13.2）。

示例：下面给出匿名函数的一些示例：

```
x => x + 1 // Implicitly typed, expression body
x => { return x + 1; } // Implicitly typed, block body
(int x) => x + 1 // Explicitly typed, expression body
(int x) => { return x + 1; } // Explicitly typed, block body
(x, y) => x * y // Multiple parameters
() => Console.WriteLine() // No parameters
async (t1, t2) => await t1 + await t2 // Async
delegate (int x) { return x + 1; } // Anonymous method expression
delegate { return 1 + 1; } // Parameter list omitted
```

示例结束

*lambda 表达式*和*匿名方法表达式*的行为相同，但以下几点除外：

- *匿名方法表达式*允许完全省略参数列表，从而可转换为任何值参数列表的委托类型。
- *lambda 表达式*允许省略并推断参数类型，而*匿名方法表达式*要求显式声明参数类型。
- *lambda 表达式*的主体可以是表达式或块，而*匿名方法表达式*的主体必须是块。
- 只有 *lambda 表达式*具有到兼容表达式树类型的转换（§8.6）。

## 12.19.2 匿名函数签名

匿名函数的*匿名函数签名*定义该匿名函数的形式参数的名称以及可选类型。匿名函数参数的作用域是*匿名函数体*（§7.7）。与参数列表（如果给出）一起，匿名方法体构成声明空间（§7.3）。因此，匿名函数的参数名称如果与作用域包含*匿名方法表达式*或*lambda 表达式*的局部变量、局部常量或参数名称匹配，则属于编译时错误。

如果匿名函数具有*显式匿名函数签名*，则兼容的委托类型和表达式树类型的集合仅限于具有相同参数类型和修饰符且顺序相同的类型（§10.7）。与方法组转换（§10.8）不同，不支持匿名函数参数类型的逆变。如果匿名函数没有*匿名函数签名*，则兼容的委托类型和表达式树类型的集合仅限于没有 out 参数的类型。

注意，*匿名函数签名*不能包含特性或参数数组。然而，*匿名函数签名*可以与参数列表包含参数数组的委托类型兼容。

另请注意，到表达式树类型的*转换*即使兼容，仍可能在编译时失败（§8.6）。

## 12.19.3 匿名函数体

匿名函数的主体（*表达式*或*块*）遵循以下规则：

- 如果匿名函数包含签名，则签名中指定的参数可在主体中使用。如果匿名函数没有签名，它可以转换为带参数的委托类型或表达式类型（§10.7），但在主体中无法访问这些参数。
- 除最近封闭匿名函数的签名（如果有）中指定的 *in*、*out* 或 *ref* 参数外，主体访问 *in*、*out* 或 *ref* 参数属于编译时错误。
- 除最近封闭匿名函数的签名（如果有）中指定的参数外，主体访问 *ref struct* 类型的参数属于编译时错误。
- 当 *this* 的类型为结构类型时，主体访问 *this* 属于编译时错误。无论访问是显式的（如 *this.x*）还是隐式的（如 *x*，其中 *x* 是结构体的实例成员），都是如此。此规则仅禁止此类访问，不影响成员查找是否得到结构体的成员。
- 主体可以访问匿名函数的外部变量（§12.19.6）。访问外部变量将引用在求值 *lambda 表达式*或*匿名方法表达式*时处于活动状态的变量实例（§12.19.7）。
- 主体包含目标在主体之外或包含的*匿名函数*主体之内的 *goto* 语句、*break* 语句或 *continue* 语句属于编译时错误。
- 主体中的 *return* 语句从最近封闭*匿名函数*的调用返回控制，而不是从封闭的函数成员返回。

除通过求值和调用 *lambda 表达式*或*匿名方法表达式*之外，是否存在任何方式执行匿名函数的块，明确未作规定。特别是，编译器可以选择通过合成一个或多个命名方法或类型来实现匿名函数。任何此类合成元素的名称应采用保留供编译器使用的形式（§6.4.3）。
