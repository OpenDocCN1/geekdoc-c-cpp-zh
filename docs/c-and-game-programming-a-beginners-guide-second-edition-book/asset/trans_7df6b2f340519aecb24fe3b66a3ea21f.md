
结合多个 catch 响应。所讨论的信息置于 try 块的参数之间，并且只有一次成功的机会（参见示例 B.66）。

## 示例 B.66.
```csharp
public class Appendix_B {
    static void Main() {
        try{}
        catch{}
        finally{}
    }
}
```

## typeof
typeof 运算符用于确定对象的类型、字段、方法、属性（参见示例 B.67）。

### 示例 B.67.
```csharp
using System;
namespace Appendix_B {
    public class Class1 {
        public static void Main() {
            Type Ob = typeof(Class1);
            Console.WriteLine(Ob.GetFields());
            Console.WriteLine(Ob.GetMethods());
        }
    }
}
```

## uint
关键字 uint 是一个无符号 32 位整型，用于存储从 0 到 4,294,967,295 的值（参见示例 B.68）。

### 示例 B.68.
```csharp
class Appendix_B {
    static void Main() {
        uint Number1 = 1;
    }
}
```

## ulong
关键字 ulong 表示无符号 64 位整型，用于存储从 0 到 18,446,744,073,709,551,615 的值（参见示例 B.69）。

### 示例 B.69.
```csharp
class Appendix_B {
    static void Main() {
        ulong Number1 = 1;
    }
}
```

## unchecked
关键字 unchecked 用于阻止“解决方案资源管理器\配置属性\生成\检查算术溢出/下溢”为 true 的语句。该语句默认情况下为 false，但如果我们更改此默认值并试图突破指定类型的界限，则可以使用 unchecked 语句阻止错误（参见示例 B.70）。

### 示例 B.70.
```csharp
class Appendix_B {
    static void Main () {
        byte Max255 = 255;
        unchecked {Max255 += 1 ;}
    }
}
```

## unsafe
关键字 unsafe 表示将设置更改为不安全模式。开发 unsafe 功能是为了帮助弥合 C++ 和 C# 编程之间的差距，允许我们使用在 C# 安全模式下未正式允许的久经考验的技术（参见示例 B.72）。除了在编码中包含关键字 unsafe 之外，我们还必须在配置管理器中更改编译器的设置（详细信息请参见第 1 章——Sizeof 和不安全编码）。

### 示例 B.71.
```csharp
class Class1 {
    static unsafe void Main() {}
}
```

## ushort
关键字 ushort 表示 16 位整型数据类型，用于存储从 0 到 65,535 的值（参见示例 B.72）。

### 示例 B.72.
```csharp
class Appendix_B {
    static void Main() {
        ushort Number1 = 1;
    }
}
```

## using
using 指令允许我们包含大量系统命名空间和用户定义命名空间；包含命名空间并不等同于包含文件（如 C++ 中所做的那样）。在这里，我们只是通知编译器在哪里找到以简写形式编写的引用。访问用户定义命名空间的方式与系统类型完全相同（参见示例 B.73）。

### 示例 B.73.
```csharp
using System;
class Appendix_B {
    static void Main() {}
}
```

## virtual
关键字 virtual 表示一个修饰符，它设置基类的方法，以便可以在派生类中重写该方法。当引用虚函数时，它会搜索重写方法。

### 示例 B.74.
```csharp
namespace Appendix_B {
    public class Area {
        public Area() {}
        public virtual void CalculateArea() {}
    }
    public class Parallelogram : Area {
        public Parallelogram() {}
        override public void CalculateArea() {}
    }
    static void Main() {}
}
```

## void
void 是一种不保存数据的数据类型，因此其目的是告诉编译器此变量或返回函数不需要任何数据。这是合乎逻辑的，因为 main 函数的结束也是程序的结束，不会有程序可以接收信息。void 也最常与使用引用变量（第 2 章解释）和泛化指针变量（第 4 章解释）的用户定义函数相关联。与其他数据类型不同，void 不占用内存中的位置，因此我们不需要以字节为单位测量其大小。

