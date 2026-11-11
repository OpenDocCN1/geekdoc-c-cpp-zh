
| 类型代码 | 字段类型 |
|---|---|
| `B` | 字节 |
| `C` | 字符 |
| `D` | 双精度浮点 |
| `F` | 单精度浮点 |
| `I` | 整数 |
| `J` | 长整数 |
| `L` | 对象 |
| `S` | 短整数 |
| `Z` | 布尔 |
| `[` | 数组 |

当类型代码为 `L` 时，字段名后面跟着字段类型。类名和字段名字符串不以字符串代码 `74` 开头，但字段类型会以它开头。字段类型对其名称使用略有不同的编码——即本地方法所用的格式。

例如，`Employee` 类的 `salary` 字段编码为

```
D 00 06 salary
```

下面是 `Employee` 类的完整类描述符：

| 描述符 | 含义 |
|---|---|
| `72 00 08 Employee` | 类名：Employee |
| `E6 D2 86 70 AE AC 18 18 02` | 指纹和标志 |
| `00 03` | 实例字段数量 |
| `D 00 06 salary` | 实例字段类型和名称 |
| `L 00 07 hireDay` | 实例字段类型和名称 |
| `74 00 10 Ljava/util/Date;` | 实例字段类名：Date |
| `L 00 04 name` | 实例字段类型和名称 |
| `74 00 12 Ljava/lang/String;` | 实例字段类名：String |
| `78` | 结束标记 |
| `70` | 无超类 |

这些描述符相当长。如果文件中再次需要同一个类描述符，则使用缩写形式：

| 代码 | 含义 |
|---|---|
| `71` | 4 字节序列号 |

该序列号指向前一个显式类描述符。我们稍后讨论编号方案。

对象按如下方式存储：

| 代码 | 含义 |
|---|---|
| `73` | 类描述符，后跟对象数据 |

例如，下面是一个 `Employee` 对象的存储方式：

```
40 E8 6A 00 00 00 00 00        salary field value: double
73                            hireDay field value: new object
   71 00 7E 00 08             Existing class java.util.Date
   77 08 00 00 00 91 1B 4E B1 80  External storage (details later)
74 00 0C Harry Hacker          name field value: String
```

如你所见，数据文件包含足够的信息来恢复 `Employee` 对象。

数组按以下格式保存：

```
75          class descriptor          4-byte number of
                                      entries
```

类描述符中的数组类名采用与本地方法所用格式相同的格式（与其他类描述符中类名所用格式略有不同）。在此格式中，类名以 `L` 开头并以分号结尾。

例如，一个包含三个 `Employee` 对象的数组开头如下：

```
75                                      Array
   72 00 0B [LEmployee;               New class, string length, class name
                                      Employee[]
   FC BF 36 11 C5 91 11 C7 02       Fingerprint and flags
   00 00                             Number of instance fields
   78                                End marker
   70                                No superclass
   00 00 00 03                       Number of array entries
```

注意，`Employee` 对象数组的指纹与 `Employee` 类本身的指纹不同。

所有对象（包括数组和字符串）以及所有类描述符在保存到输出文件时都会被分配序列号。编号从 `00 7E 00 00` 开始。

我们已经看到，任何给定类的完整类描述符只出现一次。后续描述符会引用它。例如，在前面的示例中，对 `Date` 类的重复引用编码为

```
71 00 7E 00 08
```

同一机制也用于对象。如果写入对先前保存对象的引用，则会以完全相同的方式保存——即 `71` 后跟序列号。从上下文中总能清楚判断某个特定序列引用表示类描述符还是对象。

最后，空引用存储为

```
70
```

下面是上一节 *ObjectRefTest* 程序的带注释输出。运行该程序，查看其数据文件 *employee.dat* 的十六进制转储，并与带注释的清单进行比较。输出末尾附近的重要行展示了对先前保存对象的引用。

