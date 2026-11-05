
```
class B
{
    static B() {}
    public static int Y = Test.F("Init B");
}
```

输出应为：

```
Init B
Init A
1 1
```

因为在静态构造函数执行时（定义见 §15.12）的规则规定，B 的静态构造函数（因此 B 的静态字段初始值设定项）应在 A 的静态构造函数和字段初始值设定项之前运行。结束示例]

## 15.5.6.3 实例字段初始化

类的实例字段变量初始值设定项对应于一系列赋值操作，这些赋值操作在进入该类的任何一个实例构造函数（§15.11.3）时立即执行。在部分类中，“文本顺序”的含义由 §15.5.6.1 指定。变量初始值设定项按照它们在类声明（§15.5.6.1）中出现的文本顺序执行。类实例创建和初始化过程在 §15.11 中进一步描述。

实例字段的变量初始值设定项不能引用正在创建的实例。因此，在变量初始值设定项中引用 this 会导致编译时错误，因为变量初始值设定项通过简单名称引用任何实例成员也是编译时错误。[示例：在以下代码中

```
class A
{
    int x = 1;
    int y = x + 1;    // Error, reference to instance member of this
}
```

y 的变量初始值设定项导致编译时错误，因为它引用了正在创建的实例的成员。结束示例]

## 15.6 方法

### 15.6.1 通用

方法是一个成员，它实现可由对象或类执行计算或操作。方法使用 method-declarations 声明：

```
method-declaration:
    method-header method-body

method-header:
    attributesopt method-modifiersopt partialopt return-type member-name
        type-parameter-list opt
        ( formal-parameter-list opt ) type-parameter-constraints-clausesopt

method-modifiers:
    method-modifier
    method-modifiers method-modifier
```

```
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
  async

return-type:
  type
  void

member-name:
  identifier
  interface-type . identifier

method-body:
  block
  ;
```

method-declaration 可能会包含一组属性（§22）和四种访问修饰符（§15.3.6）的有效组合，以及 new（§15.3.5）、static（§15.6.3）、virtual（§15.6.4）、override（§15.6.5）、sealed（§15.6.6）、abstract（§15.6.7）、extern（§15.6.8）和 async（§15.15）修饰符。

如果满足以下所有条件，则声明具有修饰符的有效组合：

- 声明包含访问修饰符的有效组合（§15.3.6）。
- 声明不包含相同修饰符多次。
- 声明最多包含以下修饰符之一：static、virtual 和 override。
- 声明最多包含以下修饰符之一：new 和 override。
- 如果声明包含 abstract 修饰符，则声明不包含以下任何修饰符：static、virtual、sealed 或 extern。
- 如果声明包含 private 修饰符，则声明不包含以下任何修饰符：virtual、override 或 abstract。
- 如果声明包含 sealed 修饰符，则声明还包含 override 修饰符。
- 如果声明包含 partial 修饰符，则它不包含以下任何修饰符：new、public、protected、internal、private、virtual、sealed、override、abstract 或 extern。

方法声明的 return-type 指定了方法计算并返回的值的类型。如果方法不返回值，则 return-type 为 void。如果声明包含 partial 修饰符，则返回类型应为 void。

泛型方法是指其声明包含 type-parameter-list 的方法。这指定了方法的类型参数。可选的 type-parameter-constraints-clauses 指定类型参数的约束。method-declaration 除非同时具有 type-parameter-list，否则不得具有 type-parameter-constraints-clauses。显式接口成员实现的 method-declaration 不得具有任何 type-parameter-constraints-clauses。显式接口成员实现的泛型 method-declaration 从接口方法上的约束继承任何约束。同样，具有 override 修饰符的方法声明不得具有任何 type-parameter-constraints-clauses

并且方法的类型参数的约束从被重写虚拟方法继承。member-name 指定方法名称。除非方法是显式接口成员实现（§18.6.2），否则 member-name 只是标识符。对于显式接口成员实现，member-name 由 interface-type 后跟 “.” 和标识符组成。在这种情况下，声明不得包含除（可能）extern 或 async 之外的修饰符。

可选的 formal-parameter-list 指定方法参数（§15.6.2）。

方法声明的 return-type 和 formal-parameter-list 中引用的每个类型应至少与方法本身一样可访问（§8.5.5）。

