
```java
public void readExternal(ObjectInput s)
    throws IOException
{
    name = s.readUTF();
    salary = s.readDouble();
    hireDay = LocalDate.ofEpochDay(s.readLong());
}

public void writeExternal(ObjectOutput s)
    throws IOException
{
    s.writeUTF(name);
    s.writeDouble(salary);
    s.writeLong(hireDay.toEpochDay());
}
```

> **注意：** 与 `readObject` 和 `writeObject` 方法不同——这些方法是私有的，只能由序列化机制调用——`readExternal` 和 `writeExternal` 方法是公有的。特别地，`readExternal` 可能允许修改现有对象的状态。

### 2.4.4 序列化单例与类型安全枚举

必须特别注意序列化和反序列化那些被假定为唯一的对象。这种情况通常发生在实现单例和类型安全枚举时。

如果使用 Java 语言的 `enum` 构造，则无需担心序列化——它可以直接工作。然而，假设你维护的遗留代码包含如下枚举类型：

```java
public class Orientation
{
    public static final Orientation HORIZONTAL = new Orientation(1);
    public static final Orientation VERTICAL = new Orientation(2);

    private int value;

    private Orientation(int v) { value = v; }
}
```

这种惯用法在枚举被加入 Java 语言之前很常见。注意构造器是私有的。因此，除了 `Orientation.HORIZONTAL` 和 `Orientation.VERTICAL` 之外，不能创建任何对象。特别地，可以使用 `==` 运算符测试对象相等性：

```java
if (orientation == Orientation.HORIZONTAL) . . .
```

当类型安全枚举实现 Serializable 接口时，有一个重要的转折需要记住。默认的序列化机制并不合适。假设我们写出一个 Orientation 类型的值，然后再把它读回来：

```
Orientation original = Orientation.HORIZONTAL;
ObjectOutputStream out = . . .;
out.write(original);
out.close();
ObjectInputStream in = . . .;
Orientation saved = (Orientation) in.readObject();
```

现在，测试

```
if (saved == Orientation.HORIZONTAL) . . .
```

将会失败。事实上，保存的值是一个全新的 Orientation 类型对象，它不等于任何预定义常量。即使构造器是私有的，序列化机制仍然可以创建新对象！

为了解决这个问题，需要定义另一个特殊的序列化方法，称为 readResolve。如果定义了 readResolve 方法，它会在对象反序列化之后被调用。它必须返回一个对象，该对象随后成为 readObject 方法的返回值。在我们的例子中，readResolve 方法将检查 value 字段并返回合适的枚举常量：

```
protected Object readResolve() throws ObjectStreamException
{
    if (value == 1) return Orientation.HORIZONTAL;
    if (value == 2) return Orientation.VERTICAL;
    throw new ObjectStreamException(); // this shouldn't happen
}
```

记住，要向遗留代码中的所有类型安全枚举以及遵循单例设计模式的所有类添加 readResolve 方法。

### 2.4.5 版本管理

如果使用序列化保存对象，就需要考虑程序演进时会发生什么。版本 1.1 能读取旧文件吗？仍在使用 1.0 的用户能读取新版本生成的文件吗？显然，如果对象文件能够应对类的演进，那将是理想的。

乍一看，这似乎是不可能的。当类定义以任何方式发生变化时，其 SHA 指纹也会变化，而你知道对象输入流会拒绝读入具有不同指纹的对象。然而，类可以表明自己与自身的早期版本兼容。为此，必须首先获取该类早期版本的指纹。使用 JDK 自带的独立 `serialver` 程序获取该编号。例如，运行

```
serialver Employee
```

将打印

```
Employee: static final long serialVersionUID = -1814239825517340645L;
```

如果使用 `-show` 选项启动 `serialver` 程序，该程序会弹出一个图形对话框（见图 2.7）。

![](img/7dd923a566750151a3aab0dacd0cdaa5_116_0.png)

**图 2.7** `serialver` 程序的图形版本

该类的所有*后续*版本都必须将 `serialVersionUID` 常量定义为与原始版本相同的指纹。

```java
class Employee implements Serializable // version 1.1
{
    public static final long serialVersionUID = -1814239825517340645L;
}
```

当类有一个名为 `serialVersionUID` 的静态数据成员时，它将不会手动计算指纹，而是改用该值。

一旦该静态数据成员被放入类中，序列化系统现在就愿意读入该类对象的不同版本。

如果只有类的方法发生变化，读取新的对象数据没有问题。然而，如果数据域发生变化，就可能出现问题。例如，旧文件对象可能比程序中的对象拥有更多或更少的数据域，或者数据域的类型可能不同。在这种情况下，对象输入流会努力将序列化对象转换为该类的当前版本。

对象输入流会将类的当前版本的数据域与序列化对象中版本的数据域进行比较。当然，对象输入流只考虑非 transient 且非静态的数据域。如果两个字段名称匹配但类型不同，对象输入流不会尝试将一种类型转换为另一种类型——这些对象不兼容。如果序列化对象具有当前版本中不存在的数据域，对象输入流会忽略这些额外数据。如果当前版本具有序列化对象中不存在的数据域，则新增字段会被设置为其默认值（对象为 null，数字为 0，布尔值为 false）。

这里有一个示例。假设我们使用该类的原始版本（1.0）将若干员工记录保存到磁盘上。现在，我们通过添加一个名为 department 的数据域，将员工类改为版本 2.0。图 2.8 展示了将 1.0 对象读入使用 2.0 对象的程序时会发生什么。department 字段被设置为 null。图 2.9 展示了相反的情形：使用 1.0 对象的程序读取一个 2.0 对象。额外的 department 字段被忽略。

![](img/7dd923a566750151a3aab0dacd0cdaa5_117_0.png)

图 2.8 读取数据域较少的对象

![](img/7dd923a566750151a3aab0dacd0cdaa5_117_1.png)

图 2.9 读取数据域较多的对象

### 代码清单 2.4（续）

```java
70 public Employee(String n, double s, int year, int month, int day)
71 {
72     name = n;
73     salary = s;
74     hireDay = LocalDate.of(year, month, day);
75 }
76
77 public String getName()
78 {
79     return name;
80 }
81
82 public double getSalary()
83 {
84     return salary;
85 }
86
87 public LocalDate getHireDay()
88 {
89     return hireDay;
90 }
91
92 /**
93  * Raises the salary of this employee.
94  * @byPercent the percentage of the raise
95  */
96 public void raiseSalary(double byPercent)
97 {
98     double raise = salary * byPercent / 100;
99     salary += raise;
100 }
101
102 public String toString()
103 {
104     return getClass().getName()
105         + "[name=" + name
106         + ",salary=" + salary
107         + ",hireDay=" + hireDay
108         + "]";
109 }
110 }
```

## 2.5 文件操作

你已经学习了如何从文件读取和写入数据。然而，文件管理不仅仅是读取和写入。Path 接口和 Files 类
