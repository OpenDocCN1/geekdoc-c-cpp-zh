

```
data: T;
next: Stack;
end record;
function top( s: Stack ) return T ;
end Stacks;
```

请注意 **Stack** 数据类型和包名并不相同，并且 **top** 函数在这里也被声明（但未实现），因为它是对同一类型 T 参数化的。该包规范需要一个关联的 **package body** 来提供 top 函数的实际实现：

```
package body Stacks is
    function top( s: Stack ) return T is
    begin
        return s.data;
    end top;
end Stacks;
```

现在此 Stacks 包可以按如下方式被程序使用：

```
with Stacks; -- import the Stacks package
...
package IntStacks is new Stacks(integer);
    -- instantiate the parameterized package
    -- with type integer

use IntStacks;
    -- without this, we must use the package name
    -- before all of its components, e.g.
    -- IntStacks.Stack,
    -- IntStacks.StackNode, IntStacks.pop, etc.

s : Stack := new StackNode;
t : integer;
...
s.data := 3;
s.next := null;
t := top(s); -- t is now 3
```

显式参数化的多态函数也可以使用 Ada 的通用单元来定义，但由于函数本身就是编译单元，因此不需要包（除非我们想在同一位置同时定义多个函数）。例如，以下是前面示例中 max 函数在 Ada 中的规范：

```
generic
    type T is private;
    with function gt(x, y : T) return boolean;
function max (x, y : T) return T;
```

请注意，我们并没有将 gt 函数作为 max 函数本身的参数，而是将其作为单元的“通用”参数包含在内；这是显式约束的参数多态，与 C++ 的隐式约束多态不同，它明确表明 max 函数依赖于 gt 函数，即使它不在函数调用本身的参数列表中。

max 函数单元也需要一个主体，在其中编写 max 函数的实际代码：

```
-- body of max unit
function max (x,y:T) return T is
begin
if gt(x,y) then return x;
    else return y;
    end if;
end max;
```

现在 max 函数可以按如下方式被 Ada 程序使用：

```
with max; -- import the max unit
---
function maxint is new max(integer,">");
-- instantiate the max function for integers,
-- using the ">" function as the gt function.

i: integer;
---
i := maxint(1,2); -- i is now 2
```

正如 Ada 通常所体现的那样，代码中必须显式完成所有操作。也就是说，多态必须始终是显式的，参数化必须使所有依赖关系显式化，实例化也必须显式化。这甚至需要一个新的名称——例如上面的 maxint。

## 8.10 案例研究：TinyAda 中的类型检查

在第 7.8 节中，我们为 TinyAda 解析器添加了静态语义分析的代码。在该代码中，标识符会被检查以确保它们在使用前已声明，并且在同一块中不会被重复声明。此外，当标识符被声明时，其作为常量、变量、过程或类型名的角色会被记录下来。此信息用于确保标识符在适当上下文中被引用。

在本节中，我们开发并部分实现了解析器中类型检查的设计。如前所述，这将涉及在标识符被声明时向符号表添加新信息，并在标识符被引用时查找该信息以强制执行语义限制。

### 8.10.1 类型兼容性、类型等价性和类型描述符

对于 TinyAda 这种静态类型语言，解析器必须在标识符被引用时检查其类型。其中许多检查发生在标识符作为表达式的操作数时。例如，在 TinyAda 表达式 X + 1 中，变量 X 必须是 INTEGER 类型或 INTEGER 的子范围类型，而在表达式 not (A or B) 中，变量 A 和 B 必须是 BOOLEAN 类型。因此，允许在表达式操作数中出现的标识符的类型，必须是操作符所要求的类型。此外，由于操作数本身也可以是任何表达式，因此每个表达式也必须具有类型。例如，表达式 not (A or B) 中的子表达式 A or B 必须是 BOOLEAN 类型。

限制标识符和表达式类型的另一个上下文因素是它们在赋值语句中的位置或作为过程调用的实际参数。赋值语句左侧的名称必须与右侧的表达式类型兼容。传递给过程调用作为实际参数的表达式或名称必须与该过程声明中对应的形式参数类型兼容。

