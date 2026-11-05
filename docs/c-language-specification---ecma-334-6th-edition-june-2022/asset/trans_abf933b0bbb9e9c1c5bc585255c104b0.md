
```
class X
{
    A.Stream s1; // Error, A is ambiguous
    A::Stream s2; // Ok
}
```

名称 A 在第二个命名空间体中可能有两种含义，因为类 A 和 using 别名 A 都在作用域内。因此，在限定名 A.Stream 中使用 A 会产生歧义，并导致编译时错误。但是，将 A 与 :: 限定符一起使用不会出错，因为此时 A 仅作为命名空间别名进行查找。

*示例结束*

## 14. 类

### 14.1 概述

类是一种数据结构，可以包含数据成员（常量和字段）、函数成员（方法、属性、事件、索引器、运算符、实例构造函数、终结器和静态构造函数）以及嵌套类型。类类型支持继承，这是一种机制，通过该机制，*派生类* 可以扩展并特化 *基类*。

### 14.2 类声明

#### 14.2.1 概述

一个 *类声明* 是一种 *类型声明*（§13.7），用于声明一个新类。

```
class_declaration
    : attributes? class_modifier* 'partial'? 'class' identifier type_parameter_list?
      class_base? type_parameter_constraints_clause* class_body ';'?
    ;
```

一个 *类声明* 由可选的一组 *属性*（§21）组成，后跟可选的一组 *类修饰符*（§14.2.2），后跟可选的 *partial* 修饰符（§14.2.7），后跟关键字 `class` 和一个命名该类的 *标识符*，后跟可选的 *类型参数列表*（§14.2.3），后跟可选的 *类基* 规范（§14.2.4），后跟可选的一组 *类型参数约束子句*（§14.2.5），后跟一个 *类体*（§14.2.6），并可选地后跟一个分号。

类声明不得提供 *类型参数约束子句*，除非它还提供 *类型参数列表*。

提供 *类型参数列表* 的类声明是泛型类声明。此外，任何嵌套在泛型类声明或泛型结构声明中的类本身也是泛型类声明，因为要创建构造类型（§8.4），必须为包含类型提供类型实参。

### 14.2.2 类修饰符

#### 14.2.2.1 概述

一个 *类声明* 可以选择性地包含一系列类修饰符：

```
class_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'abstract'
    | 'sealed'
    | 'static'
| unsafe_modifier  // unsafe code support
;
```

*unsafe_modifier*（§22.2）仅在 unsafe 代码（§22）中可用。

同一修饰符在类声明中多次出现是编译时错误。

*new* 修饰符允许用于嵌套类。它指定该类隐藏同名的继承成员，如 §14.3.5 所述。*new* 修饰符出现在不是嵌套类声明的类声明上是编译时错误。

*public*、*protected*、*internal* 和 *private* 修饰符控制类的可访问性。根据类声明出现的上下文，其中一些修饰符可能不被允许（§7.5.2）。

当分部类型声明（§14.2.7）包含可访问性规范（通过 *public*、*protected*、*internal* 和 *private* 修饰符）时，该规范应与包含可访问性规范的所有其他部分一致。如果分部类型的任何部分都不包含可访问性规范，则为该类型赋予适当的默认可访问性（§7.5.2）。

*abstract*、*sealed* 和 *static* 修饰符将在以下子句中讨论。

#### 14.2.2.2 抽象类

*abstract* 修饰符用于指示类是不完整的，并且仅打算用作基类。*抽象类* 与 *非抽象类* 的区别如下：

- *抽象类* 不能直接实例化，对抽象类使用 *new* 运算符是编译时错误。虽然可以拥有编译时类型为抽象类的变量和值，但这些变量和值必然要么为 *null*，要么包含对派生自抽象类型的非抽象类实例的引用。
- 允许（但不要求）*抽象类* 包含抽象 *成员*。
- *抽象类* 不能被密封。

当非抽象类派生自抽象类时，该非抽象类应包含所有继承的抽象成员的实际实现，从而重写这些抽象成员。

*示例：* 在以下代码中

```
abstract class A
{
    public abstract void F();
}

abstract class B : A
{
    public void G() {}
}

class C : B
{
    public override void F()
    {
        // Actual implementation of F
    }
}
```

#### 14.2.2.4 引用静态类类型

