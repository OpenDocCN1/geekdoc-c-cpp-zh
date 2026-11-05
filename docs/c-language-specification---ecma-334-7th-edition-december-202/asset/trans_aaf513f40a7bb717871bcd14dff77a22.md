
```
| 'static'
| 'virtual'
| 'sealed'
| 'override'
| 'abstract'
| 'extern'
| unsafe_modifier  // unsafe code support
;
```

```
property_body
: '{' accessor_declarations '}' property_initializer?
| '=>' expression ';'
;
```

```
property_initializer
: '=' variable_initializer ';'
;
```

```
ref_property_body
: '{' ref_get_accessor_declaration '}'
| '=>' ref_variable_reference ';'
;
```

unsafe_modifier（§23.2）仅在 unsafe 代码（§23）中可用。

property_declaration 有两种：

- 第一种声明非 ref 值属性。其值的类型为 type。此类属性可以是可读的和/或可写的。
- 第二种声明 ref 值属性。其值是一个 variable_reference（§9.5），它可能是只读的，指向类型为 type 的变量。此类属性仅可读。

property_declaration 可以包含一组特性（§22），以及所允许的任意一种已声明可访问性（§15.3.6）、new（§15.3.5）、static（§15.7.2）、virtual（§15.6.4、§15.7.6）、override（§15.6.5、§15.7.6）、sealed（§15.6.6）、abstract（§15.6.7、§15.7.6）和 extern（§15.6.8）修饰符。

就修饰符的有效组合而言，属性声明遵循与方法声明（§15.6）相同的规则。

member_name（§15.6.1）指定属性的名称。除非该属性是显式接口成员实现，否则 member_name 只是一个标识符。对于显式接口成员实现（§18.6.2），member_name 由 interface_type、后跟“.”和一个标识符组成。

属性的类型应至少与属性本身同样可访问（§7.5.5）。

property_body 可以由语句体或表达式体组成。在语句体中，accessor_declarations（应包含在“{”和“}”标记中）声明属性的访问器（§15.7.3）。访问器指定与读取和写入属性相关联的可执行语句。

在 property_body 中，由 => 后跟表达式 E 和分号组成的表达式体完全等价于语句体 { get { return E; } }，因此只能用于指定只读属性，其中 get 访问器的结果由单个表达式给出。

property_initializer 只能为自动实现的属性（§15.7.4）指定，并且会使用表达式给定的值初始化此类属性的基础字段。

ref_property_body 可以由语句体或表达式体组成。在语句体中，get_accessor_declaration 声明属性的 get 访问器（§15.7.3）。该访问器指定与读取属性相关联的可执行语句。

在 ref_property_body 中，由 => 后跟 ref、一个 variable_reference V 和分号组成的表达式体完全等价于语句体 { get { return ref V; } }。

> 注意：尽管访问属性的语法与访问字段的语法相同，但属性不归类为变量。因此，不能将属性作为 in、out 或 ref 实参传递，除非该属性是 ref 值属性，并因此返回变量引用（§9.7）。注释结束。

当属性声明包含 extern 修饰符时，该属性称为外部属性。由于外部属性声明不提供实际实现，其每个 accessor_declarations 都由一个分号组成。

## 15.7.2 静态属性和实例属性

当属性声明包含 static 修饰符时，该属性称为静态属性。当不存在 static 修饰符时，该属性称为实例属性。

静态属性不与特定实例关联，在静态属性的访问器中引用 this 是编译时错误。

实例属性与类的给定实例关联，并且可以在该属性的访问器中通过 this（§12.8.13）访问该实例。

静态成员与实例成员之间的差异将在 §15.3.8 中进一步讨论。

## 15.7.3 访问器

> 注意：本条款同时适用于属性（§15.7）和索引器（§15.9）。本条款以属性的措辞编写；在阅读索引器相关内容时，请将 property/properties 替换为 indexer/indexers，并参阅 §15.9.2 中给出的属性与索引器之间的差异列表。注释结束。

属性的 accessor_declarations 指定与写入和/或读取该属性相关联的可执行语句。

```
accessor_declarations
  : get_accessor_declaration set_accessor_declaration?
  | set_accessor_declaration get_accessor_declaration?
  ;

get_accessor_declaration
  : attributes? accessor_modifier? 'get' accessor_body
  ;

set_accessor_declaration
  : attributes? accessor_modifier? 'set' accessor_body
  ;

accessor_modifier
  : 'protected'
  | 'internal'
  | 'private'
  | 'protected' 'internal'
  | 'internal' 'protected'
  | 'protected' 'private'
  | 'private' 'protected'
  ;
```

