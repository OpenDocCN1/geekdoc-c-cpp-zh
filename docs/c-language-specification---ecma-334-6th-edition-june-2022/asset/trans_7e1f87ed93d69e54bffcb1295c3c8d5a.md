
```
}
class D : C<string>
{
    static void Main()
    {
        C<int>.x = 5;
    }
}
```

对受保护成员 C<int>.x 在 D 中的引用是有效的，即使类 D 派生自 C<string>。 end note

### 7.5.5 可访问性约束

C# 语言中的若干构造要求类型至少与成员或其他类型一样可访问。

A type T 被认为至少与成员或类型 M 一样可访问，如果 T 的可访问性域是 M 的可访问性域的超集。换句话说，如果 T 在 M 可访问的所有上下文中都可访问，则 T 至少与 M 一样可访问。

以下可访问性约束存在：

- 类类型的直接基类应至少与类类型本身一样可访问。
- 接口类型的显式基接口应至少与接口类型本身一样可访问。
- 委托类型的返回类型和参数类型应至少与委托类型本身一样可访问。
- 常量的类型应至少与常量本身一样可访问。
- 字段的类型应至少与字段本身一样可访问。
- 方法的返回类型和参数类型应至少与方法本身一样可访问。
- 属性的类型应至少与属性本身一样可访问。
- 事件的类型应至少与事件本身一样可访问。
- 索引器的类型和参数类型应至少与索引器本身一样可访问。
- 运算符的返回类型和参数类型应至少与运算符本身一样可访问。
- 实例构造函数的参数类型应至少与实例构造函数本身一样可访问。
- 类型参数上的接口或类类型约束应至少与声明该约束的成员一样可访问。

Example: 以下代码中

```
class A {...}
public class B: A {...}
```

B 类会导致编译时错误，因为 A 并不是至少与 B 一样可访问。

end example

Example: 同样地，在以下代码中

```
class A { ... }

public class B
{
    A F() { ... }
    internal A G() { ... }
    public A H() { ... }
}
```

B 中的 H 方法会导致编译时错误，因为返回类型 A 并不是至少与该方法一样可访问。

*end example*

## 7.6 签名和重载

方法、实例构造函数、索引器和运算符由其 **签名** 刻画：

- 方法的签名由方法名、类型参数的数量以及每个形式参数的类型和参数传递模式（值、引用或输出）组成，按从左到右的顺序考虑。对于此目的，方法中出现在形式参数类型中的任何类型参数不是按其名称标识，而是按其在方法类型参数列表中的序数位置标识。方法的签名特指不包括返回类型、参数名、类型参数名、类型参数约束、`params` 或 `this` 参数修饰符，以及参数是否必需或可选。
- 实例构造函数的签名由每个形式参数的类型和参数传递模式（值、引用或输出）组成，按从左到右的顺序考虑。实例构造函数的签名特指不包括可能为最右参数指定的 `params` 修饰符。
- 索引器的签名由每个形式参数的类型组成，按从左到右的顺序考虑。索引器的签名特指不包括元素类型，也不包括可能为最右参数指定的 `params` 修饰符。
- 运算符的签名由运算符名和每个形式参数的类型组成，按从左到右的顺序考虑。运算符的签名特指不包括结果类型。
- 转换运算符的签名由源类型和目标类型组成。转换运算符的隐式或显式分类不是签名的一部分。
- 相同成员种类（方法、实例构造函数、索引器或运算符）的两个签名如果具有相同的名称、类型参数数量、参数数量和参数传递模式，并且其对应参数的类型之间存在恒等转换（§10.2.2），则被认为相同。

签名是类、结构和接口中成员 **重载** 的启用机制：

- 方法的重载允许类、结构或接口声明多个同名方法，前提是其签名在该类、结构或接口内唯一。
- 实例构造函数的重载允许类或结构声明多个实例构造函数，前提是其签名在该类或结构内唯一。
- 索引器的重载允许类、结构或接口声明多个索引器，前提是其签名在该类、结构或接口内唯一。
- 运算符的重载允许类或结构声明多个同名运算符，前提是其签名在该类或结构内唯一。

尽管 out 和 ref 参数修饰符被视为签名的一部分，但在单个类型中声明的成员不能仅因 ref 和 out 而在签名上有所不同。如果在同一类型中声明了两个成员，其签名在将两个方法中所有带 out 修饰符的参数都改为 ref 修饰符后会相同，则会发生编译时错误。对于签名字符串匹配的其他目的（例如隐藏或重写），ref 和 out 被视为签名的一部分且互不匹配。