如果满足以下条件，则允许 namespace_or_type_name（§7.8）引用静态类：

- namespace_or_type_name 是形式为 T . I 的 namespace_or_type_name 中的 T，或者
- namespace_or_type_name 是形式为 typeof(T) 的 typeof_expression（§11.7.16）中的 T。

如果满足以下条件，则允许 primary_expression（§11.7）引用静态类：

- primary_expression 是形式为 E . I 的 member_access（§11.7.6）中的 E。

在任何其他上下文中，引用静态类都是编译时错误。

> *注意：* 例如，将静态类用作基类、成员的构成类型（§14.3.7）、泛型类型实参或类型参数约束都是错误。同样，静态类不能用于数组类型、指针类型、new 表达式、强制转换表达式、is 表达式、as 表达式、sizeof 表达式或默认值表达式。 注释结束

### 14.2.3 类型参数

类型参数是一个简单标识符，表示用于创建构造类型时所提供的类型实参的占位符。相比之下，类型实参（§8.4.2）是在创建构造类型时替换类型参数的类型。

```
type_parameter_list
  : '<' type_parameters '>'
  ;

type_parameters
  : attributes? type_parameter
  | type_parameters ',' attributes? type_parameter
  ;
```

type_parameter 在 §8.5 中定义。

类声明中的每个类型参数都在该类的声明空间（§7.3）中定义一个名称。因此，它不能与该类的另一个类型参数或该类中声明的成员同名。类型参数不能与该类型本身同名。

如果两个分部泛型类型声明（在同一程序中）具有相同的完全限定名（其中包含用于表示类型参数数量的 generic_dimension_specifier（§11.7.16））（§7.8.3），则它们构成同一个未绑定泛型类型。两个这样的分部类型声明应按顺序为每个类型参数指定相同的名称。

### 14.2.4 类基规范

#### 14.2.4.1 概述

类声明可以包含 class_base 规范，它定义该类的直接基类以及该类直接实现的接口（§17）。

```
class_base
  : ':' class_type
  | ':' interface_type_list
  | ':' class_type ',' interface_type_list
  ;
```

interface_type_list

```
: interface_type (',' interface_type)*
;
```

#### 14.2.4.2 基类

当 class_type 包含在 class_base 中时，它指定正在声明的类的直接基类。如果非分部类声明没有 class_base，或者 class_base 仅列出接口类型，则假定直接基类为 object。当分部类声明包含基类规范时，该基类规范应引用与该分部类型中包含基类规范的所有其他部分相同的类型。如果分部类的任何部分都不包含基类规范，则基类为 object。类从其直接基类继承成员，如 §14.3.4 所述。

示例：在以下代码中

```
class A {}
class B : A {}
```

类 A 被称为 B 的直接基类，而 B 被称为派生自 A。由于 A 未显式指定直接基类，其直接基类隐式为 object。

示例结束

对于构造类类型（包括在泛型类型声明（§14.3.9.7）内声明的嵌套类型），如果在泛型类声明中指定了基类，则通过将基类声明中的每个 type_parameter 替换为构造类型对应的 type_argument，来获得该构造类型的基类。

示例：给定以下泛型类声明

```
class B<U,V> {...}
class G<T> : B<string,T[]> {...}
```

构造类型 G<int> 的基类将是 B<string,int[]>。

示例结束

类声明中指定的基类可以是构造类类型（§8.4）。基类本身不能是类型参数（§8.5），但它可以涉及作用域内的类型参数。

示例：

```
class Base<T> {}
class Extend : Base<int>    // Valid, non-constructed class with constructed base
class Extend<V> : V {}      // Error, type parameter used as base class
class Extend<V> : Base<V> {} // Valid, type parameter used as type argument for base
```

示例结束

类类型的直接基类型应至少与类类型本身具有相同的可访问性（§7.5.5）。例如，public 类派生自 private 或 internal 类是编译时错误。

类类型的直接基类不得为以下任何类型：System.Array、System.Delegate、System.Enum 或 System.ValueType。此外，泛型类声明不得将 System.Attribute 用作直接或间接基类（§21.2.1）。

在确定类 B 的直接基类规范 A 的含义时，暂时假定 B 的直接基类为 object，这确保基类规范的含义不能递归地依赖于自身。