```
accessor_body
: block
| '=>' expression ';'
| ';'
;

ref_get_accessor_declaration
: attributes? accessor_modifier? 'get' ref_accessor_body
;

ref_accessor_body
: block
| '=>' 'ref' variable_reference ';'
| ';'
;
```

accessor_declarations 由一个 get_accessor_declaration、一个 set_accessor_declaration 或两者组成。每个访问器声明由可选特性、可选 accessor_modifier、标记 get 或 set，以及后跟的 accessor_body 组成。

对于 ref 值属性，ref_get_accessor_declaration 由可选特性、可选 accessor_modifier、标记 get，以及后跟的 ref_accessor_body 组成。

accessor_modifier 的使用受以下限制约束：

- accessor_modifier 不得用于接口中或显式接口成员实现中。
- 对于没有 override 修饰符的属性或索引器，只有当该属性或索引器同时具有 get 和 set 访问器时，才允许使用 accessor_modifier，并且只允许在其中一个访问器上使用。
- 对于包含 override 修饰符的属性或索引器，访问器应匹配被重写访问器的 accessor_modifier（如果有）。
- accessor_modifier 声明的可访问性应严格限制于属性或索引器本身已声明的可访问性。具体而言：
  - 如果属性或索引器的已声明可访问性为 public，则 accessor_modifier 声明的可访问性可以是 private protected、protected internal、internal、protected 或 private。
  - 如果属性或索引器的已声明可访问性为 protected internal，则 accessor_modifier 声明的可访问性可以是 private protected、protected private、internal、protected 或 private。
  - 如果属性或索引器的已声明可访问性为 internal 或 protected，则 accessor_modifier 声明的可访问性应为 private protected 或 private。
  - 如果属性或索引器的已声明可访问性为 private protected，则 accessor_modifier 声明的可访问性应为 private。
  - 如果属性或索引器的已声明可访问性为 private，则不得使用任何 accessor_modifier。

对于 abstract 和 extern 的非 ref 值属性，所指定的每个访问器的 accessor_body 都只是一个分号。非 abstract、非 extern 的属性（但不是索引器）也可以将所有指定访问器的 accessor_body 设为分号，此时它是自动实现的属性（§15.7.4）。自动实现的属性应至少具有一个 get 访问器。对于任何其他非 abstract、非 extern 属性的访问器，accessor_body 是以下之一：

- 一个块，指定调用相应访问器时要执行的语句；或
- 一个表达式体，由 => 后跟一个表达式和分号组成，表示调用相应访问器时要执行的单个表达式。

对于 abstract 和 extern 的 ref 值属性，ref_accessor_body 只是一个分号。对于任何其他非 abstract、非 extern 属性的访问器，ref_accessor_body 是以下之一：

- 一个块，指定调用 get 访问器时要执行的语句；或
- 一个表达式体，由 => 后跟 ref、一个 variable_reference 和分号组成。变量引用在调用 get 访问器时求值。

非 ref 值属性的 get 访问器对应于一个无参数方法，其返回值为该属性的类型。除非作为赋值目标，否则在表达式中引用此类属性时，会调用其 get 访问器来计算该属性的值（§12.2.2）。

非 ref 值属性的 get 访问器体应符合 §15.6.11 中所述的值返回方法的规则。特别是，get 访问器体中的所有 return 语句都应指定一个可隐式转换为该属性类型的表达式。此外，get 访问器的端点不可到达。

ref 值属性的 get 访问器对应于一个无参数方法，其返回值为指向该属性类型的变量的 variable_reference。当在表达式中引用此类属性时，会调用其 get 访问器来计算该属性的 variable_reference 值。然后，该变量引用像任何其他变量引用一样，用于读取所引用的变量，或者在非只读 variable_reference 的情况下，根据上下文要求写入所引用的变量。

示例：以下示例说明将 ref 值属性作为赋值目标：

```csharp
class Program
{
    static int field;
    static ref int Property => ref field;

    static void Main()
    {
        field = 10;
        Console.WriteLine(Property); // Prints 10
        Property = 20;               // This invokes the getter, then assigns
                                     // via the resulting variable reference
        Console.WriteLine(field);    // Prints 20
    }
}
```

示例结束

ref 值属性的 get 访问器体应符合 §15.6.11 中所述的 ref 值方法的规则。

set 访问器对应于一个方法，该方法具有一个属性类型的值参数和 void 返回类型。set 访问器的隐式参数始终命名为 value。当属性为
