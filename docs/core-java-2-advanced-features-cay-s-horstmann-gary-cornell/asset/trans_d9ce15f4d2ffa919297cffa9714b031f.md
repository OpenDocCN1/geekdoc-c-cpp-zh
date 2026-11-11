
这是上一节ObjectRefTest程序的带注释输出。运行该程序，查看其数据文件employee.dat的十六进制转储，并与带注释的列表进行比较。输出末尾的重要几行显示了对先前保存对象的引用。

| 十六进制转储 | 注释 |
|---|---|
| `AC ED 00 05` | 文件头 |
| `75` | 数组staff（序列号#1） |
| `72 00 0B [LEmployee;` | 新类、字符串长度、类名Employee[]（序列号#0） |
| `FC BF 36 11 C5 91 11 C7 02` | 指纹和标志 |
| `00 00` | 实例字段数量 |
| `78` | 结束标记 |
| `70` | 无超类 |
| `00 00 00 03` | 数组条目数量 |
| `73` | staff[0]—新对象（序列号#7） |
| `72 00 07 Manager` | 新类、字符串长度、类名（序列号#2） |
| `36 06 AE 13 63 8F 59 87 02` | 指纹和标志 |
| `00 01` | 数据字段数量 |
| `L 00 09 secretary` | 实例字段类型和名称 |
| `74 00 0A LEmployee;` | 实例字段类名：String（序列号#3） |
| `78` | 结束标记 |
| `72 00 08 Employee` | 超类：新类、字符串长度、类名（序列号#4） |
| `E6 D2 86 70 AE AC 18 18 02` | 指纹和标志 |
| `00 03` | 实例字段数量 |
| `D 00 06 salary` | 实例字段类型和名称 |
| `L 00 07 hireDay` | 实例字段类型和名称 |
| `74 00 10 Ljava/util/Date;` | 实例字段类名：String（序列号#5） |
| `L 00 04 name` | 实例字段类型和名称 |
| `74 00 12 Ljava/lang/String;` | 实例字段类名：String（序列号#6） |
| `78` | 结束标记 |
| `70` | 无超类 |
| `40 F3 88 00 00 00 00 00` | salary字段值：double |
| `73` | hireDay字段值：新对象（序列号#9） |
| `72 00 0E java.util.Date` | 新类、字符串长度、类名（序列号#8） |
| `68 6A 81 01 48 59 74 19 03` | 指纹和标志 |
| `00 00` | 无实例变量 |
| `78` | 结束标记 |
| `70` | 无超类 |
| `77 08` | 外部存储，字节数 |
| `00 00 00 83 E9 39 E0 00` | 日期 |
| `78` | 结束标记 |
| `74 00 0C Carl Cracker` | name字段值：String（序列号#10） |
| `73` | secretary字段值：新对象（序列号#11） |
| `71 00 7E 00 04` | 现有类（使用序列号#4） |
| `40 E8 6A 00 00 00 00 00` | salary字段值：double |
| `73` | hireDay字段值：新对象（序列号#12） |
| `71 00 7E 00 08` | 现有类（使用序列号#8） |
| `77 08` | 外部存储，字节数 |
| `00 00 00 91 1B 4E 01 80` | 日期 |
| `78` | 结束标记 |
| `74 00 0C Harry Hacker` | name字段值：String（序列号#13） |
| `71 00 7E 00 08` | staff[1]：现有对象（使用序列号#11） |
| `73` | staff[2]：新对象（序列号#14） |
| `71 00 7E 00 02` | 现有类（使用序列号#2） |
| `40 E3 88 00 00 00 00 00` | salary字段值：double |
| `73` | hireDay字段值：新对象（序列号#15） |
| `71 00 7E 00 08` | 现有类（使用序列号#8） |
| `77 08` | 外部存储，字节数 |
| `00 00 00 94 60 3E EC 00 00` | 日期 |
| `78` | 结束标记 |
| `74 00 08 Tony Tester` | name字段值：String（序列号#16） |
| `71 00 7E 00 08` | secretary字段值：现有对象（使用序列号#11） |

当然，研究这些代码可能就像读电话簿一样枯燥乏味。了解确切的文件格式并不重要（除非你想通过修改数据来制造破坏效果），但了解序列化格式包含了其中所有对象的详细描述仍然具有启发意义，其详尽程度足以重建对象和对象数组。

你应该记住的是：

-   序列化格式包含所有对象的类型和数据字段。
-   每个对象都被分配一个序列号。
-   同一对象的重复出现会存储为对该序列号的引用。

## 2.4.3 修改默认序列化机制

某些数据字段永远不应被序列化——例如，存储文件句柄或窗口句柄的整数值，这些句柄仅对本地方法有意义。当你稍后重新加载对象或将其传输到另一台机器时，这类信息肯定毫无用处。事实上，这些字段的值不当可能会导致本地方法崩溃。Java提供了一种机制来防止这些字段被序列化：用关键字transient标记它们。如果字段属于不可序列化的类，也需要将它们标记为transient。在对象序列化时，transient字段总是被跳过。

序列化机制为各个类提供了一种方式，可以向默认的读写行为添加验证或任何其他所需操作。可序列化类可以定义具有以下签名的方法：

```java
private void readObject(ObjectInputStream in)
    throws IOException, ClassNotFoundException;
private void writeObject(ObjectOutputStream out)
    throws IOException;
```

然后，数据字段不再自动序列化，而是调用这些方法。

下面是一个典型示例。java.awt.geom包中的许多类，如Point2D.Double，都是不可序列化的。现在，假设你要序列化一个存储String和Point2D.Double的LabeledPoint类。首先，需要将Point2D.Double字段标记为transient，以避免NotSerializableException。

```java
public class LabeledPoint implements Serializable
{
    private String label;
    private transient Point2D.Double point;
    ...
}
```

在writeObject方法中，我们首先通过调用defaultWriteObject方法来写入对象描述符和String字段label。这是ObjectOutputStream类的一个特殊方法，只能从可序列化类的writeObject方法内部调用。然后，我们使用标准的DataOutput调用来写入点的坐标。

```java
private void writeObject(ObjectOutputStream out)
    throws IOException
{
    out.defaultWriteObject();
    out.writeDouble(point.getX());
    out.writeDouble(point.getY());
}
```

在readObject方法中，我们反转该过程：

```java
private void readObject(ObjectInputStream in)
    throws IOException
{
    in.defaultReadObject();
    double x = in.readDouble();
    double y = in.readDouble();
    point = new Point2D.Double(x, y);
}
```

另一个例子是java.util.Date类，它提供了自己的readObject和writeObject方法。这些方法将日期写为自纪元（1970年1月1日午夜UTC）以来的毫秒数。Date类具有复杂的内部表示，存储了Calendar对象和毫秒计数以优化查找。Calendar的状态是冗余的，不需要保存。

readObject和writeObject方法只需要保存和加载它们的数据字段。它们不应关心超类数据或任何其他类信息。

类可以不依赖序列化机制来保存和恢复对象数据，而是定义自己的机制。为此，类必须实现*Externalizable*接口。这反过来要求它定义两个方法：

```java
public void readExternal(ObjectInputStream in)
    throws IOException, ClassNotFoundException;
public void writeExternal(ObjectOutputStream out)
    throws IOException;
```

与上一节描述的readObject和writeObject方法不同，这些方法完全负责保存和恢复整个对象，*包括超类数据*。写入对象时，序列化机制仅记录对象在输出流中的类。读取可外部化对象时，对象输入流使用无参构造器创建对象，然后调用readExternal方法。以下是如何为Employee类实现这些方法：

