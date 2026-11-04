
Table 5.2. Definitions of preprocessor directives.
表 5.2. 预处理器指令的定义。

| Directive | Definition |
|---|---|
| #define and #undef | The defined value is used like a variable and can be tested and even undefined. |
| #define 和 #undef | 定义的值像变量一样使用，可以被测试甚至取消定义。 |
| #error and #warning | Error and warning work in basically the same way; both allow for a statement always placed in quotes. |
| #error 和 #warning | 错误和警告基本以相同的方式工作；两者都允许放置在引号中的语句。 |
| #if, #elif, #else, and #endif | #if works in basically the same manner as the if statement, including the else-if (#elif) and the (#else) statement. The only addition would be the #endif which works like the standard } block. |
| #if、#elif、#else 和 #endif | #if 基本上与 if 语句的工作方式相同，包括 else-if（#elif）和（#else）语句。唯一的补充是 #endif，它的工作方式类似于标准的 } 块。 |
| #line | The line directive is used to alter output that is caught by warning and error messages. You'll need to include the line number and file name as in #line 12 "chapter5.cs." |
| #line | 行指令用于更改被警告和错误消息捕获的输出。你需要包含行号和文件名，如 #line 12 "chapter5.cs." 中所示。 |
| #region and #endregion | The region and end region markers are used to mark a certain block of coding. That block can then be collapsed and even given a name. |
| #region 和 #endregion | 区域和结束区域标记用于标记某段代码块。然后该块可以被折叠甚至命名。 |

## The external Modifier
## 外部修饰符

The external modifier (extern), as its name implies, indicates that the method will be implemented externally, such as with the DllImport attribute. The external method will contain all appropriate declarations, but because it is executed outside of our programs, its declaration does not require a function body. External references do require a terminating semicolon, and they cannot be used to modify abstract classes. We can also declare our methods using external modifiers, but these methods will not include implementation, thus, their definitions will contain no bodies (these methods will also require a terminating semicolon). C++ users will find this version of extern a bit more constrictive (see Example 5.50).
外部修饰符（extern），顾名思义，表示方法将在外部实现，例如使用 DllImport 属性。外部方法将包含所有适当的声明，但由于它在程序外部执行，其声明不需要函数体。外部引用需要以分号结尾，并且不能用于修改抽象类。我们也可以使用外部修饰符声明方法，但这些方法不包含实现，因此它们的定义不包含主体（这些方法也需要以分号结尾）。C++ 用户会发现这个版本的 extern 有点更受限制（参见示例 5.50）。

### Example 5.50. The extern modifier.
### 示例 5.50. extern 修饰符。

```
using System;
using System.Runtime.InteropServices;
namespace Chapter5 {
public class Class1 {
    [DllImport("winmm.dll")]
    public static extern long PlaySound(String lpszName, long hModule,
        long dwFlags);

    static void Main() {
        PlaySound(@"media\Mouse.wav", 0, 0);
    }
}
}
```

## The explicit Operator
## 显式运算符

The keyword explicit is used to define an explicit type conversion, which is a conversion that would not normally be allowed by basic implicit reasoning. The standard implicit types convert only from lower to higher accuracy, which prevents data loss. Occasionally, however, the programmer will want to reverse that process and formally reduce the accuracy of the data type, anticipating no relevant loss in computations. In such cases, an explicit modifier can be applied (they are used with a standard class in Example 5.51).
关键字 explicit 用于定义显式类型转换，即基本隐式推理通常不允许的转换。标准隐式类型仅从较低精度转换为较高精度，从而防止数据丢失。然而，有时程序员希望反转该过程并正式降低数据类型的精度，预计计算中不会有相关损失。在这种情况下，可以应用显式修饰符（它们在示例 5.51 中与标准类一起使用）。

### Example 5.51. The explicit operator.
### 示例 5.51. 显式运算符。

```
using System;
namespace Chapter5 {
    class IsByte {
        byte value;

        public IsByte(int value) {
            if (value < 0 || value > 255)
                throw new ArgumentException();
            this.value = (byte)value;
        }

        public static explicit operator IsByte(byte Byte) {
            return new IsByte(Byte);
        }

        public static void Main() {
            int Integer = 3;
            IsByte Byte = (IsByte)Integer;
        }
    }
}
```

## The implicit Operator
## 隐式运算符

The keyword implicit is used when declaring a user-defined conversion operator. Implicit conversions are called implicitly, thus they do not need to be referenced using explicit casts, increasing source code readability as well as safety. However, since implicit conversion can occur without the programmer's knowledge, care must be taken: Implicit conversions should never be allowed to throw exceptions, nor should they be allowed to truncate relevant data. Implicit classes can be defined using static modifiers and are referenced using instances (see Example 5.52).
关键字 implicit 用于声明用户定义的转换运算符。隐式转换会被隐式调用，因此不需要使用显式转换来引用，从而提高源代码的可读性和安全性。然而，由于隐式转换可能在程序员不知情的情况下发生，必须谨慎：隐式转换绝不允许抛出异常，也不允许截断相关数据。隐式类可以使用静态修饰符定义，并使用实例引用（参见示例 5.52）。

### Example 5.52. The implicit operator.
### 示例 5.52. 隐式运算符。

```
using System;

namespace Chapter5 {
    class IsByte {
        byte value;

        public IsByte(byte value) {
            this.value = value;
        }

        public static implicit operator byte(IsByte Byte) {
            return Byte.value;
        }

        public static void Main() {
            IsByte Byte = new IsByte(3);

            byte Byte2 = Byte;
        }
    }
}
```

