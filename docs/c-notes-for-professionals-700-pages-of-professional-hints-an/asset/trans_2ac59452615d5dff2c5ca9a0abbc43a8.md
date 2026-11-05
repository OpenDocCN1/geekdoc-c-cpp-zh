
在计算过程中，值允许“环绕”发生：

```
byte Checksum(byte[] data) {
    byte result = 0;
    for (int i = 0; i < data.Length; i++) {
        result = unchecked(result + data[i]); // unchecked expression
    }
    return result;
}
```

unchecked 最常见的用途之一是实现 object.GetHashCode() 的自定义重写，这是一种校验和。你可以在这个问题（System.Object.GetHashCode 的最佳重写算法是什么？）的答案中看到该关键字的用法。

当块或表达式被声明为 checked 时，任何导致溢出的算术运算都会引发 OverflowException。

```
int SafeSum(int x, int y) {
    checked { // checked block
        return x + y;
    }
}
```

checked 和 unchecked 都可以采用块形式和表达式形式。

checked 和 unchecked 块不会影响所调用的方法，只会影响当前方法中直接调用的运算符。例如，Enum.ToObject()、Convert.ToInt32() 和用户自定义运算符不受自定义 checked/unchecked 上下文的影响。

注意：默认的溢出行为（checked 与 unchecked）可以在项目属性中或通过 /checked[+/-] 命令行开关进行更改。通常，调试版本默认使用 checked 操作，而发布版本默认使用 unchecked 操作。只有在默认方式不适用并且需要显式行为来确保正确性时，才应使用 checked 和 unchecked 关键字。

## 第 52.5 节：virtual、override、new

### virtual 和 override

virtual 关键字允许方法、属性、索引器或事件被派生类重写并呈现多态行为。（在 C# 中，成员默认是非 virtual 的。）

```
public class BaseClass
{
    public virtual void Foo()
    {
        Console.WriteLine("Foo from BaseClass");
    }
}
```

```
Console.WriteLine("Foo from DerivedClass");
}
}
```

virtual 成员的多态行为意味着，在调用时，实际执行的成员是在运行时而非编译时确定的。将执行特定对象所属的最派生类中的重写成员。

简而言之，对象在编译时可以声明为 BaseClass 类型，但如果在运行时它是 DerivedClass 的实例，那么将执行被重写的成员：

```
BaseClass obj1 = new BaseClass();
obj1.Foo(); //Outputs "Foo from BaseClass"

obj1 = new DerivedClass();
obj1.Foo(); //Outputs "Foo from DerivedClass"
```

重写方法不是强制的：

```
public class SecondDerivedClass: DerivedClass {}

var obj1 = new SecondDerivedClass();
obj1.Foo(); //Outputs "Foo from DerivedClass"
```

### new

由于只有定义为 virtual 的成员才可以被重写并具有多态性，因此派生类重新定义非 virtual 成员可能会导致意外结果。

```
public class BaseClass
{
    public void Foo()
    {
        Console.WriteLine("Foo from BaseClass");
    }
}

public class DerivedClass: BaseClass
{
    public void Foo()
    {
        Console.WriteLine("Foo from DerivedClass");
    }
}

BaseClass obj1 = new BaseClass();
obj1.Foo(); //Outputs "Foo from BaseClass"

obj1 = new DerivedClass();
obj1.Foo(); //Outputs "Foo from BaseClass" too!
```

发生这种情况时，所执行的成员始终在编译时根据对象的类型确定。

- 如果对象声明为 BaseClass 类型（即使运行时是派生类），则执行 BaseClass 的方法。
- 如果对象声明为 DerivedClass 类型，则执行 DerivedClass 的方法。

这通常是意外情况（当一个相同成员先添加到派生类型，之后又添加到基类型时），在这种情况下，编译器会生成警告 CS0108。

如果这是有意为之，则使用 new 关键字来抑制编译器警告（并告知其他开发人员你的意图！）。行为保持不变，new 关键字只是抑制了编译器警告。

```
public class BaseClass
{
    public void Foo()
    {
        Console.WriteLine("Foo from BaseClass");
    }
}

public class DerivedClass : BaseClass
{
    public new void Foo()
    {
        Console.WriteLine("Foo from DerivedClass");
    }
}
```

