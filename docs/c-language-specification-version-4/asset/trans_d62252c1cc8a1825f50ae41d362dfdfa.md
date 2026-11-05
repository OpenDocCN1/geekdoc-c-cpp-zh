
```
      static void F(long l) {}
    }
```

调用 F(1) 会调用 Inner 中声明的 F，因为所有外部的 F 出现都被内部声明隐藏了。出于同样的原因，调用 F("Hello") 会导致编译时错误。

## 3.7.1.2 Hiding through inheritance

Name hiding through inheritance occurs when classes or structs redeclare names that were inherited from base classes. This type of name hiding takes one of the following forms:

通过继承隐藏名称发生在类或结构体重新声明从基类继承的名称时。这种名称隐藏有以下几种形式：

- A constant, field, property, event, or type introduced in a class or struct hides all base class members with the same name.
在类或结构体中引入的常量、字段、属性、事件或类型会隐藏所有同名基类成员。

- A method introduced in a class or struct hides all non-method base class members with the same name, and all base class methods with the same signature (method name and parameter count, modifiers, and types).
在类或结构体中引入的方法会隐藏所有同名非方法基类成员，以及所有具有相同签名（方法名和参数个数、修饰符和类型）的基类方法。

- An indexer introduced in a class or struct hides all base class indexers with the same signature (parameter count and types).
在类或结构体中引入的索引器会隐藏所有具有相同签名（参数个数和类型）的基类索引器。

The rules governing operator declarations (§10.10) make it impossible for a derived class to declare an operator with the same signature as an operator in a base class. Thus, operators never hide one another.
运算符声明的规则（§10.10）使得派生类无法声明与基类运算符具有相同签名的运算符。因此，运算符永远不会相互隐藏。

Contrary to hiding a name from an outer scope, hiding an accessible name from an inherited scope causes a warning to be reported. In the example

与从外部作用域隐藏名称相反，从继承作用域隐藏可访问名称会导致发出警告。在示例中

```csharp
class Base
{
    public void F() {}
}
class Derived: Base
{
    public void F() {}      // warning, hiding an inherited name
}
```

the declaration of F in Derived causes a warning to be reported. Hiding an inherited name is specifically not an error, since that would preclude separate evolution of base classes. For example, the above situation might have come about because a later version of Base introduced an F method that wasn't present in an earlier version of the class. Had the above situation been an error, then any change made to a base class in a separately versioned class library could potentially cause derived classes to become invalid.
在 Derived 中声明 F 会导致发出警告。隐藏继承的名称特意不是错误，因为那样会阻止基类的独立演进。例如，上述情况可能是因为 Base 的较新版本引入了 F 方法，而该方法在类的早期版本中不存在。如果上述情况是错误，那么在单独版本化的类库中对基类所做的任何更改都可能导致派生类变得无效。

The warning caused by hiding an inherited name can be eliminated through use of the new modifier:

通过使用 new 修饰符可以消除隐藏继承名称引起的警告：

```csharp
class Base
{
    public void F() {}
}
class Derived: Base
{
    new public void F() {}
}
```

The new modifier indicates that the F in Derived is “new”, and that it is indeed intended to hide the inherited member.
new 修饰符表示 Derived 中的 F 是“新的”，并且确实 intended to hide the inherited member。

A declaration of a new member hides an inherited member only within the scope of the new member.

新成员的声明仅在其自身作用域内隐藏继承的成员。

```csharp
class Base
{
    public static void F() {}
}
class Derived: Base
{
    new private static void F() {}    // Hides Base.F in Derived only
}
class MoreDerived: Derived
{
    static void G() { F(); }          // Invokes Base.F
}
```

In the example above, the declaration of F in Derived hides the F that was inherited from Base, but since the new F in Derived has private access, its scope does not extend to MoreDerived. Thus, the call F() in MoreDerived.G is valid and will invoke Base.F.
在上面的示例中，Derived 中 F 的声明隐藏了从 Base 继承的 F，但由于 Derived 中的新 F 具有私有访问权限，其作用域不会扩展到 MoreDerived。因此，MoreDerived.G 中对 F() 的调用是有效的，并且会调用 Base.F。

## 3.8 Namespace and type names

Several contexts in a C# program require a namespace-name or a type-name to be specified.

C# 程序中的多个上下文要求指定 namespace-name 或 type-name。

```
namespace-name:
    namespace-or-type-name

type-name:
    namespace-or-type-name

namespace-or-type-name:
    identifier type-argument-list_opt
    namespace-or-type-name . identifier type-argument-list_opt
    qualified-alias-member
```

