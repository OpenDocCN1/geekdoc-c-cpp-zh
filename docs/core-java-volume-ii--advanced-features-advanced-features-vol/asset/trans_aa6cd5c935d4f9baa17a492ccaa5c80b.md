
代码清单 12.11 和 12.12 展示了一个测试程序和 Employee 类的 Java 代码。代码清单 12.13 包含本地 raiseSalary 方法的 C 代码。

### 代码清单 12.11 employee/EmployeeTest.java

```java
/**
 * @version 1.11 2018-05-01
 * @author Cay Horstmann
 */

public class EmployeeTest
{
   public static void main(String[] args)
   {
      var staff = new Employee[3];

      staff[0] = new Employee("Harry Hacker", 35000);
      staff[1] = new Employee("Carl Cracker", 75000);
      staff[2] = new Employee("Tony Tester", 38000);

      for (Employee e : staff)
         e.raiseSalary(5);
      for (Employee e : staff)
         e.print();
   }
}
```

### 代码清单 12.12 employee/Employee.java

```java
/**
 * @version 1.10 1999-11-13
 * @author Cay Horstmann
 */

public class Employee
{
   private String name;
   private double salary;

   public native void raiseSalary(double byPercent);

   public Employee(String n, double s)
   {
      name = n;
      salary = s;
   }
}
```

## 12.5 编码签名

要访问 Java 编程语言中定义的实例字段并调用方法，你需要学习“改编”数据类型名称和方法签名的规则。（方法签名描述方法的参数和返回类型。）以下是编码方案：

| 代码 | 含义 |
|---|---|
| `B` | 字节型 |
| `C` | 字符型 |
| `D` | 双精度浮点型 |
| `F` | 单精度浮点型 |
| `I` | 整型 |
| `J` | 长整型 |
| `Lclassname;` | 类类型 |
| `S` | 短整型 |
| `V` | 无返回值 |
| `Z` | 布尔型 |

要描述数组类型，请使用 `[`。例如，字符串数组为

```text
[Ljava/lang/String;
```

float[][] 被改编为

```text
[[F
```

要获得方法的完整签名，请在一对括号内列出参数类型，然后列出返回类型。例如，接收两个整数并返回一个整数的方法编码为

```text
(II)I
```

第 819 页第 12.3 节“字符串参数”中的 sprint 方法具有以下改编后的签名：

```text
(Ljava/lang/String;D)Ljava/lang/String;
```

也就是说，该方法接收一个 String 和一个 double，并返回一个 String。

请注意，L 表达式末尾的分号是类型表达式的终止符，而不是参数之间的分隔符。例如，构造函数

```text
Employee(java.lang.String, double, java.util.Date)
```

的签名为

```text
(Ljava/lang/String;DLjava/util/Date;)V
```

请注意，`D` 和 `Ljava/util/Date;` 之间没有分隔符。另请注意，在此编码方案中，必须使用 `/` 而不是 `.` 来分隔包名和类名。末尾的 `V` 表示返回类型为 void。尽管在 Java 中不为构造函数指定返回类型，但仍需在虚拟机签名中添加 `V`。

> **提示：** 可以使用 `javap` 命令及 `-s` 选项从类文件生成方法签名。例如，运行
>
> `javap -s -private Employee`
>
> 将得到以下输出，显示所有字段和方法的签名：

```text
Compiled from "Employee.java"
public class Employee extends java.lang.Object{
  private java.lang.String name;
    Signature: Ljava/lang/String;
  private double salary;
    Signature: D
  public Employee(java.lang.String, double);
    Signature: (Ljava/lang/String;D)V
  public native void raiseSalary(double);
    Signature: (D)V
  public void print();
    Signature: ()V
  static {};
    Signature: ()V
}
```

> **注意：** 强迫程序员对签名使用这种改编方案没有任何道理。本地调用机制的设计者本来也可以轻松编写一个函数，以 Java 编程语言风格读取签名，例如 `void(int,java.lang.String)`，并将其编码为他们偏好的任意内部表示。不过话又说回来，使用改编后的签名可以让你体验贴近虚拟机编程的神秘感。

