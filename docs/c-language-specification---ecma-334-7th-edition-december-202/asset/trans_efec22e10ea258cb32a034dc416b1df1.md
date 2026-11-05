
```
#if true
...
#endif
```

> Note: 这意味着一个区域可以包含一个或多个 #if.../#endif，或包含在 #if.../#endif 内的条件部分中；但一个区域不能与 #if.../#endif 的仅一部分重叠，或在不同的条件部分中开始和结束。 end note

## 6.5.8 行指令

行指令可用于更改编译器在警告和错误等输出中报告的行号和编译单元名称。这些值也由调用信息属性 (§22.5.5) 使用。

> Note: 行指令最常用于从其他文本输入生成 C# 源代码的元编程工具中。 end note

```
fragment PP_Line
  : 'line' PP_Whitespace PP_Line_Indicator
  ;

fragment PP_Line_Indicator
  : Decimal_Digit+ PP_Whitespace PP_Compilation_Unit_Name
  | Decimal_Digit+
  | DEFAULT
  | 'hidden'
  ;

fragment PP_Compilation_Unit_Name
  : '"' PP_Compilation_Unit_Name_Character+ '"'
  ;

fragment PP_Compilation_Unit_Name_Character
  // Any Input_Character except "
  : ~('\\u000D' | '\\u000A' | '\\u0085' | '\\u2028' | '\\u2029' | '#')
  ;
```

当不存在 #line 指令时，编译器在其输出中报告真实的行号和编译单元名称。当处理包含非默认 PP_Line_Indicator 的 #line 指令时，编译器将该指令之后的行的行号视为给定行号（如果指定，则包括编译单元名称）。

最大允许的 Decimal_Digit+ 值由实现定义。

#line default 指令会撤销所有前面 #line 指令的效果。编译器对后续行报告真实的行信息，就好像没有处理过 #line 指令一样。

#line hidden 指令对错误消息中报告的编译单元和行号，或由 CallerLineNumberAttribute (§22.5.5.2) 使用产生的结果没有影响。它的目的是影响源代码级调试工具，以便在调试时，#line hidden 指令与后续 #line 指令（不是 #line hidden）之间的所有行都没有行号信息，并且在单步执行代码时完全被跳过。

> Note: 尽管 PP_Compilation_Unit_Name 可能包含看起来像转义序列的文本，但此类文本不是转义序列；在这种情况下，'\' 字符仅表示普通的反斜杠字符。 end note

## 6.5.9 Pragma 指令

#pragma 预处理指令用于向编译器指定上下文信息。

*注意：例如，编译器可能会提供 #pragma 指令，例如*
- 在编译后续代码时启用或禁用特定警告消息。
- 指定对后续代码应用哪些优化。
- 指定调试器使用的信息。
*结束注释*

```
fragment PP_Pragma
    : 'pragma' PP_Pragma_Text?
    ;

fragment PP_Pragma_Text
    : PP_Whitespace Input_Character*
    ;
```

*Input_Characters* 在 *PP_Pragma_Text* 中由编译器以实现定义的方式解释。#pragma 指令中提供的信息不得更改程序语义。#pragma 指令只能更改超出本语言规范范围的编译器行为。如果编译器无法解释 *Input_Characters*，编译器可以发出警告；但是，它不得产生编译时错误。

*注意：PP_Pragma_Text 可以包含任意文本；具体来说，它不必包含格式良好的标记。结束注释*

## 7. 基本概念

### 7.1 应用程序启动

程序可以编译为 *类库* 以作为其他应用程序的一部分使用，也可以编译为可直接启动的 *应用程序*。确定此编译模式的机制是实现特定的，并且在该规范之外。

程序编译为应用程序时，必须至少包含一个满足以下要求的方法作为入口点：
- 它的名称应为 `Main`。
- 它应为 `static`。
- 它不应是泛型的。
- 它应在非泛型类型中声明。如果声明该方法的类型是嵌套类型，则其所有封闭类型都不得是泛型的。
- 如果方法返回类型为 `System.Threading.Tasks.Task` 或 `System.Threading.Tasks.Task<int>`，则它可以具有 `async` 修饰符。
- 返回类型应为 `void`、`int`、`System.Threading.Tasks.Task` 或 `System.Threading.Tasks.Task<int>`。
- 它不得是没有实现的 partial 方法 (§15.6.9)。
- 形式参数列表应为空，或具有单个类型为 `string[]` 的值参数。