### 示例 B.75.
```csharp
class Appendix_B {
    static void Main(){}
}
```

## volatile
关键字 volatile 用于表示无法优化的变量，这通常是由于对其进行了某些不可预测的更改或引用，频繁来自外部源，例如操作系统或硬件设备（参见示例 B.76）。

### 示例 B.76.
```csharp
class Appendix_B {
    public volatile char variable3 = 'A';
    static void Main(){}
}
```

## while
while 循环可以通过多种不同方式设置为重复和/或终止。最常见的方式包括使用预定计数（例如重复迭代五次然后结束）、根据用户输入（按请求结束）以及终止命令（使循环短路或中断的命令——参见示例 B.77）。

### 示例 B.77.
```csharp
class Appendix_B {
    static void Main() {
        while(true){}
    }
}
```

## 附录 C：访问器

### get 和 set
get 和 set 访问器并非正式的关键字，而是无参数方法，其名称与某些字段匹配，用于包含与这些字段的存储和检索相关的可执行数据体的类和接口中。它们的可执行语句可以包括计算、转换以及大量其他任务，但其基本目的必须包括读取或记录这些属性。访问器的主体被视为等效于方法，尽管它们不包含标识签名。get 访问器返回一个值，并可在需要时设置为抛出值；相反，set 访问器始终设置为 void。关键字 value 也用作设置字段的隐式参数，因此它接受任何传递变量的值。get 和 set 访问器始终共享相同的用户定义名称，因此它们不能存在于同一个基类中。因此，将 set 访问器放在基类中，而将 get 访问器列在下一个派生类中，被认为是自然的。同样重要的是要记住，get 属性检索的值仅供参考，而 set 属性中记录的值只写（参见示例 C.1）。

### 示例 C.1.
```csharp
namespace Appendix_C {
    public class BaseClass {
        public short width;
        protected BaseClass() {}
        public short Width {set{width = value;}}
    }
    public class DerivedClass : BaseClass {
        protected DerivedClass() {}
        public new short Width {get{return(width);}}
        static void Main() {}
    }
}
```

### value
value 类型是作为方法签名的一部分声明的隐式字段，并且像实际字段一样被引用。它们具有与其声明类型的字段相关的相同限制和能力，并应如此对待（参见示例 C.2）。

### 示例 C.2.
```csharp
namespace Appendix_C {
    public class Objects {
        int Number;
        public Objects(int value) {
            this.Number = value;
        }
        static void Main() {}
    }
}
```

## 附录 D：优先级顺序

| 符号 | 描述 |
|---|---|
| `.` | 点运算符 |
| `[]` | 数组索引 |
| `()` | 函数调用 |
| `++` | 后缀递增运算符（置于变量之后） |
| `--` | 后缀递减运算符（置于变量之后） |
| `new, typeof` |  |
| `checked, unchecked` |  |
| `++` | 前缀递增运算符（置于变量之前） |
| `--` | 前缀递减运算符（置于变量之前） |
| `!` | 逻辑非 |
| `-` | 一元减 |
| `+` | 一元加 |
| `~` | 一元 |
| `(T)x` |  |
| `*` | 乘法 |
| `/` | 除法 |
| `%` | 取余 |
| `+` | 加法 |
| `-` | 减法 |
| `<<` | 左移 |
| `>>` | 右移 |
| `<` | 小于 |
| `>` | 大于 |
| `<=` | 小于或等于 |
| `>=` | 大于或等于 |
| `as, is` |  |
| `==` | 等于 |
| `!=` | 不等于 |
| `&` | 逻辑与 |
| `^` | 逻辑异或 |
| `|` | 逻辑或 |
| `&&` | 与 |
| `||` | 或 |
| `?:` | 条件 |
| `= += -= *= /= %=` | 赋值、加、减、乘、除、取余... |
| `/= %= <<= >>= ` |  |
| `|= &= ^=` |  |