## 12.6 调用 Java 方法

当然，Java 编程语言函数可以调用 C 函数——这正是本地方法的用途。能否反过来呢？我们究竟为什么要这样做？经常会出现本地方法需要向传给它的对象请求服务的情况。我们将首先展示如何对实例方法执行此操作，然后展示如何对静态方法执行此操作。

### 12.6.1 实例方法

作为从本地代码调用 Java 方法的示例，让我们增强 Printf 类并添加一个类似于 C 函数 fprintf 的方法。也就是说，它应能将字符串打印到任意 PrintWriter 对象上。以下是该方法的 Java 定义：

```java
class Printf3
{
    public native static void fprintf(PrintWriter out, String s, double x);
    . . .
}
```

我们首先将要打印的字符串组装到 String 对象 str 中，就像我们已经实现的 sprint 方法一样。然后，在实现该本地方法的 C 函数中，我们将调用 PrintWriter 类的 print 方法。

可以使用以下函数调用从 C 中调用任何 Java 方法

```c
(*env)->CallXxxMethod(env, implicit parameter, methodID, explicit parameters)
```

根据方法的返回类型，将 Xxx 替换为 Void、Int、Object 等。正如访问对象字段需要 fieldID 一样，调用方法需要方法 ID。要获取方法 ID，请调用 JNI 函数 GetMethodID，并提供类、方法名和方法签名。

在我们的示例中，我们希望获取 PrintWriter 类的 print 方法的 ID。PrintWriter 类有几个名为 print 的重载方法。因此，还必须提供一个字符串，描述要使用的特定函数的参数和返回值。例如，我们想使用 void print(java.lang.String)。如上一节所述，现在必须将签名“改编”为字符串“(Ljava/lang/String;)V”。

以下是进行方法调用的完整代码：

```c
/* get the class of the implicit parameter */
jclass class_PrintWriter = (*env)->GetObjectClass(env, out);

/* get the method ID */
jmethodID id_print = (*env)->GetMethodID(env, class_PrintWriter, "print", "(Ljava/lang/String;)V");

/* call the method */
(*env)->CallVoidMethod(env, out, id_print, str);
```

代码清单 12.14 和 12.15 展示了测试程序和 Printf3 类的 Java 代码。代码清单 12.16 包含本地 printf 方法的 C 代码。

> **注意：** 数值方法 ID 和字段 ID 在概念上类似于反射 API 中的 Method 和 Field 对象。可以使用以下函数在它们之间进行转换：
>
> ```c
> jobject ToReflectedMethod(JNIEnv* env, jclass class, jmethodID methodID);
>     // returns Method object
> methodID FromReflectedMethod(JNIEnv* env, jobject method);
> jobject ToReflectedField(JNIEnv* env, jclass class, jfieldID fieldID);
>     // returns Field object
> fieldID FromReflectedField(JNIEnv* env, jobject field);
> ```

### 12.6.2 静态方法

从本地方法调用静态方法与调用实例方法类似。有两个区别：

- 使用 `GetStaticMethodID` 和 `CallStaticXxxMethod` 函数
- 调用方法时提供 `class` 对象，而不是隐式参数对象

作为示例，让我们从本地方法中调用静态方法

```java
System.getProperty("java.class.path")
```

该调用的返回值是一个给出当前类路径的字符串。

首先，必须找到要使用的类。由于没有现成的 `System` 类对象，我们使用 `FindClass` 而不是 `GetObjectClass`。

```c
jclass class_System = (*env)->FindClass(env, "java/lang/System");
```

接下来，需要静态 `getProperty` 方法的 ID。该方法的编码签名是

```c
"(Ljava/lang/String;)Ljava/lang/String;"
```

因为参数和返回值都是字符串。因此，我们按如下方式获取方法 ID：

```c
jmethodID id_getProperty = (*env)->GetStaticMethodID(env, class_System, "getProperty",
    "(Ljava/lang/String;)Ljava/lang/String;");
```