## Fixed Pointers
## 固定指针

The keyword fixed, used only in unsafe mode, is a modifier that sets unmanaged pointers to managed variable locations. These positions are then fixed, which means that they won't be subject to automatic garbage collection (or random relocation); the term pinned is also commonly associated with this process. Pointers initialized in fixed statements cannot be modified; however, once the statement is executed, the variables are no longer pinned, hence any references to those variables should be done in the appropriate fixed reference (see Example 5.53).
关键字 fixed，仅在不安全模式下使用，是一个修饰符，它将非托管指针设置为托管变量位置。这些位置随后被固定，这意味着它们不会受到自动垃圾回收（或随机重新定位）的影响；术语 pinned 也常与此过程相关联。在 fixed 语句中初始化的指针不能被修改；然而，一旦语句执行，变量不再被固定，因此对这些变量的任何引用都应在适当的 fixed 引用中进行（参见示例 5.53）。

### Example 5.53. Fixed pointers.
### 示例 5.53. 固定指针。

```csharp
using System;

namespace Chapter5 {
    class ClassFixed {
        public int variable;
    }

    class Class1 {
        static unsafe void Main () {
            ClassFixed TestFixed = new ClassFixed();

            Console.Write("Enter a number: ");
            TestFixed.variable = int.Parse(Console.ReadLine());

            fixed (int* pointer = &TestFixed.variable) {
                Console.WriteLine("{0}", TestFixed.variable);
                Console.WriteLine("{0}", *pointer);
            }
        }
    }
}
```

## The get and set Accessors
## get 和 set 访问器

The get and set accessors aren't officially keywords, rather, they are parameterless methods named to match certain fields, and are used in classes and interfaces that hold a body of executable data pertaining to the storage and retrieval of those fields. Their executable statements may include calculations, conversions, and a large host of other tasks, but their underlying purpose must include reading or recording those properties. The body of an accessor is considered equivalent to a method, although they do not include identity signatures. The get accessor returns a value and may be set to throw a value when needed; in contrast, the set accessor is always set to void. The keyword value is also used as an implicit parameter when setting our fields. Thus, value takes on the value of any passed variables. The get and the set accessors always share the same user-defined name, thus they cannot exist in the same base class. It is therefore considered natural to place the set accessor in the base class, and the get accessor in the nested derived class. It is also important to remember that the value retrieved by the get property is for reference only, while the value recorded in the set property is write only (see Example 5.54).
get 和 set 访问器并不是正式的关键字，而是无参数的方法，其名称与某些字段匹配，并用于包含与存储和检索这些字段相关的可执行数据体的类和接口。它们的可执行语句可能包括计算、转换以及大量其他任务，但其基本目的必须包括读取或记录这些属性。访问器的主体被视为等同于方法，尽管它们不包含标识签名。get 访问器返回一个值，并且在需要时可以设置为抛出值；相比之下，set 访问器始终设置为 void。关键字 value 也用作设置字段时的隐式参数。因此，value 采用任何传递变量的值。get 和 set 访问器始终共享相同的用户定义名称，因此它们不能存在于同一个基类中。因此，将 set 访问器放在基类中，而将 get 访问器放在嵌套派生类中被认为是自然的。还必须记住，get 属性检索的值仅供参考，而 set 属性记录的值仅供写入（参见示例 5.54）。

### Example 5.54. The get and set accessors—linking classes.
### 示例 5.54. get 和 set 访问器——链接类。

```csharp
using System;

namespace Chapter5 {
    public class BaseClass {
        public short width, length;

        protected BaseClass() {}

        protected BaseClass(short w, short l) {
            Width = w;
            Length = l;
        }

        public short Width {
            set {
                width = value;
            }
        }

        public short Length {
            set {
                length = value;
            }
        }
    }

    public class DerivedClass : BaseClass {
        protected DerivedClass() {}

        protected DerivedClass(short w, short l) {
            width = w;
            length = l;
        }

        public new short Width {
            get {
                return(width);
            }
        }
    }
}
```

```csharp
}

public new short Length {
    get {
        return(length);
    }
}

protected static void DisplayArea(DerivedClass Y) {
    Console.WriteLine("Area = " + Y.Width * Y.Length);
}
}

public class DerivedX : DerivedClass {
    protected DerivedX(short w, short l) {
        width = w;
        length = l;
    }

    protected static void DisplayArea(DerivedX Z) {
        Console.WriteLine("Area = " + Z.Width * Z.Length);
    }

    protected static void Triangle(DerivedX Z) {
        Console.WriteLine("The Area of the Triangle is " + .5 *
            Z.Width * Z.Length);
    }

    static void Main() {
        DerivedX Instance = new DerivedX(5, 6);
        Console.WriteLine(Instance.Width);
        Console.WriteLine(Instance.Length);
        DisplayArea(Instance);
        Triangle(Instance);
    }
}
}
```

## Linking Interfaces
## 链接接口

An *interface* is a structured set of coding used to guarantee a basic level of execution. An interface’s definition includes an attribute, an access modifier, the keyword *interface*, its identifying value, and a base list. All five of the class modifiers are also compatible with
一个 *接口* 是用于保证基本执行水平的结构化代码集。接口的定义包括一个属性、一个访问修饰符、关键字 *接口*、其标识值和一个基列表。所有五个类修饰符也与
