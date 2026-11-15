

清单 5.20 在 Employee 构造函数内部为字段赋值，而不是为属性赋值（_id = id）。通过属性赋值会导致编译错误，就像在 Program.Main() 中一样。

## Getter 和 Setter 上的访问修饰符

如前所述，最好不要从属性外部访问字段，因为这样做会绕过可能插入的任何验证或附加逻辑。不幸的是，C# 1.0 不允许属性的 getter 和 setter 部分之间具有不同的封装级别。因此，不可能创建公共 getter 和私有 setter，以便外部类对属性具有只读访问权限，而类内部的代码可以写入属性。

在 C# 2.0 中，添加了对在属性实现的 get 或 set 部分（而不是两者）上放置访问修饰符的支持，从而覆盖属性声明中指定的访问修饰符。清单 5.21 演示了如何执行此操作。

### 清单 5.21：在 setter 上放置访问修饰符

```
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();
        employee1.Initialize(42);

        // ERROR: The property or indexer 'Employee.Id'
        // cannot be used in this context because the set
        // accessor is inaccessible
        employee1.Id = "498";
    }
}

class Employee
{
    public void Initialize(int id)
    {
        // Set Id property
        Id = id.ToString();
    }

    // ...
}
// Id property declaration
public string Id
{
    get
    {
        return _id;
    }
    // Providing an access modifier is in C# 2.0
    // and higher only
    private set
    {
        _id = value;
    }
}
private string _id;
}
```

在 setter 上使用 private，该属性对于 Employee 以外的类来说显示为只读。从 Employee 内部，该属性显示为读/写，因此你可以在构造函数中为属性赋值。在 getter 或 setter 上指定访问修饰符时，请注意该访问修饰符应比整个属性上的访问修饰符更严格。例如，将属性声明为 private 而将 setter 声明为 public 是编译错误。

## 作为虚拟字段的属性

如你所见，属性的行为类似于虚拟字段。在某些情况下，你根本不需要后备字段。相反，属性 getter 返回计算值，而 setter 解析值并将其持久化到其他成员字段（如果存在的话）。例如，考虑清单 5.22 中显示的 Name 属性实现。输出 5.7 显示了结果。

### 清单 5.22：定义属性

```
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();
        employee1.Name = "Inigo Montoya";
        System.Console.WriteLine(employee1.Name);
    }
}
// ...
}
}

class Employee
{
    // ...
    // FirstName property
    public string FirstName
    {
        get
        {
            return _FirstName;
        }
        set
        {
            _FirstName = value;
        }
    }
    private string _FirstName;

    // LastName property
    public string LastName
    {
        get
        {
            return _LastName;
        }
        set
        {
            _LastName = value;
        }
    }
    private string _LastName;
    // ...

// Name property
public string Name
{
    get
    {
        return FirstName + " " + LastName;
    }
    set
    {
        // Split the assigned value into
// first and Last names.
string[] names;
names = value.Split(new char[] { ' ' });
if(names.Length == 2)
{
    FirstName = names[0];
    LastName = names[1];
}
else
{
    // Throw an exception if the full
    // name was not assigned.
    throw new System.ArgumentException(
        string.Format(
            "Assigned value '{0}' is invalid", value));
}
}
// ...
}
```

### 输出 5.7:

```
Inigo Montoya
```

Name 属性的 getter 将 FirstName 和 LastName 属性返回的值连接起来。实际上，分配的名称值并未实际存储。当为 Name 属性赋值时，右侧的值会被解析为其名和姓部分。

## 属性和方法调用不允许作为 ref 或 out 参数值

C# 允许属性与字段以相同的方式使用，但当它们作为 ref 或 out 参数值传递时除外。ref 和 out 参数值在内部通过将内存地址传递给目标方法来实现。但是，因为属性可以是没有后备字段的虚拟字段，或者可以是只读/只写属性，所以无法传递底层存储的地址。因此，你不能将属性作为 ref 或 out 参数值传递。方法调用也是如此。相反，当代码需要将属性或方法调用作为 ref 或 out 参数值传递时，代码必须先将值复制到变量中，然后传递该变量。方法调用完成后，代码必须将变量重新赋值给属性。

## 高级主题

## 属性内部

清单 5.23 显示，getter 和 setter 在 CIL 中公开为 get_FirstName() 和 set_FirstName()。

### 清单 5.23：属性生成的 CIL 代码

```
.method public hidebysig specialname instance string
get_FirstName() cil managed
{
    // Code size       12 (0xc)
    .maxstack  1
    .locals init ([0] string CS$1$0000)
    IL_0000:  nop
    IL_0001:  ldarg.0
    IL_0002:  ldfld      string Program::FirstName
    IL_0007:  stloc.0
    IL_0008:  br.s       IL_000a
    IL_000a:  ldloc.0
    IL_000b:  ret
} // end of method Program::get_FirstName

.method public hidebysig specialname instance void
set_FirstName(string value) cil managed
{
    // Code size       9 (0x9)
    .maxstack  8
    IL_0000:  nop
    IL_0001:  ldarg.0
    IL_0002:  ldarg.1
    IL_0003:  stfld      string Program::FirstName
    IL_0008:  ret
} // end of method Program::set_FirstName
```

与它们作为常规方法出现同样重要的是，属性也是 CIL 中的显式构造。如清单 5.24 所示，getter 和 setter 由 CIL 属性调用，CIL 属性是 CIL 代码中的显式构造。因此，语言和编译器不受限于始终根据命名约定解释属性。相反，CIL 属性为编译器和代码编辑器提供特殊语法的手段。

### 清单 5.24：属性是 CIL 中的显式构造

```
.property instance string FirstName()
{
    .get instance string Program::get_FirstName()
    .set instance void Program::set_FirstName(string)
} // end of property Program::FirstName
```

请注意，在清单 5.23 中，属性的一部分的 getter 和 setter 包含 specialname 元数据。IDE（例如 Visual Studio）使用此修饰符作为标志，以将成员从 IntelliSense 中隐藏。

自动实现的属性与你显式定义后备字段的属性几乎相同。C# 编译器会生成一个名为 <PropertyName>k__BackingField 的字段（在 IL 中），以替代手动定义的后备字段。此生成的字段包含一个名为 System.Runtime.CompilerServices.CompilerGeneratedAttribute 的特性（参见第 17 章）。getter 和 setter 都装饰了相同的特性，因为它们也是生成的——实现与清单 5.23 和 5.24 中相同。

## 构造函数

现在你已向类添加字段并可以存储数据，需要考虑该数据的有效性。如你在清单 5.3 中所见，可以使用 new 运算符实例化对象。然而，这会导致能够创建具有无效数据的员工。在对 employee 赋值后立即，你会得到一个名称和薪水未初始化的 Employee 对象。在这个特定的清单中，你在实例化员工后立即为未初始化的字段赋值，但如果你未执行初始化，则不会收到编译器的警告。结果，你可能会得到一个名称无效的 Employee 对象。

