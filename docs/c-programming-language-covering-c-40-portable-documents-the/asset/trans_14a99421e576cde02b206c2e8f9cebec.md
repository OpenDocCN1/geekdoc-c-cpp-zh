
前两个运算符声明是允许的，因为就 §10.9.3 而言，T 分别与 int 和 string 没有关系；在这两种情况下，它们被视为唯一类型。但是，第三个运算符是错误的，因为 C<T> 是 D<T> 的基类。

由第二条规则可知，转换运算符必须转换为声明该运算符的类或结构类型，或者从该类型转换。例如，类或结构类型 C 可以定义从 C 到 int 以及从 int 到 C 的转换，但不能定义从 int 到 bool 的转换。

不能直接重新定义预定义转换。因此，不允许转换运算符从 object 转换或转换为 object，因为 object 与所有其他类型之间已经存在隐式转换和显式转换。同样，转换的源类型和目标类型都不能是对方的基类型，因为此时转换已经存在。

但是，可以在泛型类型上声明运算符，这些运算符在特定类型实参下指定已作为预定义转换存在的转换。在示例

```csharp
struct Convertible<T>
{
    public static implicit operator Convertible<T>(T value) {...}
    public static explicit operator T(Convertible<T> value) {...}
}
```

当将类型 object 指定为 T 的类型实参时，第二个运算符声明了一个已存在的转换（从任何类型到类型 object 存在隐式转换，因此也存在显式转换）。

如果两个类型之间存在预定义转换，则忽略这些类型之间的任何用户定义转换。具体而言：

- 如果存在从类型 S 到类型 T 的预定义隐式转换（§6.1），则忽略从 S 到 T 的所有用户定义转换（隐式或显式）。
- 如果存在从类型 S 到类型 T 的预定义显式转换（§6.2），则忽略从 S 到 T 的任何用户定义显式转换。此外：
  - 如果 T 是接口类型，则忽略从 S 到 T 的用户定义隐式转换。
  - 否则，仍考虑从 S 到 T 的用户定义隐式转换。

对于除 object 之外的所有类型，上面由 Convertible<T> 类型声明的运算符不会与预定义转换冲突。例如：

```csharp
void F(int i, Convertible<int> n) {
    i = n;          // Error
    i = (int)n;     // User-defined explicit conversion
    n = i;          // User-defined implicit conversion
    n = (Convertible<int>)i; // User-defined implicit conversion
}
```

但是，对于类型 object，预定义转换在除一种情况外的所有情况下都隐藏用户定义转换：

```csharp
void f(object o, Convertible<object> n) {
    o = n;        // Predefined boxing conversion
    o = (object)n; // Predefined boxing conversion
    n = o;        // User-defined implicit conversion
    n = (Convertible<object>)o; // Predefined unboxing conversion
}
```

不允许用户定义转换从接口类型转换或转换为接口类型。具体而言，此限制确保在转换为接口类型时不发生用户定义转换，并且仅当被转换的对象实际实现指定接口类型时，到接口类型的转换才会成功。

转换运算符的签名由源类型和目标类型组成。（请注意，这是返回类型参与签名的唯一成员形式。）转换运算符的隐式或显式分类不属于运算符的签名。因此，类或结构不能声明具有相同源类型和目标类型的隐式转换运算符和显式转换运算符。

通常，用户定义隐式转换应设计为从不引发异常且从不丢失信息。如果用户定义转换可能引发异常（例如，因为源参数超出范围）或丢失信息（例如丢弃高位），则该转换应定义为显式转换。

在示例

```csharp
using System;
public struct Digit
{
    byte value;

    public Digit(byte value) {
        if (value < 0 || value > 9) throw new ArgumentException();
        this.value = value;
    }
    public static implicit operator byte(Digit d) {
        return d.value;
    }
    public static explicit operator Digit(byte b) {
        return new Digit(b);
    }
}
```

从 Digit 到 byte 的转换是隐式的，因为它从不引发异常或丢失信息，但从 byte 到 Digit 的转换是显式的，因为 Digit 只能表示 byte 可能值的一个子集。

## 10.11 实例构造函数

实例构造函数是实现初始化类实例所需操作的成员。实例构造函数使用构造函数声明来声明：

```
constructor-declaration:
    attributes_opt constructor-modifiers_opt constructor-declarator constructor-body

constructor-modifiers:
    constructor-modifier
    constructor-modifiers constructor-modifier

constructor-modifier:
    public
    protected
    internal
    private
    extern

constructor-declarator:
    identifier ( formal-parameter-list_opt ) constructor-initializer_opt

constructor-initializer:
    : base ( argument-list_opt )
    : this ( argument-list_opt )

constructor-body:
    block
    ;
```

构造函数声明可以包含一组特性（§17）、四个访问修饰符（§10.3.5）的有效组合以及 extern（§10.6.7）修饰符。不允许构造函数声明多次包含同一修饰符。

构造函数声明符的标识符必须命名声明该实例构造函数的类。如果指定任何其他名称，则发生编译时错误。

实例构造函数的可选*形参列表*遵循与方法（§10.6）的*形参列表*相同的规则。形参列表定义实例构造函数的签名（§3.6），并控制重载决策（§7.5.2）在调用中选择特定实例构造函数的过程。

实例构造函数的*形参列表*中引用的每个类型都必须至少与构造函数本身一样可访问（§3.5.4）。

可选的*构造函数初始值设定项*指定要在此实例构造函数的*构造函数体*中给出的语句执行之前调用的另一个实例构造函数。这在 §10.11.1 中进一步描述。

当构造函数声明包含 extern 修饰符时，该构造函数称为*外部构造函数*。由于外部构造函数声明不提供实际实现，其*构造函数体*由分号组成。对于所有其他构造函数，*构造函数体*由一个*块*组成，该块指定用于初始化类的新实例的语句。这完全对应于具有 void 返回类型的实例方法的*块*（§10.6.10）。

实例构造函数不被继承。因此，类除了实际在该类中声明的实例构造函数外，没有其他实例构造函数。如果类不包含实例构造函数声明，则自动提供默认实例构造函数（§10.11.4）。

实例构造函数由*对象创建表达式*（§7.6.10.1）以及通过*构造函数初始值设定项*调用。

### 10.11.1 构造函数初始值设定项

所有实例构造函数（类 object 的构造函数除外）都隐式包含在*构造函数体*之前立即调用另一个实例构造函数。要隐式调用的构造函数由*构造函数初始值设定项*确定：

- 形式为 *base*(*参数列表*<sub>opt</sub>) 的实例构造函数初始值设定项会导致调用直接基类中的实例构造函数。该构造函数使用*参数列表*和 §7.5.3 的重载决策规则来选择。候选实例构造函数集合由直接基类中包含的所有可访问实例构造函数组成；如果直接基类中未声明实例构造函数，则由默认构造函数（§10.11.4）组成。如果此集合为空，或无法标识单个最佳实例构造函数，则发生编译时错误。
- 形式为 *this*(*参数列表*<sub>opt</sub>) 的实例构造函数初始值设定项会导致调用该类自身的实例构造函数。该构造函数使用*参数列表*和 §7.5.3 的重载决策规则来选择。候选实例构造函数集合由所有可访问的实例
