

## 第 7 章：继承

以列表 7.12 为例。它的输出显示在输出 7.4 中。

列表 7.12：override 与 new 修饰符对比

```csharp
public class Program
{
    public class BaseClass
    {
        public static void DisplayName()
        {
            Console.WriteLine("BaseClass");
        }
    }

    public class DerivedClass : BaseClass
    {
        // 编译器警告：DisplayName() 隐藏了继承的成员
        // 如果意图是隐藏，请使用 new 关键字
        public virtual void DisplayName()
        {
            Console.WriteLine("DerivedClass");
        }
    }

    public class SubDerivedClass : DerivedClass
    {
        public override void DisplayName()
        {
            Console.WriteLine("SubDerivedClass");
        }
    }

    public class SuperDerivedClass : DerivedClass
    {
        public new new void DisplayName()
        {
            Console.WriteLine("SuperDerivedClass");
        }
    }

    public static void Main()
    {
        BaseClass baseObj = new BaseClass();
        baseObj.DisplayName();

        DerivedClass derivedObj = new DerivedClass();
        derivedObj.DisplayName();

        SubDerivedClass subObj = new SubDerivedClass();
        subObj.DisplayName();

        SuperDerivedClass superObj = new SuperDerivedClass();
        superObj.DisplayName();
    }
}
```

## 重写基类

```csharp
BaseClass.DisplayName();
DerivedClass.DisplayName();
BaseClass.DisplayName();
```

输出 7.4

```
BaseClass
DerivedClass
SuperDerivedClass
```

这些结果由于以下原因产生：

- **SuperDerivedClass**：SuperDerivedClass.DisplayName() 显示的是 BaseClass，因为没有派生类重写它。
- **SubDerivedClass**：DerivedClass.DisplayName() 是为了重写基类成员。SuperDerivedClass.DisplayName() 是虚方法。
- **DerivedClass**：DerivedClass.DisplayName() 是为了重写基类成员。SuperDerivedClass.DisplayName() 是由于 `new` 修饰符。
- **BaseClass**：BaseClass.DisplayName() 隐藏了派生类的成员。SuperDerivedClass.DisplayName() 是由于 `new` 修饰符。

当涉及到基类属性时，`new` 修饰符没有影响。`sealed` 修饰符可以阻止派生类重写。然而，`sealed` 修饰符的作用是防止该方法被重写。

## sealed 修饰符

正如可以使用 `sealed` 修饰符来阻止类继承一样，也可以使用它来阻止派生类重写基类的虚方法（参见列表 7.13）。

列表 7.13：密封成员

```csharp
class A
{
    public virtual void Method()
    {
    }
}
class B : A
{
    public override sealed void Method()
    {
    }
}
class C : B
{
    // ：无法重写密封成员
    // public override void Method()
    // {}
}
```

在上面的示例中，对类 B 使用 `sealed` 修饰符阻止了类 C。

通常，将类标记为 `sealed` 很少见，但它适用于那些由于密封类带来的好处大于其派生类的情况。由于单元测试的需要，密封类有时是理想理想的。

## base 成员

在重写成员时，开发者通常需要调用基类的实现（参见列表 7.14）。

列表 7.14：访问基类成员

在列表 7.14 中，使用 `base` 关键字来调用基类的实现。其语法与使用 `this` 关键字非常相似，包括在构造函数中使用（稍后讨论）。

此外，在 `Address.ToString()` 实现中，你需要重写它因为它是 `object` 类的成员。

> 注意
> 带有 `override` 修饰符的方法自动是虚的。基类方法只有是虚方法才能被重写，因此重写方法也是虚的。