BaseClass obj1 = new BaseClass();
obj1.Foo(); //Outputs "Foo from BaseClass"

obj1 = new DerivedClass();
obj1.Foo(); //Outputs "Foo from BaseClass" too!

### 使用 override 并不是可选的

与 C++ 不同，override 关键字的使用不是可选的：

```
public class A
{
    public virtual void Foo()
    {
    }
}

public class B : A
{
    public void Foo() // Generates CS0108
    {
    }
}
```

上面的示例同样会导致警告 CS0108，因为 B.Foo() 不会自动重写 A.Foo()。当意图是重写基类并实现多态行为时，请添加 override；当需要非多态行为并根据静态类型解析调用时，请添加 new。后者应谨慎使用，因为它可能造成严重混乱。

下面的代码甚至会导致错误：

```
public class A
{
    public void Foo()
    {
    }
}

public class B : A
{
    public override void Foo() // Error: Nothing to override
    {
    }
}
```

### 派生类可以引入多态

下面的代码是完全有效的（尽管很少见）：

```
public class A
{
    public void Foo()
    {
        Console.WriteLine("A");
    }
}

public class B : A
{
    public new virtual void Foo()
    {
        Console.WriteLine("B");
    }
}
```

现在，所有具有 B（及其派生类）静态引用的对象都使用多态来解析 Foo()，而 A 的引用使用 A.Foo()。

```
A a = new A();
a.Foo(); // Prints "A";
a = new B();
a.Foo(); // Prints "A";
B b = new B();
b.Foo(); // Prints "B";
```

### virtual 方法不能是 private

C# 编译器严格禁止无意义的构造。标记为 virtual 的方法不能是 private。因为 private 方法无法从派生类型中看到，因此它也不能被重写。以下代码无法编译：

```
public class A
{
    private virtual void Foo() // Error: virtual methods cannot be private
    {
    }
}
```

## 第 52.6 节：stackalloc

stackalloc 关键字在栈上创建一块内存区域，并返回指向该内存起始位置的指针。栈上分配的内存在其创建所在的作用域退出时自动释放。

//Allocate 1024 bytes. This returns a pointer to the first byte.
byte* ptr = stackalloc byte[1024];

//Assign some values...
ptr[0] = 109;
ptr[1] = 13;
ptr[2] = 232;
...

*在不安全上下文中使用。*

与 C# 中的所有指针一样，读取和赋值没有边界检查。读取超出所分配内存边界的内容将产生不可预测的结果——它可能访问内存中的任意位置，也可能导致访问冲突异常。

//Allocate 1 byte
byte* ptr = stackalloc byte[1];

//Unpredictable results...
ptr[10] = 1;
ptr[-1] = 2;

栈上分配的内存在其创建所在的作用域退出时自动释放。这意味着你不应返回使用 stackalloc 创建的内存，也不应在该作用域生命周期之外存储它。

unsafe IntPtr Leak() {
    //Allocate some memory on the stack
    var ptr = stackalloc byte[1024];

    //Return a pointer to that memory (this exits the scope of "Leak")
    return new IntPtr(ptr);
}

unsafe void Bad() {
    //ptr is now an invalid pointer, using it in any way will have
    //unpredictable results. This is exactly the same as accessing beyond
    //the bounds of the pointer.
    var ptr = Leak();
}

stackalloc 只能在声明和初始化变量时使用。以下是无效的：

byte* ptr;
...
ptr = stackalloc byte[1024];

### 备注：

stackalloc 仅应用于性能优化（无论是计算还是互操作）。这是因为：

- 不需要垃圾回收器，因为内存是在栈上而非堆上分配的——变量一超出作用域，内存即被释放。
- 在栈上分配内存比在堆上更快。
- 由于数据的局部性，增加了 CPU 缓存命中的机会。

## 第 52.7 节：break

在循环（for、foreach、do、while）中，break 语句会中止最内层循环的执行，并返回到循环之后的代码。它还可以与 yield 一起使用，用来指定迭代器已到达末尾。

```
for (var i = 0; i < 10; i++)
{
```