对于 abstract 和 extern 方法，method-body 仅由分号组成。对于 partial 方法，method-body 可能由分号或块组成。对于所有其他方法，method-body 由块组成，该块指定在调用方法时要执行的语句。

如果 method-body 由分号组成，则声明不得包含 async 修饰符。

方法的名称、类型参数的数量和形式参数列表定义了方法签名（§8.6）。具体来说，方法的签名由其名称、其类型参数的数量以及其形式参数的数量、参数模式修饰符（§15.6.2.1）和类型组成。返回类型不是方法签名的一部分，形式参数的名称、类型参数的名称或约束也不是。 当形式参数类型引用方法的类型参数时，使用类型参数的序数位置（而不是类型参数的名称）进行类型等价。

方法的名称应与同一类中声明的所有其他非方法名称不同。此外，方法的签名应与同一类中声明的所有其他方法的签名不同，并且同一类中声明的两个方法不得仅因 ref 和 out 而签名不同。

方法的 type-parameters 在整个 method-declaration 中处于作用域内，并且可以在该作用域内的 return-type、method-body 和 type-parameter-constraints-clauses 中用于形成类型，但在属性中不能使用。

所有形式参数和类型参数应具有不同的名称。

### 15.6.2 方法参数

### 15.6.2.1 通用

方法的参数（如果有）由方法的 formal-parameter-list 声明。

```
formal-parameter-list:
    fixed-parameters
    fixed-parameters , parameter-array
    parameter-array
fixed-parameters:
    fixed-parameter
    fixed-parameters , fixed-parameter
fixed-parameter:
    attributesopt parameter-modifieropt type identifier default-argumentopt
default-argument:
    = expression
parameter-modifier:
    parameter-mode-modifier
    this
```

```
parameter-mode-modifier:
  ref
  out
```

```
parameter-array:
  attributesopt params array-type identifier
```

形式参数列表由一个或多个以逗号分隔的参数组成，其中只有最后一个可以是 parameter-array。

fixed-parameter 由可选的属性集（§22）；可选的 ref、out 或 this 修饰符；类型；标识符；以及可选的 default-argument 组成。每个 fixed-parameter 声明给定类型和给定名称的参数。this 修饰符将方法指定为扩展方法，并且仅允许在非泛型、非嵌套静态类中的静态方法的第一个参数上使用。扩展方法在 §15.6.10 中进一步描述。具有 default-argument 的 fixed-parameter 称为可选参数，而没有 default-argument 的 fixed-parameter 是必需参数。必需参数在 formal-parameter-list 中不得出现在可选参数之后。

具有 ref、out 或 this 修饰符的参数不能具有 default-argument。default-argument 中的表达式应为以下之一：

- constant-expression
- 形式为 new S() 的表达式，其中 S 是值类型
- 形式为 default(S) 的表达式，其中 S 是值类型

该表达式应可通过标识或可空转换隐式转换为参数的类型。

如果在实现 partial 方法声明（§15.6.9）、显式接口成员实现（§18.6.2）、单参数索引器声明（§15.9）或运算符声明（§15.10.1）中出现可选参数，编译器应发出警告，因为这些成员永远无法以允许省略参数的方式调用。

parameter-array 由可选的属性集（§22）、params 修饰符、array-type 和标识符组成。参数数组声明给定数组类型和给定名称的单个参数。参数数组的 array-type 应为单维数组类型（§17.2）。在方法调用中，参数数组允许指定给定数组类型的单个参数，也允许指定零个或多个数组元素类型的参数。参数数组在 §15.6.2.5 中进一步描述。

parameter-array 可能出现在可选参数之后，但不能具有默认值——对于 parameter-array 省略参数将导致创建空数组。

[示例：以下示例说明了不同种类的参数：

```
public void M(
  ref int i,
  decimal d,
  bool b = false,
  bool? n = false,
  string s = "Hello",
  object o = null,
  T t = default(T),
  params int[] a
) { }
```

在 M 的 formal-parameter-list 中，i 是必需的 ref 参数，d 是必需的值参数，b、s、o 和 t 是可选值参数，a 是参数数组。结束示例

方法声明为参数和类型参数创建单独的声明空间（§8.3）。名称由类型参数列表和形式参数列表引入到此声明空间中