*注意：* 具有 `async` 修饰符的方法必须具有上述两个返回类型之一，才能符合入口点的条件。`async void` 方法，或返回不同可等待类型（如 `ValueTask` 或 `ValueTask<int>`）的 `async` 方法不符合入口点的条件。 *结束注释*

如果在程序中声明了多个符合入口点条件的方法，可以使用外部机制指定哪个方法被视为应用程序的实际入口点。如果找到返回类型为 `int` 或 `void` 的符合条件的方法，则返回类型为 `System.Threading.Tasks.Task` 或 `System.Threading.Tasks.Task<int>` 的任何符合条件的方法均不被视为入口点方法。将程序编译为应用程序而没有恰好一个入口点是编译时错误。编译为类库的程序可能包含符合应用程序入口点条件的方法，但生成的库没有入口点。

通常，方法的声明可访问性 (§7.5.2) 由其声明中指定的访问修饰符 (§15.3.6) 决定，类似地，类型的声明可访问性由其声明中指定的访问修饰符决定。为了使给定类型的给定方法可调用，类型和成员都应可访问。然而，应用程序入口点是一个特例。具体来说，执行环境可以访问应用程序的入口点，而不管其声明的可访问性以及其封闭类型声明的声明可访问性如何。

当入口点方法的返回类型为 System.Threading.Tasks.Task 或 System.Threading.Tasks.Task<int> 时，编译器会合成一个调用相应 Main 方法的同步入口点方法。合成的方法具有基于 Main 方法的参数和返回类型：
- 合成方法的形式参数列表与 Main 方法的形式参数列表相同
- 如果 Main 方法的返回类型为 System.Threading.Tasks.Task，则合成方法的返回类型为 void
- 如果 Main 方法的返回类型为 System.Threading.Tasks.Task<int>，则合成方法的返回类型为 int

合成方法的执行按如下方式进行：
- 合成方法调用 Main 方法，如果 Main 方法具有此类参数，则将其 string[] 参数值作为参数传递。
- 如果 Main 方法抛出异常，则异常由合成方法传播。
- 否则，合成的入口点等待返回的任务完成，对任务调用 GetAwaiter().GetResult()，使用无参数实例方法或 §C.3 中描述的扩展方法。如果任务失败，GetResult() 将抛出异常，并且该异常由合成方法传播。
- 对于返回类型为 System.Threading.Tasks.Task<int> 的 Main 方法，如果任务成功完成，则 GetResult() 返回的 int 值将从合成方法返回。

应用程序的有效入口点是程序中声明的入口点，或如上所述需要时合成的方法。因此，有效入口点的返回类型始终为 void 或 int。

当应用程序运行时，会创建一个新的应用程序域。同一台机器上可能同时存在应用程序的多个不同实例，每个实例都有自己的应用程序域。应用程序域通过充当应用程序状态的容器来实现应用程序隔离。应用程序域充当应用程序中定义的类型及其使用的类库的容器和边界。加载到一个应用程序域中的类型与加载到另一个应用程序域中的相同类型是不同的，并且对象实例不会在应用程序域之间直接共享。例如，每个应用程序域都有这些类型的静态变量的自己的副本，并且类型的静态构造函数每个应用程序域最多运行一次。实现可以自由提供创建和销毁应用程序域的实现特定策略或机制。

应用程序启动发生在执行环境调用应用程序的有效入口点时。如果有效入口点声明了一个参数，则在应用程序启动期间，实现应确保该参数的初始值为对字符串数组的非空引用。该数组应由非空的字符串引用组成，称为应用程序参数，这些参数在应用程序启动之前由主机环境赋予实现定义的值。其目的是将托管环境中在应用程序启动前确定的信息提供给应用程序。

> Note: 在支持命令行系统的系统上，应用程序参数对应于通常所知的命令行参数。 end note
