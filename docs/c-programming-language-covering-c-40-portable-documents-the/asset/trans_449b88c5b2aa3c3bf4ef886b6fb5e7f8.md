
## 10.6.10 方法体

方法声明的方法体由块或分号组成。

抽象和外部方法声明不提供方法实现，因此它们的方法体仅由分号组成。对于任何其他方法，方法体是一个块（§8.2），其中包含调用该方法时要执行的语句。

当方法的返回类型为 void 时，该方法体中的返回语句（§8.9.4）不允许指定表达式。如果 void 方法的方法体执行正常完成（即，如果控制流离开方法体的末尾），该方法只是返回到其调用方。

当方法的返回类型不是 void 时，该方法体中的每个返回语句都必须指定一个可隐式转换为返回类型的表达式。有返回值的方法的方法体结束点必须不可达。换句话说，在有返回值的方法中，不允许控制流离开方法体的末尾。

在示例中

```
class A
{
    public int F() {}    // Error: return value required
    public int G() {
        return 1;
    }
    public int H(bool b) {
        if (b) {
            return 1;
        } else {
            return 0;
        }
    }
}
```

有返回值的 F 方法会导致编译时错误，因为控制流可能离开方法体的末尾。G 和 H 方法正确，因为所有可能的执行路径都以指定返回值的返回语句结束。

## 10.6.11 方法重载

方法重载解析规则在 §7.5.2 中描述。

## 10.7 属性

属性是提供对对象或类的特征进行访问的成员。属性的示例包括字符串的长度、字体的大小、窗口的标题、客户的名称等。属性是字段的自然扩展——两者都是具有关联类型的命名成员，并且访问字段和属性的语法相同。但是，与字段不同，属性不表示存储位置。相反，属性具有访问器，这些访问器指定在读取或写入其值时执行的语句。因此，属性提供了一种将操作与对象特性的读取和写入相关联的机制；此外，它们允许计算这些特性。

属性使用属性声明来声明：

```
property-declaration:
    attributes_opt property-modifiers_opt type member-name { accessor-declarations }

property-modifiers:
    property-modifier
    property-modifiers property-modifier

property-modifier:
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

member-name:
    identifier
    interface-type . identifier
```

属性声明可以包括一组特性（§17）、四个访问修饰符的有效组合（§10.3.5），以及 new（§10.3.4）、static（§10.6.2）、virtual（§10.6.3）、override（§10.6.4）、sealed（§10.6.5）、abstract（§10.6.6）和 extern（§10.6.7）修饰符。

属性声明在修饰符的有效组合方面遵循与方法声明（§10.6）相同的规则。

属性声明的*类型*指定该声明所引入属性的类型，而*成员名*指定属性的名称。除非属性是显式接口成员实现，否则*成员名*只是一个标识符。对于显式接口成员实现（§13.4.1），*成员名*由*接口类型*后跟一个“.”和一个标识符组成。

属性的*类型*必须至少与属性本身一样可访问（§3.5.4）。

*访问器声明*必须用“{”和“}”标记括起来，声明属性的访问器（§10.7.2）。访问器指定与读取和写入属性相关联的可执行语句。

尽管访问属性的语法与访问字段的语法相同，但属性不归类为变量。因此，不能将属性作为 ref 或 out 实参传递。

当属性声明包含 extern 修饰符时，称该属性为*外部属性*。由于外部属性声明不提供实际实现，其每个访问器声明都由一个分号组成。

### 10.7.1 静态和实例属性

当属性声明包含 static 修饰符时，称该属性为*静态属性*。当不存在 static 修饰符时，称该属性为*实例属性*。

静态属性不与特定实例关联，在静态属性的访问器中引用 this 是编译时错误。

实例属性与类的给定实例关联，并且可以在该属性的访问器中作为 this（§7.6.7）访问该实例。

当在形式为 E.M 的*成员访问*（§7.6.4）中引用属性时，如果 M 是静态属性，则 E 必须表示包含 M 的类型；如果 M 是实例属性，则 E 必须表示包含 M 的类型的实例。

静态成员和实例成员之间的差异在 §10.3.7 中进一步讨论。

### 10.7.2 访问器

属性的访问器声明指定与读取和写入该属性相关联的可执行语句。

```
accessor-declarations:
    get-accessor-declaration  set-accessor-declaration_opt
    set-accessor-declaration  get-accessor-declaration_opt

get-accessor-declaration:
    attributes_opt  accessor-modifier_opt  get  accessor-body

set-accessor-declaration:
    attributes_opt  accessor-modifier_opt  set  accessor-body

accessor-modifier:
    protected
    internal
    private
    protected  internal
    internal  protected

accessor-body:
    block
    ;
```

访问器声明由 get 访问器声明、set 访问器声明或两者组成。每个访问器声明由标记 get 或 set 后跟可选的访问器修饰符和访问器体组成。

访问器修饰符的使用受以下限制约束：

- 访问器修饰符不得在接口或显式接口成员实现中使用。
- 对于没有 override 修饰符的属性或索引器，仅当该属性或索引器同时具有 get 和 set 访问器时才允许使用访问器修饰符，并且此时只允许在其中之一访问器上使用。
- 对于包含 override 修饰符的属性或索引器，访问器必须与被重写访问器的访问器修饰符（如果有）匹配。
- 访问器修饰符必须声明比属性或索引器本身声明的可访问性更严格限制的可访问性。确切地说：
- 如果属性或索引器声明的可访问性为 public，则访问器修饰符可以是 protected internal、internal、protected 或 private。
- 如果属性或索引器声明的可访问性为 protected internal，则访问器修饰符可以是 internal、protected 或 private。
- 如果属性或索引器声明的可访问性为 internal 或 protected，则访问器修饰符必须是 private。
- 如果属性或索引器声明的可访问性为 private，则不得使用访问器修饰符。

对于抽象属性和外部属性，所指定的每个访问器的访问器体只是一个分号。非抽象、非外部属性可以是自动实现的属性，在这种情况下必须同时给出 get 和 set 访问器，两者都具有分号体（§10.7.3）。对于任何其他非抽象、非外部属性的访问器，访问器体是一个块，指定调用相应访问器时要执行的语句。

get 访问器对应于一个无参数方法，其返回值为属性类型。除作为赋值目标外，当在表达式中引用属性时，将调用该属性的 get 访问器来计算属性的值（§7.1.1）。get 访问器体必须符合 §10.6.10 中描述的有返回值方法的规则。特别是，get 访问器体中的所有返回语句都必须指定一个可隐式转换为属性类型的表达式。此外，get 访问器的结束点必须不可达。

set 访问器对应于一个方法，该方法具有一个属性类型的值参数和 void 返回类型。set 访问器的隐式参数始终命名为 value。当属性作为赋值目标（§7.17）或作为 ++ 或 -- 的操作数（§7.6.9、§7.7.5）被引用时，将调用 set 访问器，并传入一个实参（其值为赋值右侧的值或 ++ 或 -- 运算符的操作数），该实参提供新值（§7.17.1）。set 访问器体必须符合 §10.6.10 中描述的 void 方法规则。特别是，set 访问器体中的返回语句不允许指定表达式。由于 set 访问器隐式具有名为 value 的参数，因此 set 访问器中的局部变量或常量声明使用该名称是编译时错误。

根据 get 和 set 访问器的存在与否，属性分类如下：