> 注记：此限制是为了允许 C# 程序易于翻译为在通用语言基础结构（CLI）上运行，后者没有提供一种仅在 ref 和 out 上有所不同的方式来定义方法。 end note

比较签名时，类型 object 和 dynamic 不予区分。因此，在单个类型中声明的仅因用 dynamic 替换 object 而签名不同的成员是不允许的。

Example: 以下示例展示了一组重载的方法声明及其签名。

```
interface ITest
{
    void F();                         // F()
    void F(int x);                    // F(int)
    void F(ref int x);                // F(ref int)
    void F(out int x);                // F(out int) error
    void F(object o);                 // F(object)
    void F(dynamic d);                // error.
    void F(int x, int y);             // F(int, int)
    int F(string s);                  // F(string)
    int F(int x);                     // F(int) error
    void F(string[] a);               // F(string[])
    void F(params string[] a);        // F(string[]) error
    void F<S>(S s);                   // F<S>(S)
    void F<T>(T t);                   // F<T>(T) error
    void F<S,T>(S s);                 // F<S,T>(S)
    void F<T,S>(S s);                 // F<T,S>(S) ok
}
```

请注意，任何 ref 和 out 参数修饰符（§14.6.2）都是签名的一部分。因此，F(int)、F(ref int) 和 F(out int) 都是唯一的签名。然而，F(ref int) 和 F(out int) 不能在同一接口中声明，因为它们的签名仅因 ref 和 out 而不同。此外，请注意返回类型和 params 修饰符不是签名的一部分，因此无法仅基于返回类型或 params 修饰符的包含或排除来进行重载。因此，上述标识的方法 F(int) 和 F(params string[]) 的声明会导致编译时错误。

end example

## 7.7 作用域

### 7.7.1 通用

名称的作用域是程序文本中可以在不限定名称的情况下引用该名称所声明的实体的区域。作用域可以嵌套，内部作用域可能会重新声明外部作用域中名称的含义。（然而，这并不会消除 §7.3 规定的限制，即在嵌套块内无法声明与封闭块中的局部变量或局部常量同名的局部变量或局部常量。）此时，外部作用域的名称在内部作用域覆盖的程序文本区域中被视为隐藏，并且只能通过限定名称来访问外部名称。

- 由 namespace_member_declaration (§13.6) 声明的、没有封闭 namespace_declaration 的命名空间成员的作用域是整个程序文本。
- 由 namespace_declaration 内的 namespace_member_declaration 声明的命名空间成员的作用域，其完全限定名称为 N，是完全限定名称为 N 或以 N 开随后跟一个句点的每个 namespace_declaration 的 namespace_body。
- 由 extern_alias_directive (§13.4) 定义的名称的作用域扩展到其直接包含的 compilation_unit 或 namespace_body 的 using_directives、global_attributes 和 namespace_member_declarations。extern_alias_directive 不向底层声明空间贡献任何新成员。换句话说，extern_alias_directive 不是传递的，而是仅影响它出现的 compilation_unit 或 namespace_body。
- 由 using_directive (§13.5) 定义或导入的名称的作用域扩展到 using_directive 出现的 compilation_unit 或 namespace_body 的 global_attributes 和 namespace_member_declarations。using_directive 可能使零个或多个命名空间或类型名称在特定 compilation_unit 或 namespace_body 中可用，但不向底层声明空间贡献任何新成员。换句话说，using_directive 不是传递的，而是仅影响它出现的 compilation_unit 或 namespace_body。
- 由 class_declaration (§14.2) 上的 type_parameter_list 声明的类型参数的作用域是该 class_declaration 的 class_base、type_parameter_constraints_clauses 和 class_body。注记：与类的成员不同，此作用域不扩展到派生类。 end note
- 由 struct_declaration (§15.2) 上的 type_parameter_list 声明的类型参数的作用域是该 struct_declaration 的 struct_interfaces、type_parameter_constraints_clauses 和 struct_body。
- 由 interface_declaration (§17.2) 上的 type_parameter_list 声明的类型参数的作用域是该 interface_declaration 的 interface_base、type_parameter_constraints_clauses 和 interface_body。
- 由 delegate_declaration (§19.2) 上的 type_parameter_list 声明的类型参数的作用域是该 delegate_declaration 的 return_type、formal_parameter_list 和 type_parameter_constraints_clauses。
- 由 method_declaration (§14.6.1) 上的 type_parameter_list 声明的类型参数的作用域是 method_declaration。
- 由 class_member_declaration (§14.3.1) 声明的成员的作用域是声明发生的 class_body。此外，类成员的作用域扩展到包含在该成员的可访问性域 (§7.5.3) 中的那些派生类的 class_body。