```
AC ED 00 05                    File header
75
   72 00 0B [LEmployee;        New class, string length, class name
                               Employee[] (serial #0)
      FC BF 36 11 C5 91 11 C7 02  Fingerprint and flags
      00 00                   Number of instance fields
      78                      End marker
      70                      No superclass
      00 00 00 03             Number of array entries
73                            staff[0]— new object (serial #7)
   72 00 07 Manager           New class, string length, class name
                              (serial #2)
      36 06 AE 13 63 8F 59 87 02  Fingerprint and flags
      00 01                   Number of data fields
      L 00 09 secretary       Instance field type and name
      74 00 0A LEmployee;     Instance field class name: Employee (serial #3)
      78                      End marker
   72 00 08 Employee          Superclass: new class, string length, class
                              name (serial #4)
      E6 D2 86 70 AE AC 18 18 02  Fingerprint and flags
      00 03                   Number of instance fields
      D 00 06 salary          Instance field type and name
      L 00 07 hireDay         Instance field type and name
      74 00 10 Ljava/util/Date;  Instance field class name: Date (serial #5)
      L 00 04 name            Instance field type and name
      74 00 12 Ljava/lang/String; Instance field class name: String (serial #6)
      78                      End marker
      70                      No superclass
40 F3 88 00 00 00 00 00    salary field value: double
73                          hireDay field value: new object (serial #9)
72 00 0E java.util.Date      New class, string length, class name
                             (serial #8)
68 6A 81 01 4B 59 74 19 03  Fingerprint and flags
00 00                      No instance variables
78                         End marker
70                         No superclass
77 08                      External storage, number of bytes
00 00 00 83 E9 39 E0 00    Date
78                         End marker

74 00 0C Carl Cracker       name field value: String (serial #10)
73                         secretary field value: new object
                             (serial #11)
71 00 7E 00 04             existing class (use serial #4)
40 E8 6A 00 00 00 00 00    salary field value: double
73                         hireDay field value: new object (serial #12)
71 00 7E 00 08             Existing class (use serial #8)
77 08                      External storage, number of bytes
00 00 00 91 1B 4E B1 80    Date
78                         End marker
74 00 0C Harry Hacker       name field value: String (serial #13)
71 00 7E 00 0B             staff[1]: existing object (use serial #11)
73                         staff[2]: new object (serial #14)
71 00 7E 00 02             Existing class (use serial #2)
40 E3 88 00 00 00 00 00    salary field value: double
73                         hireDay field value: new object (serial #15)
71 00 7E 00 08             Existing class (use serial #8)
77 08                      External storage, number of bytes
00 00 00 94 6D 3E EC 00    Date
78                         End marker
74 00 0B Tony Tester        name field value: String (serial #16)
71 00 7E 00 0B             secretary field value: existing object (use
                             serial #11)
```

当然，研究这些代码可能和读电话簿一样枯燥。知道确切的文件格式并不重要（除非你想通过修改数据来制造恶意效果），但了解序列化格式对其包含的所有对象都有详细描述，且细节足以重建对象和对象数组，仍然很有启发性。

你应该记住的是：

- 序列化格式包含所有对象的类型和数据字段。
- 每个对象都会被分配一个序列号。
- 同一对象的重复出现会存储为对该序列号的引用。

## 2.3.3 修改默认序列化机制

某些数据字段绝不应被序列化——例如，存储文件句柄或窗口句柄的整数值，这些句柄只对本地方法有意义。当你在以后重新加载对象或将其传输到另一台机器时，此类信息肯定无用。事实上，此类字段的不正确值实际上可能导致本地方法崩溃。Java 有一种简单的机制来防止此类字段被序列化：用关键字 `transient` 标记它们。如果字段属于可序列化类，你也需要将这些字段标记为 `transient`。序列化对象时，瞬态字段总会被跳过。

序列化机制为各个类提供了一种方式，可向默认读写行为添加验证或任何其他所需操作。可序列化类可以定义具有以下签名的方法：

```
private void readObject(ObjectInputStream in)
        throws IOException, ClassNotFoundException;
private void writeObject(ObjectOutputStream out)
        throws IOException;
```

然后，数据字段不再自动序列化——而是调用这些方法。

下面是一个典型示例。`java.awt.geom` 包中的许多类（例如 `Point2D.Double`）不可序列化。现在，假设你想序列化一个存储 `String` 和 `Point2D.Double` 的类 `LabeledPoint`。首先，需要将 `Point2D.Double` 字段标记为 `transient`，以避免 `NotSerializableException`。

```
public class LabeledPoint implements Serializable
{
    private String label;
    private transient Point2D.Double point;
    . . .
}
```
