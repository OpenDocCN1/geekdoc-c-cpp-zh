

### 10.5.5.2 实例字段初始化

类的实例字段变量初始值设定项对应于一系列赋值，这些赋值会在进入该类的任一实例构造函数（§10.11.1）时立即执行。变量初始值设定项按照它们在类声明中出现的文本顺序执行。类实例的创建和初始化过程将在 §10.11 中进一步描述。

实例字段的变量初始值设定项不能引用正在创建的实例。因此，在变量初始值设定项中引用 `this` 会导致编译时错误，因为变量初始值设定项通过简单名称引用任何实例成员也会导致编译时错误。

在以下示例中：

```
class A
{
    int x = 1;
    int y = x + 1; // Error: reference to instance member of this
}
```

`y` 的变量初始值设定项引用了正在创建的实例的成员，因此会导致编译时错误。

## 10.6 方法

*方法*是实现可由对象或类执行的计算或操作的成员。方法使用*方法声明*进行声明：

```
method-declaration:
    method-header  method-body

method-header:
    attributes_opt  method-modifiers_opt  partial_opt  return-type  member-name
        type-parameter-list_opt  (  formal-parameter-list_opt  )
        type-parameter-constraints-clauses_opt

method-modifiers:
    method-modifier
    method-modifiers  method-modifier

method-modifier:
    new
    public
    protected
    internal
    private
    static
    virtual
    sealed
    override
    abstract
    extern

return-type:
    type
    void

member-name:
    identifier
    interface-type  .  identifier

method-body:
    block
    ;
```

*方法声明*可以包含一组特性（§17），以及四种访问修饰符（§10.3.5）和 `new`（§10.3.4）、`static`（§10.6.2）、`virtual`（§10.6.3）、`override`（§10.6.4）、`sealed`（§10.6.5）、`abstract`（§10.6.6）和 `extern`（§10.6.7）修饰符的有效组合。

如果满足以下所有条件，则声明中的修饰符组合有效：

- 声明包含有效的访问修饰符组合（§10.3.5）。
- 声明不包含多次相同的修饰符。
- 声明至多包含以下修饰符中的一个：`static`、`virtual` 和 `override`。
- 声明至多包含以下修饰符中的一个：`new` 和 `override`。
- 如果声明包含 `abstract` 修饰符，则声明不包含以下任何修饰符：`static`、`virtual`、`sealed` 或 `extern`。
- 如果声明包含 `private` 修饰符，则声明不包含以下任何修饰符：`virtual`、`override` 或 `abstract`。
- 如果声明包含 `sealed` 修饰符，则声明也包含 `override` 修饰符。
- 如果声明包含 `partial` 修饰符，则声明不包含以下任何修饰符：`new`、`public`、`protected`、`internal`、`private`、`virtual`、`sealed`、`override`、`abstract` 或 `extern`。

方法声明的*返回类型*指定方法计算并返回的值的类型。如果方法不返回值，则*返回类型*为 `void`。如果声明包含 `partial` 修饰符，则返回类型必须为 `void`。

*成员名称*指定方法的名称。除非方法是显式接口成员实现（§13.4.1），否则*成员名称*就是一个*标识符*。对于显式接口成员实现，*成员名称*由一个*接口类型*、一个“.”和一个*标识符*组成。

可选的*类型参数列表*指定方法的类型参数（§10.1.3）。如果指定了*类型参数列表*，则该方法是*泛型方法*。如果方法包含 `extern` 修饰符，则不能指定*类型参数列表*。

可选的*形式参数列表*指定方法的参数（§10.6.1）。

可选的*类型参数约束子句*指定对各个类型参数的约束（§10.1.5），且只有在同时提供*类型参数列表*并且方法不具有 `override` 修饰符时才能指定。

方法的返回类型以及其形式参数列表中引用的每一种类型，都必须至少具有与方法本身相同的可访问性（§3.5.4）。

对于抽象方法和外部方法，方法体仅由一个分号组成。对于分部方法，方法体可以由一个分号或一个代码块组成。对于所有其他方法，方法体由一个代码块组成，该代码块指定方法被调用时要执行的语句。

方法的名称、类型参数列表和形式参数列表定义了方法的签名（§3.6）。具体而言，方法的签名由其名称、类型参数的数量，以及其形式参数的数量、修饰符和类型组成。就此而言，方法类型中出现的任何方法类型参数，不根据其名称进行标识，而是根据其在方法类型实参列表中的序号位置进行标识。返回类型不属于方法签名，类型参数的名称和形式参数的名称也不属于方法签名。

方法的名称必须不同于同一个类中声明的所有其他非方法的名称。此外，方法的签名必须不同于同一个类中声明的所有其他方法的签名，并且同一个类中声明的两个方法不能仅通过 `ref` 和 `out` 使其签名产生差异。

方法的类型参数在整个*方法声明*中都处于作用域内，并且可以在该作用域内的返回类型、方法体和类型参数约束子句中用于构造类型，但不能在特性中使用。

所有形式参数和类型参数都必须具有不同的名称。

### 10.6.1 方法参数

方法的参数（如果有）通过方法的形式参数列表进行声明。

```
formal-parameter-list:
  fixed-parameters
  fixed-parameters , parameter-array
  parameter-array

fixed-parameters:
  fixed-parameter
  fixed-parameters , fixed-parameter

fixed-parameter:
  attributes_opt parameter-modifier_opt type identifier default-argument_opt

default-argument:
  = expression

parameter-modifier:
  ref
  out
  this

parameter-array:
  attributes_opt params array-type identifier
```

形式参数列表由一个或多个以逗号分隔的参数组成，其中只有最后一个参数可以是参数数组。

固定参数由以下部分组成：可选的一组特性（§17）、可选的 `ref`、`out` 或 `this` 修饰符、一个类型、一个标识符，以及可选的默认实参。每个固定参数都声明一个具有给定类型和名称的参数。`this` 修饰符将方法标记为扩展方法，并且只能用于静态方法的第一个参数。扩展方法将在 §10.6.9 中进一步介绍。

带有默认实参的固定参数称为可选参数，而不带默认实参的固定参数称为必需参数。在形式参数列表中，必需参数不能出现在可选参数之后。

> **克里斯蒂安·纳格尔** 关于版本控制，必须注意可选参数。编译器会获取默认实参，并将其添加到调用方的程序集中。如果默认实参在新版本代码中更改为新值，而调用方代码未重新编译，则调用方仍然包含旧值。

`ref` 或 `out` 参数不能具有默认实参。默认实参中的表达式必须是以下形式之一：

- 常量表达式。
- 形式为 `new S()` 的表达式，其中 `S` 是值类型。
- 形式为 `default(S)` 的表达式，其中 `S` 是值类型。

该表达式必须通过标识转换或可空转换隐式转换为参数的类型。

如果可选参数出现在实现分部方法声明（§10.2.7）、显式接口成员实现（§13.4.1）或单参数索引器声明（§10.9）中，则编译器应发出警告，因为这些成员永远无法以允许省略实参的方式调用。

