
数组的元素可以使用 foreach 语句（§12.9.5）来枚举。

### 16.5 数组成员

每个数组类型都继承 System.Array 类型声明的成员。

### 16.6 数组协变

对于任意两个引用类型 A 和 B，如果存在从 A 到 B 的隐式引用转换（§10.2.8）或显式引用转换（§10.3.5），那么也存在从数组类型 A[R] 到数组类型 B[R] 的相同引用转换，其中 R 是任意给定的秩说明符（但对两个数组类型相同）。这种关系称为数组协变。具体而言，数组协变意味着，如果存在从 B 到 A 的隐式引用转换，则数组类型 A[R] 的值实际上可能是对数组类型 B[R] 实例的引用。

由于数组协变，对引用类型数组元素的赋值包含运行时检查，以确保赋给数组元素的值实际上是允许的类型（§11.18.2）。

*示例：*

```
class Test
{
    static void Fill(object[] array, int index, int count, object value)
    {
        for (int i = index; i < index + count; i++)
        {
            array[i] = value;
        }
    }

    static void Main()
    {
        string[] strings = new string[100];
        Fill(strings, 0, 100, "Undefined");
        Fill(strings, 0, 10, null);
        Fill(strings, 90, 10, 0);
    }
}
```

Fill 方法中对 array[i] 的赋值隐式包含运行时检查，该检查确保 value 要么是 null 引用，要么是对一种对象的引用，该对象的类型与 array 的实际元素类型兼容。在 Main 中，前两次 Fill 调用成功，但第三次调用在执行对 array[i] 的第一次赋值时导致抛出 System.ArrayTypeMismatchException。发生此异常是因为装箱的 int 不能存储在 string 数组中。

*示例结束*

数组协变具体不扩展到值类型数组。例如，不存在允许将 int[] 视为 object[] 的转换。

### 16.7 数组初始值设定项

数组初始值设定项可以在字段声明（§14.5）、局部变量声明（§12.6.2）和数组创建表达式（§11.7.15.5）中指定：

```
array_initializer
  : '{' variable_initializer_list? '}'
  | '{' variable_initializer_list ',' '}'
  ;

variable_initializer_list
  : variable_initializer (',' variable_initializer)*
  ;

variable_initializer
  : expression
  | array_initializer
  ;
```

数组初始值设定项由一系列变量初始值设定项组成，这些变量初始值设定项由“{”和“}”标记包围，并由“,”标记分隔。每个变量初始值设定项是一个表达式，或者对于多维数组而言，是一个嵌套的数组初始值设定项。

使用数组初始值设定项的上下文确定正在初始化的数组的类型。在数组创建表达式中，数组类型紧接在初始值设定项之前，或者从数组初始值设定项中的表达式推断。在字段或变量声明中，数组类型是所声明的字段或变量的类型。当在字段或变量声明中使用数组初始值设定项时，

```
int[] a = {0, 2, 4, 6, 8};
```

它只是等效数组创建表达式的简写：

```
int[] a = new int[] {0, 2, 4, 6, 8};
```

对于一维数组，数组初始值设定项应包含一系列表达式，每个表达式都具有到该数组元素类型的隐式转换（§10.2）。这些表达式按递增顺序初始化数组元素，从索引零处的元素开始。数组初始值设定项中表达式的数量确定正在创建的数组实例的长度。

*示例：* 上面的数组初始值设定项创建一个长度为 5 的 int[] 实例，然后用以下值初始化该实例：

```
a[0] = 0; a[1] = 2; a[2] = 4; a[3] = 6; a[4] = 8;
```

*示例结束*

对于多维数组，数组初始值设定项的嵌套层数应与数组的维数相同。最外层嵌套级别对应最左侧维度，最内层嵌套级别对应最右侧维度。数组每个维度的长度由数组初始值设定项中对应嵌套级别的元素数量确定。对于每个嵌套的数组初始值设定项，其元素数量应与同一级别的其他数组初始值设定项相同。

*示例：* 下面的示例：

```
int[,] b = {{0, 1}, {2, 3}, {4, 5}, {6, 7}, {8, 9}};
```

创建一个二维数组，其最左侧维度的长度为五，最右侧维度的长度为二：

```
int[,] b = new int[5, 2];
```

然后用以下值初始化该数组实例：

```
b[0, 0] = 0; b[0, 1] = 1;
b[1, 0] = 2; b[1, 1] = 3;
b[2, 0] = 4; b[2, 1] = 5;
b[3, 0] = 6; b[3, 1] = 7;
b[4, 0] = 8; b[4, 1] = 9;
```

示例结束

如果除最右侧维度之外的某个维度被指定为长度零，则后续维度也被假定为长度零。

示例：

```
int[,] c = {};
```

创建一个二维数组，其最左侧维度和最右侧维度的长度均为零：

```
int[,] c = new int[0, 0];
```

示例结束

当数组创建表达式同时包含显式维度长度和数组初始值设定项时，这些长度应为常量表达式，并且每个嵌套级别的元素数量应与对应的维度长度匹配。

示例：下面是一些示例：

```
int i = 3;
int[] x = new int[3] {0, 1, 2}; // OK
int[] y = new int[i] {0, 1, 2}; // Error, i not a constant
int[] z = new int[3] {0, 1, 2, 3}; // Error, length/initializer mismatch
```

这里，y 的初始值设定项导致编译时错误，因为维度长度表达式不是常量；z 的初始值设定项导致编译时错误，因为长度与初始值设定项中的元素数量不一致。

示例结束

注意：C# 允许在 array_initializer 末尾使用尾随逗号。此语法为在此类列表中添加或删除成员提供了灵活性，并简化了此类列表的机器生成。注意结束

## 17. 接口

### 17.1 概述

接口定义协定。实现接口的类或结构体应遵守其协定。接口可以继承多个基接口，类或结构体可以实现多个接口。

接口可以包含方法、属性、事件和索引器。接口本身不为其声明的成员提供实现。接口仅指定实现该接口的类或结构体应提供的成员。

### 17.2 接口声明

### 17.2.1 概述

interface_declaration 是一种 type_declaration（§13.7），用于声明新的接口类型。

```
interface_declaration
: attributes? interface_modifier* 'partial'? 'interface'
identifier variant_type_parameter_list? interface_base?
type_parameter_constraints_clause* interface_body ';'?
;
```

interface_declaration 由可选的一组特性（§21）、可选的一组 interface_modifiers（§17.2.2）、可选的 partial 修饰符（§14.2.7）、关键字 interface 和命名该接口的标识符、可选的 variant_type_parameter_list 规范（§17.2.3）、可选的 interface_base 规范（§17.2.4）、可选的 type_parameter_constraints_clauses 规范（§14.2.5）、interface_body（§17.3）以及可选的分号组成。

接口声明不得提供 type_parameter_constraints_clauses，除非它同时提供 type_parameter_list。

提供 type_parameter_list 的接口声明是泛型接口声明。此外，嵌套在泛型类声明或泛型结构体声明中的任何接口本身也是泛型接口声明，因为创建构造类型（§8.4）时应提供包含类型的类型实参。

### 17.2.2 接口修饰符

interface_declaration 可以选择性地包含一系列接口修饰符：

```
interface_modifier
: 'new'
| 'public'
| 'protected'
| 'internal'
| 'private'
| unsafe_modifier // unsafe code support
;
```