A namespace-name is a namespace-or-type-name that refers to a namespace. Following resolution as described below, the namespace-or-type-name of a namespace-name must refer to a namespace, or otherwise a compile-time error occurs. No type arguments (§4.4.1) can be present in a namespace-name (only types can have type arguments).
namespace-name 是一个引用命名空间的 namespace-or-type-name。按照下面描述的解析，namespace-name 的 namespace-or-type-name 必须引用一个命名空间，否则会发生编译时错误。namespace-name 中不能存在类型参数（§4.4.1）（只有类型可以具有类型参数）。

A type-name is a namespace-or-type-name that refers to a type. Following resolution as described below, the namespace-or-type-name of a type-name must refer to a type, or otherwise a compile-time error occurs.
type-name 是一个引用类型的 namespace-or-type-name。按照下面描述的解析，type-name 的 namespace-or-type-name 必须引用一个类型，否则会发生编译时错误。

If the namespace-or-type-name is a qualified-alias-member, its meaning is as described in §9.7. Otherwise, a namespace-or-type-name has one of four forms:
如果 namespace-or-type-name 是 qualified-alias-member，则其含义如 §9.7 中所述。否则，namespace-or-type-name 有以下四种形式之一：

- I
- I<A₁, ..., Aₙ>
- N.I
- N.I<A₁, ..., Aₙ>

where I is a single identifier, N is a namespace-or-type-name and <A₁, ..., Aₙ> is an optional type-argument-list. When no type-argument-list is specified, consider K to be zero.
其中 I 是一个标识符，N 是一个 namespace-or-type-name，而 <A₁, ..., Aₙ> 是一个可选的类型参数列表。当未指定类型参数列表时，将 K 视为零。

The meaning of a namespace-or-type-name is determined as follows:
namespace-or-type-name 的含义确定如下：