最后，声明中某些元素的类型也受到限制。例如，数组类型定义的索引类型必须是序数类型 BOOLEAN 或 CHAR 或 INTEGER 的子范围。

TinyAda 使用一种松散的名称等价形式来确定两个标识符（或表达式）是否类型兼容。在数组和枚举的情况下，这意味着两个标识符如果且仅当它们在声明中使用相同的类型名声明时才是类型兼容的。对于内置类型 INTEGER、CHAR 和 BOOLEAN 及其程序员定义的子范围类型而言，两个标识符如果且仅当它们的超类型名称等价时才是类型兼容的。例如，以下声明中类型名 INDEX 的超类型是 INTEGER：

```
type INDEX is range 1 .. 10;
```

INTEGER 的超类型是其自身；因此，INDEX 类型的变量与 INTEGER 类型的变量是类型兼容的，因为它们的超类型相同。从关于类型兼容性和类型等价性的这些基本事实出发，可以推导出 TinyAda 解析器中类型检查的规则。

用于表示类型属性的主要数据结构称为类型描述符。当对应的类型名被引入时，会将给定类型的类型描述符输入到符号表中。这在程序启动时对内置类型名 BOOLEAN、CHAR 和 INTEGER 发生，并在随后遇到新的类型声明时发生。当遇到标识符引用或表达式并检查其类型时，解析器要么比较两个操作数的类型描述符，要么将给定的类型描述符与期望的描述符进行比较。当需要严格的名称等价时（针对数组或枚举），两个类型描述符必须是完全相同的对象。否则（针对内置序数类型及其子范围），两个类型描述符必须具有完全相同的超类型描述符。这些规则自然地导出了本节后面出现的若干类型检查方法的实现。

### 8.10.2 类型描述符类的设计与使用

从概念上讲，类型描述符就像一个变体记录，其包含的信息取决于所描述的数据类型类别。以下是 TinyAda 中每种类别数据类型的类型描述符所包含的信息。

- 1. 每个类型描述符都包含一个称为 **type form** 的字段，其可能取值为 ARRAY、ENUM、SUBRANGE 和 NONE。该字段用于标识数据类型的类别，并允许用户访问其特定属性。
- 2. 数组类型描述符包含索引类型和元素类型的属性。这些属性也是类型描述符。
- 3. 枚举类型描述符包含该类型枚举常量名称的符号条目列表。
- 4. 子范围类型的类型描述符（包括 BOOLEAN、CHAR 和 INTEGER）包含下界和上界的值，以及超类型的类型描述符。

Java 中没有变体记录结构来表示此信息，但我们可以用 TypeDescriptor 类和三个子类 ArrayDescriptor、SubrangeDescriptor 和 EnumDescriptor 很方便地对其建模。顶层类包含 type form，在创建任何子类的实例时会自动设置。子类包含刚才列出的信息，其中记录和枚举类型的表示合并到一个类中。每个类还包含用于设置其属性的方法。用户可以直接将其作为公共字段访问。这些类的完整实现可在本书网站上获得。

在程序启动时，解析器现在为三种内置类型创建类型描述符。这些描述符被声明为解析器的实例变量，以便于访问，并且因为它们将成为所有子范围类型的唯一超类型。我们定义了一个新方法来初始化这些对象，并更新另一个方法以将它们作为类型附加到 TinyAda 的内置标识符上。以下是这些更改的代码：

```
// Built-in type descriptors, globally accessible within the parser
private SubrangeDescriptor BOOL_TYPE, CHAR_TYPE, INT_TYPE;

// Sets up the type information for the built-in type descriptors
private void initTypeDescriptors() {
    BOOL_TYPE = new SubrangeDescriptor();
    BOOL_TYPE.setLowerAndUpper(0, 1);
    BOOL_TYPE.setSuperType(BOOL_TYPE);
    CHAR_TYPE = new SubrangeDescriptor();
    CHAR_TYPE.setLowerAndUpper(0, 127);
    CHAR_TYPE.setSuperType(CHAR_TYPE);
    INT_TYPE = new SubrangeDescriptor();
    INT_TYPE.setLowerAndUpper(Integer.MIN_VALUE, Integer.MAX_VALUE);
```

