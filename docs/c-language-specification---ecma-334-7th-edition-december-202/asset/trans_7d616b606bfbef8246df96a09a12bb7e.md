
这允许上下文跟踪在其下运行着多少个返回 void 的异步函数，并决定如何传播从这些函数中产生的异常。

## 16. 结构体

### 16.1 概述

结构体与类相似，因为它们表示可以包含数据成员和函数成员的数据结构。然而，与类不同，结构体是值类型，不需要堆分配。结构体类型的变量直接包含结构体的数据，而类类型的变量包含对数据的引用，后者称为对象。

> 注意：结构体对于具有值语义的小型数据结构特别有用。复数、坐标系中的点或字典中的键值对都是结构体的良好示例。这些数据结构的要点在于它们的数据成员很少，不需要使用继承或引用语义，而是可以方便地使用值语义实现，其中赋值复制值而不是引用。结束注释

如 §8.3.5 所述，C# 提供的简单类型（例如 int、double 和 bool）实际上都是结构体类型。

### 16.2 结构体声明

### 16.2.1 概述

struct_declaration 是一种 type_declaration（§14.7），它声明一个新的结构体：

```
struct_declaration
: attributes? struct_modifier* 'ref'? 'partial'? 'struct'
identifier type_parameter_list? struct_interfaces?
type_parameter_constraints_clause* struct_body ';'?
```

struct_declaration 由可选的一组特性（§22）组成，随后是可选的一组 struct_modifiers（§16.2.2），随后是可选的 ref 修饰符（§16.2.3），随后是可选的 partial 修饰符（§15.2.7），随后是关键字 struct 和命名该结构体的标识符，随后是可选的 type_parameter_list 规范（§15.2.3），随后是可选的 struct_interfaces 规范（§16.2.5），随后是可选的 type_parameter_constraints_clauses 规范（§15.2.5），随后是 struct_body（§16.2.6），可选后跟分号。

结构体声明不得提供 type_parameter_constraints_clauses，除非它还提供 type_parameter_list。

提供 type_parameter_list 的结构体声明是泛型结构体声明。此外，在泛型类声明或泛型结构体声明中嵌套的任何结构体本身也是泛型结构体声明，因为创建构造类型（§8.4）时必须提供包含类型的类型实参。

包含 ref 关键字的结构体声明不得具有 struct_interfaces 部分。

### 16.2.2 结构体修饰符

struct_declaration 可以选择性地包含一系列 struct_modifiers：

```
struct_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'readonly'
  | unsafe_modifier  // unsafe code support
  ;
```

unsafe_modifier（§23.2）仅在 unsafe 代码（§23）中可用。

同一修饰符在结构体声明中多次出现属于编译时错误。

除 readonly 外，结构体声明的修饰符与类声明的修饰符（§15.2.2）含义相同。

readonly 修饰符指示 struct_declaration 声明一个其实例不可变的类型。

readonly 结构体具有以下约束：
- 它的每个实例字段也都应声明为 readonly。
- 它的任何实例属性都不得具有 set_accessor_declaration（§15.7.3）。
- 它不得声明任何类似字段的事件（§15.8.2）。

当 readonly 结构体的实例传递给方法时，其 this 被视为 in 实参/形参，这不允许对任何实例字段进行写访问（构造函数除外）。

### 16.2.3 ref 修饰符

ref 修饰符指示 struct_declaration 声明一个其实例分配在执行栈上的类型。这些类型称为 ref 结构体类型。ref 修饰符声明实例可以包含类似 ref 的字段，并且不得复制出其安全上下文（§16.4.12）。确定 ref 结构体安全上下文的规则在 §16.4.12 中描述。

如果 ref 结构体类型用于以下任何上下文，则属于编译时错误：
- 作为数组的元素类型。
- 作为不具有 ref 修饰符的类或结构体的字段的声明类型。
- 被装箱到 System.ValueType 或 System.Object。
- 作为类型实参。
- 作为元组元素的类型。
- 异步方法。
- 迭代器。
- 不存在从 ref 结构体类型到 object 类型或 System.ValueType 类型的转换。
- 不得将 ref 结构体类型声明为实现任何接口。
- 在 object 或 System.ValueType 中声明但未在 ref 结构体类型中重写的实例方法，不得使用该 ref 结构体类型的接收者来调用。
- ref 结构体类型的实例方法不得被方法组转换为委托类型所捕获。
- ref 结构体不得由 lambda 表达式或局部函数捕获。