- If the namespace-or-type-name is of the form I or of the form I<A₁, ..., Aₙ>:
如果 namespace-or-type-name 的形式为 I 或 I<A₁, ..., Aₙ>：

  - If K is zero and the namespace-or-type-name appears within a generic method declaration (§10.6) and if that declaration includes a type parameter (§10.1.3) with name I, then the namespace-or-type-name refers to that type parameter.
  如果 K 为零且 namespace-or-type-name 出现在泛型方法声明（§10.6）中，并且该声明包含名称为 I 的类型参数（§10.1.3），则 namespace-or-type-name 引用该类型参数。

  - Otherwise, if the namespace-or-type-name appears within a type declaration, then for each instance type T (§10.3.1), starting with the instance type of that type declaration and continuing with the instance type of each enclosing class or struct declaration (if any):
  否则，如果 namespace-or-type-name 出现在类型声明中，则对于每个实例类型 T（§10.3.1），从该类型声明的实例类型开始，继续到每个封闭的类或结构体声明（如果有）的实例类型：

    - If K is zero and the declaration of T includes a type parameter with name I, then the *namespace-or-type-name* refers to that type parameter.
    如果 K 为零且 T 的声明包含名称为 I 的类型参数，则 *命名空间或类型名* 引用该类型参数。

    - Otherwise, if the *namespace-or-type-name* appears within the body of the type declaration, and T or any of its base types contain a nested accessible type having name I and K type parameters, then the *namespace-or-type-name* refers to that type constructed with the given type arguments. If there is more than one such type, the type declared within the more derived type is selected. Note that non-type members (constants, fields, methods, properties, indexers, operators, instance constructors, destructors, and static constructors) and type members with a different number of type parameters are ignored when determining the meaning of the *namespace-or-type-name*.
    否则，如果 *命名空间或类型名* 出现在类型声明的主体中，并且 T 或其任何基类型包含名称为 I 且具有 K 个类型参数的嵌套可访问类型，则 *命名空间或类型名* 引用使用给定类型参数构造的该类型。如果存在多个此类类型，则选择在更派生的类型中声明的类型。请注意，非类型成员（常量、字段、方法、属性、索引器、运算符、实例构造函数、析构函数和静态构造函数）以及类型参数数量不同的类型成员在确定 *命名空间或类型名* 的含义时会被忽略。

    - If the previous steps were unsuccessful then, for each namespace N, starting with the namespace in which the *namespace-or-type-name* occurs, continuing with each enclosing namespace (if any), and ending with the global namespace, the following steps are evaluated until an entity is located:
    如果前面的步骤不成功，则对于每个命名空间 N，从 *命名空间或类型名* 出现的命名空间开始，继续到每个封闭的命名空间（如果有），并以全局命名空间结束，以下步骤将被评估直到找到一个实体：

      - If K is zero and I is the name of a namespace in N, then:
      如果 K 为零且 I 是 N 中的命名空间的名称，则：

        - If the location where the *namespace-or-type-name* occurs is enclosed by a namespace declaration for N and the namespace declaration contains an *extern-alias-directive* or *using-alias-directive* that associates the name I with a namespace or type, then the *namespace-or-type-name* is ambiguous and a compile-time error occurs.
        如果 *命名空间或类型名* 出现的位置被 N 的命名空间声明所包含，并且命名空间声明包含一个将名称 I 与命名空间或类型关联的 *extern 别名指令* 或 *using 别名指令*，则 *命名空间或类型名* 是模棱两可的，并且会发生编译时错误。

        - Otherwise, the *namespace-or-type-name* refers to the namespace named I in N.
        否则，*命名空间或类型名* 引用 N 中名为 I 的命名空间。

      - Otherwise, if N contains an accessible type having name I and K type parameters, then:
      否则，如果 N 包含名称为 I 且具有 K 个类型参数的可访问类型，则：

        - If K is zero and the location where the *namespace-or-type-name* occurs is enclosed by a namespace declaration for N and the namespace declaration contains an *extern-alias-directive* or *using-alias-directive* that associates the name I with a namespace or type, then the *namespace-or-type-name* is ambiguous and a compile-time error occurs.
        如果 K 为零且 *命名空间或类型名* 出现的位置被 N 的命名空间声明所包含，并且命名空间声明包含一个将名称 I 与命名空间或类型关联的 *extern 别名指令* 或 *using 别名指令*，则 *命名空间或类型名* 是模棱两可的，并且会发生编译时错误。

        - Otherwise, the *namespace-or-type-name* refers to the type constructed with the given type arguments.
        否则，*命名空间或类型名* 引用使用给定类型参数构造的类型。

      - Otherwise, if the location where the *namespace-or-type-name* occurs is enclosed by a namespace declaration for N:
      否则，如果 *命名空间或类型名* 出现的位置被 N 的命名空间声明所包含：

        - If K is zero and the namespace declaration contains an *extern-alias-directive* or *using-alias-directive* that associates the name I with an imported namespace or type, then the *namespace-or-type-name* refers to that namespace or type.
        如果 K 为零且命名空间声明包含一个将名称 I 与导入的命名空间或类型关联的 *extern 别名指令* 或 *using 别名指令*，则 *命名空间或类型名* 引用该命名空间或类型。

        - Otherwise, if the namespaces imported by the *using-namespace-directives* of the namespace declaration contain exactly one type having name I and K type parameters, then the *namespace-or-type-name* refers to that type constructed with the given type arguments.
        否则，如果命名空间声明的 *using 命名空间指令* 导入的命名空间恰好包含一个名称为 I 且具有 K 个类型参数的类型，则 *命名空间或类型名* 引用使用给定类型参数构造的该类型。

        - Otherwise, if the namespaces imported by the *using-namespace-directives* of the namespace declaration contain more than one type having name I and K type parameters, then the *namespace-or-type-name* is ambiguous and an error occurs.
        否则，如果命名空间声明的 *using 命名空间指令* 导入的命名空间包含多个名称为 I 且具有 K 个类型参数的类型，则 *命名空间或类型名* 是模棱两可的，并且会发生错误。

        - Otherwise, the *namespace-or-type-name* is undefined and a compile-time error occurs.
        否则，*命名空间或类型名* 未定义，并且会发生编译时错误。

      - Otherwise, the *namespace-or-type-name* is of the form N.I or of the form N.I<A₁, ..., Aₖ>. N is first resolved as a *namespace-or-type-name*. If the resolution of N is not successful, a compile-time error occurs. Otherwise, N.I or N.I<A₁, ..., Aₖ> is resolved as follows:
      否则，*命名空间或类型名* 的形式为 N.I 或 N.I<A₁, ..., Aₖ>。首先将 N 解析为 *命名空间或类型名*。如果 N 的解析不成功，则会发生编译时错误。否则，按如下方式解析 N.I 或 N.I<A₁, ..., Aₖ>：

        - If K is zero and N refers to a namespace and N contains a nested namespace with name I, then the *namespace-or-type-name* refers to that nested namespace.
        如果 K 为零且 N 引用一个命名空间并且 N 包含名称为 I 的嵌套命名空间，则 *命名空间或类型名* 引用该嵌套命名空间。
