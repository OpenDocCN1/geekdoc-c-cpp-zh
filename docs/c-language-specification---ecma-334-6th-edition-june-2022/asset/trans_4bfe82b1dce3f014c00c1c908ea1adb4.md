
- 在同一个声明空间中，允许存在两个或更多具有相同名称的命名空间声明。此类命名空间声明会聚合形成单个逻辑命名空间，并共享同一个声明空间。
- 在不同程序中但在同一个命名空间声明空间中的声明，允许共享相同的名称。
  注意：但是，如果这些声明包含在同一个应用程序中，则可能引入歧义。
  注释结束
- 在同一个声明空间中，允许存在两个或更多具有相同名称但签名不同的方法（§7.6）。
- 在同一个声明空间中，允许存在两个或更多具有相同名称但类型参数数目不同的类型声明（§7.8.2）。
- 在同一个声明空间中，具有 partial 修饰符的两个或更多类型声明可以共享相同的名称、相同的类型参数数目和相同的分类（class、struct 或 interface）。在这种情况下，这些类型声明共同构成一个类型，并聚合形成单个声明空间（§14.2.7）。
- 在同一个声明空间中，命名空间声明和类型声明可以共享相同的名称，只要该类型声明至少有一个类型参数（§7.8.2）。

如下所述，声明空间有几种不同的类型。

- 在程序的所有编译单元中，没有包含在 namespace_declaration 中的 namespace_member_declarations 是名为全局声明空间的单个组合声明空间的成员。
- 在程序的所有编译单元中，位于具有相同完全限定命名空间名称的 namespace_declarations 内的 namespace_member_declarations 是单个组合声明空间的成员。
- 每个 compilation_unit 和 namespace_body 都有一个别名声明空间。compilation_unit 或 namespace_body 的每个 extern_alias_directive 和 using_alias_directive 都向别名声明空间贡献一个成员（§13.5.2）。
- 每个非 partial 的 class、struct 或 interface 声明都会创建一个新的声明空间。每个 partial 的 class、struct 或 interface 声明都会向由同一程序中所有匹配部分共享的声明空间贡献内容（§15.2.3）。名称通过 class_member_declarations、struct_member_declarations、interface_member_declarations 或 type_parameters 引入到此声明空间。除重载的实例构造函数声明和静态构造函数声明外，class 或 struct 不能包含与 class 或 struct 同名的成员声明。class、struct 或 interface 允许声明重载的方法和索引器。此外，class 或 struct 允许声明重载的实例构造函数和运算符。例如，class、struct 或 interface 可以包含多个同名的方法声明，只要这些方法声明的签名不同（§7.6）。请注意，基类不会向 class 的声明空间贡献成员，基接口也不会向 interface 的声明空间贡献成员。因此，允许派生类或派生接口声明与继承成员同名的成员。这样的成员称为隐藏了继承成员。
- 每个 delegate 声明都会创建一个新的声明空间。名称通过形参（fixed_parameters 和 parameter_arrays）和 type_parameters 引入到此声明空间。
- 每个枚举声明都会创建一个新的声明空间。名称通过 enum_member_declarations 引入到此声明空间。
- 每个方法声明、属性声明、属性访问器声明、索引器声明、索引器访问器声明、运算符声明、实例构造函数声明和匿名函数都会创建一个称为局部变量声明空间的新声明空间。名称通过形参（fixed_parameters 和 parameter_arrays）和 type_parameters 引入到此声明空间。属性或索引器的 set 访问器将名为 value 的形参引入。函数成员或匿名函数的主体（如果有）被视为嵌套在局部变量声明空间内。如果局部变量声明空间与其嵌套的局部变量声明空间包含同名元素，则是错误的。因此，在嵌套声明空间中，不能声明与外部声明空间中的局部变量或常量同名的局部变量或常量。只要两个声明空间互不包含，它们就可以包含同名元素。
- 每个 block 或 switch_block，以及 for、foreach 和 using 语句，都会为局部变量和局部常量创建一个局部变量声明空间。名称通过 local_variable_declarations 和 local_constant_declarations 引入到此声明空间。请注意，作为函数成员或匿名函数的主体出现或位于其主体内的 block，嵌套在这些函数为其参数声明的局部变量声明空间内。因此，例如，一个方法的局部变量和参数同名是错误的。
- 每个 block 或 switch_block 都会为标签创建一个单独的声明空间。名称通过 labeled_statements 引入到此声明空间，并通过 goto_statements 引用这些名称。block 的标签声明空间包含任何嵌套的 block。因此，在嵌套 block 内，不能声明与外部 block 中的标签同名的标签。

名称声明的文本顺序通常无关紧要。特别是，对于命名空间、常量、方法、属性、事件、索引器、运算符、实例构造函数、终结器、静态构造函数和类型的声明和使用，文本顺序并不重要。声明顺序在以下方面具有重要意义：

- 字段声明的声明顺序决定了其初始化器（如果有）的执行顺序（§14.5.6.2、§14.5.6.3）。
- 局部变量必须先定义后使用（§7.7）。
- 当省略 constant_expression 值时，枚举成员声明（§18.4）的声明顺序很重要。

示例：命名空间的声明空间是“开放”的，两个具有相同完全限定名称的命名空间声明会贡献到同一个声明空间。例如

```
namespace Megacorp.Data
{
    class Customer
    {
        ...
    }
}

namespace Megacorp.Data
{
    class Order
    {
        ...
    }
}
```

上面的两个命名空间声明贡献到同一个声明空间，在本例中声明了两个类，其完全限定名分别为 `Megacorp.Data.Customer` 和 `Megacorp.Data.Order`。由于这两个声明贡献到同一个声明空间，如果每个声明中都包含一个同名类的声明，则会导致编译时错误。

*示例结束*

*注意：* 如上所述，block 的声明空间包含任何嵌套的 block。因此，在下面的示例中，F 和 G 方法会导致编译时错误，因为名称 i 在外部 block 中声明，不能在内部 block 中重新声明。但是，H 和 I 方法是有效的，因为两个 i 是在互不嵌套的 block 中声明的。

```csharp
class A
{
    void F()
    {
        int i = 0;
        if (true)
        {
            int i = 1;
        }
    }

    void G()
    {
        if (true)
        {
            int i = 0;
        }
        int i = 1;
    }

    void H()
    {
        if (true)
        {
            int i = 0;
        }
        if (true)
        {
            int i = 1;
        }
    }

    void I()
    {
        for (int i = 0; i < 10; i++)
        {
            H();
        }
    }
}
```