> 注意：ref 结构体不得声明异步实例方法，也不得在实例方法内使用 yield return 或 yield break 语句，因为隐式 this 参数不能在这些上下文中使用。结束注释

这些约束确保 ref 结构体类型的变量不会引用不再有效的栈内存，也不会引用不再有效的变量。

### 16.2.4 partial 修饰符

partial 修饰符指示此 struct_declaration 是分部类型声明。在封闭命名空间或类型声明中，具有相同名称的多个分部结构体声明按照 §15.2.7 中指定的规则合并形成一个结构体声明。

### 16.2.5 结构体接口

结构体声明可以包含 struct_interfaces 规范，在这种情况下，称该结构体直接实现给定的接口类型。对于构造的结构体类型（包括在泛型类型声明（§15.3.9.7）中声明的嵌套类型），每个实现的接口类型都是通过以下方式获得的：对于给定接口中的每个 type_parameter，替换为构造类型对应的 type_argument。

```
struct_interfaces
  : ':' interface_type_list
  ;
```

关于分部结构体声明（§15.2.7）多个部分上的接口处理，将在 §15.2.4.3 中进一步讨论。

接口实现将在 §18.6 中进一步讨论。

### 16.2.6 结构体主体

结构体的 struct_body 定义该结构体的成员。

```
struct_body
  : '{' struct_member_declaration* '}'
  ;
```

### 16.3 结构体成员

结构体的成员由 struct_member_declarations 引入的成员以及从 System.ValueType 类型继承的成员组成。

```
struct_member_declaration
  : constant_declaration
  | field_declaration
  | method_declaration
  | property_declaration
  | event_declaration
  | indexer_declaration
  | operator_declaration
  | constructor_declaration
```

```
| static_constructor_declaration
| type_declaration
| fixed_size_buffer_declaration  // unsafe code support
;
```

fixed_size_buffer_declaration（§23.8.2）仅在 unsafe 代码（§23）中可用。

> 注意：除 finalizer_declaration 之外，所有种类的 class_member_declarations 也都是 struct_member_declarations。结束注释

除 §16.4 中指出的差异外，§15.3 至 §15.12 中提供的类成员描述也适用于结构体成员。

### 16.4 类与结构体的差异

### 16.4.1 概述

结构体在几个重要方面与类不同：
- 结构体是值类型（§16.4.2）。
- 所有结构体类型都隐式继承自 System.ValueType 类（§16.4.3）。
- 对结构体类型的变量进行赋值会创建所赋值的副本（§16.4.4）。
- 结构体的默认值是将所有字段设置为其默认值后产生的值（§16.4.5）。
- 装箱和拆箱操作用于在结构体类型与某些引用类型之间进行转换（§16.4.6）。
- this 的含义在结构体成员内有所不同（§16.4.7）。
- 结构体的实例字段声明不允许包含变量初始值设定项（§16.4.8）。
- 不允许结构体声明无参数实例构造函数（§16.4.9）。
- 不允许结构体声明终结器。

### 16.4.2 值语义

结构体是值类型（§8.3），称为具有值语义。另一方面，类是引用类型（§8.2），称为具有引用语义。

结构体类型的变量直接包含结构体的数据，而类类型的变量包含对包含该数据的对象的引用。当结构体 B 包含类型为 A 的实例字段且 A 是结构体类型时，A 依赖 B 或依赖由 B 构造的类型属于编译时错误。如果结构体 X 包含类型为 Y 的实例字段，则结构体 X 直接依赖结构体 Y。根据此定义，一个结构体所依赖的完整结构体集合是“直接依赖”关系的传递闭包。

示例：

```
struct Node
{
    int data;
    Node next; // error, Node directly depends on itself
}
```
