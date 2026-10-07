
- [API 2013] Annotation Type SuppWarnings
- [Bloch 2008] 项目 24, “消除未检查警告”
- [Long 2012] OBJ03-J. 不要在新代码中混合泛型与非泛型类型

# 24. 缩小类及其成员的访问权限

类和类成员（类、接口、字段和方法）在 Java 中受访问控制的。访问权限通过访问修饰符（`public`、`protected` 或 `private`）或通过缺少访问修饰符（默认访问，也称为包私有访问权限）来指示。

## 访问修饰符表

| 访问修饰符 | 类 | 包 | 子类 | 世界 |
|---|---|---|---|---|
| `private` | x | | | |
| 无 | | x | x* | |
| `protected` | | x | x | |
| `public` | x | x | x |

表格 2–1 展示了访问控制的简化视图。x 表示在领域内允许访问。例如，类列中的 x 表示在同一个类内允许。包列中的 x 表示在包内允许。子类列中的 x 表示在子类内允许。世界列中的 x 表示在世界范围内允许。

尽可能，类应该赋予最小访问权限。注意，即使非本地类的可见性是默认的，它也可能被误用。执行所有安全检查并清理所有输入的方法可以通过接口暴露。保护性访问对于非嵌套类无效，但嵌套类可以是保护的。非 `final` 类字段很少声明为保护；另一个包中的不受信任代码可以子类该类并访问成员。此外，成员是类的一部分，因此需要持续支持。遵循此规则时，没有必要将字段声明为保护。“OBJ01-J. 将数据成员声明为私并提供可访问的封装方法” [Long 2012] 建议将字段声明为私。

如果类、接口、方法或字段属于发布的 API（例如 Web 服务端点），则可以声明为公共。其他类和成员应该声明为包私有或私有。例如，鼓励非安全关键类提供公共静态工厂通过私有构造函数实现实例控制。

### 不合规代码示例 (公共类)

这个不合规代码示例定义了一个系统内部且不属于任何公共 API 的类。然而，该类被声明为公共。

```java
public final class Point {
    private final int x;
    private final int y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public void getPoint() {
        System.out.println("" + x + "," + y + ")");
    }
}
```

即使此示例符合“OBJ01-J. 将数据成员声明为私并提供可访问的封装方法” [Long 2012]，不受信任代码也可以实例化 `Point` 并调用公共的 `getPoint()` 方法获取坐标。

### 合规解决方案 (带有公共方法的最终类)

该合规解决方案根据其不属于公共 API 的状态，将 `Point` 类声明为包私有。

```java
final class Point {
    private final int x;
    private final int y;

    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public void getPoint() {
        System.out.println("" + x + "," + y + "");
    }
}
```

像 `Point` 这样的顶层类不能声明为 `private`。包私有（Package-private）访问权限是可以接受的，前提是避免包插入攻击。详见“ENV01-J. 将所有安全敏感代码放在单个 JAR 中并进行签名” [Long 2012]。包插入攻击发生在：在运行时，类的任何一个包私有成员都可以被恶意插入到相同包中的类直接调用。然而，这种攻击在实践中很难实施，因为除了需要渗透包权限外，目标类和不可信的类必须由同一个类加载器加载。不可信的代码通常被剥夺了这种程度的访问权限。

由于该类是 `final` 的，`getPoint()` 方法可以声明为 `public`。违反此规则的子类无法重写该方法并将其暴露给不可信代码，因此其访问权限是无关的。对于 `final` 类，将方法的访问权限降低到 `private` 或包私有可以消除这种威胁。

### 合规方案（带有非公共方法的非最终类）

此合规方案将 `Point` 类及其 `getPoint()` 方法声明为包私有，这允许 `Point` 类为非 `final` 类，并允许 `getPoint()` 被存在于相同包中且由公共类加载器加载的类调用。

```java
class Point {
    private final int x;
    private final int y;

    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    void getPoint() {
      System.out.println("" + x + "," + y + ")");
    }
}
```

### 不合规代码示例（带有公共静态方法的公共类）

此不合规代码示例定义了一个系统内部的类，不属于任何公共 API。尽管如此，该类被声明为 `public`。

```java
public final class Point {
  private static final int x = 1;
  private static final int y = 2;

  Point(int x, int y) {}
  public static void getPoint() {
    System.out.println("" + x + "," + y + ")");
  }
}
```

此示例也符合“OBJ01-J. 将数据成员声明为私并提供可访问的包装方法” [Long 2012]，不可信代码可以访问 `Point` 并调用公共静态方法 `getPoint()` 获取默认坐标。使用私有构造函数实现实例控制的尝试是徒劳的，因为公共静态方法暴露了类的的内容。

### 合规方案（包私有类）

此合规方案将类的访问权限降低到包私有。

```java
final class Point {
  private static final int x = 1;
  private static final int y = 2;

  Point(int x, int y) {}

  public static void getPoint() {
    System.out.println("" + x + "," + y + ")");
  }
}
```

对 `getPoint()` 方法的访问被限于位于相同包内的类。防止不可信代码调用 `getPoint()` 并获取坐标。

#### 适用性

授予过度访问会破坏封装并削弱 Java 应用程序的安全性。

一个设计供第三方代码使用（并可能扩展）的 API 系统必须通过公共接口暴露 API。此类 API 的需求优先于此准则。

对于任何代码，都可以计算每个类和成员的最小访问权限，以避免引入编译错误。局限性在于，计算结果可能与代码编写时的意图没有任何相似之处。例如，未使用的成员可以声明为 `private`。但因为所检查的特定代码体恰好缺少对这些成员的引用。尽管如此，这种计算可以为希望最小化类及其成员访问权限的程序员提供一个有用的起点。

#### 参考文献

- [Bloch 2008] Item 13, "Minimize the Accessibility of Classes and Members"
- [Campione 1996] Item 16, "Prefer Interfaces to Abstract Classes"
- [JLS 2013] Access Control §6.6, "Access Control"
- [Long 2012] ENV01-j. Place all security-sensitive code in a single JAR and sign and seal it
- OBJ1-j. Declare data members as private and provide accessible wrapper methods
- OBJ04-j. Provide mutable classes with copy functionality to safely allow instances to untrusted code
- [McGraw 1999] Chapter 3, "Java Language Security Constructs"

# 25. 记录线程安全性并在可用处使用注解

Java 语言的注解机制对于记录设计意图非常有用。源代码注解是一种将元数据与程序元素关联的机制，并使其供编译器、分析器、调试器或 Java 虚拟机（JVM）可用以进行检查。有多种注解可用于记录线程安全性或缺乏线程安全性。

## 获取并发注解

两组并发注解可以免费获取，并许可在任何代码中使用。第一组由四种注解组成，这些在《Java 并发编程》（Java Concurrency in Practice, JCIP）[Goetz 2006] 中描述，可以从 `http://jcip.net` 下载。JCIP 注释根据知识共享署名许可（Creative Commons Attribution License）发布。

第二组更大的并发注解集由 SureLogic 提供并支持。这些注解根据 Apache 软件许可证 2.0 发布，可以在 `www.surelogic.com` 下载。这些注解可以使用 SureLogic 工具进行验证，并且当工具不可用时它们仍然有用。这些注解包含了 JCIP 注释（SureLogic 也支持 JAR 文件）。

要使用这些注解，请将上述一个或两个 JAR 文件添加到代码构建路径中。使用这些注解记录线程安全性将在后续章节中描述。

## 记录线程安全性

JCIP 提供了三种类级注解来描述关于线程安全性的设计意图。

`@ThreadSafe` 注解应用于类，表示该类是线程安全的。这意味着无论运行时或调用者的外部同步或协调如何交错，对公共字段的读写以及公共方法的调用序列都不会让对象处于不一致状态。

例如，接下来的 `AircraftSafe` 类通过其锁定策略指定其是线程安全的。该类使用重入锁保护 `x` 和 `y` 字段。

```java
@ThreadSafe
@Region("AircraftState")
@RegionLock("StateLock protects AircraftState")
public final class Aircraft {
    private final Lock stateLock = new ReentrantLock();
    // ...
    @InRegion("AircraftState")
    private long x, y;
    // ...
}
```

`@Region` 和 `@RegionLock` 注解记录了作为安全性承诺的锁定策略。

当使用一个或多个 `@RegionLock` 或 `@GuardedBy` 注解来记录类的锁定策略时，`@ThreadSafe` 注解为评审人员提供了一个直观的注解，告知该类是线程安全的。

`@Immutable` 注解应用于不可变类。不可变对象是天然线程安全的；一旦完全构造，就可以通过引用并在多个线程之间安全地共享。

以下示例展示了一个不可变的 `Point` 类：

```java
@Immutable
public final class Point {
  private final int f_x;
  private final int f_y;

  Point(int x, int y) {
    f_x = x;
    f_y = y;
  }

  public int getX() {
    return f_x;
  }

  public int getY() {
    return f_y;
  }
}
```

根据 Joshua Bloch [Bloch 2008] 的观点：

没有必要记录枚举类型的不可变性。除非从返回类型显而易见，否则静态工厂必须记录返回对象的线程安全性，如 `Collections.synchronizedMap` 所示。

`@NotThreadSafe` 注解应用于非线程安全的类。许多类未能记录它们是否在多线程使用时是安全的。因此，程序员没有简单的方法来确定该类是否是线程安全的。该注解清晰地指示了类缺乏线程安全性。

例如，`java.util` 中提供的大多数集合实现都不是线程安全的。`java.util.ArrayList` 类可以这样记录此点：

```java
package java.util.ArrayList;

@NotThreadSafe
public class ArrayList<E> extends ... {
    // ...
}
```

## 文档化锁策略

记录所有用于保护共享状态的锁是非常重要的。根据 Brian Goetz 及其同事 [Goetz 2006] 的观点：

> 对于每个可能被多个线程访问的可变状态变量，对该变量的所有访问都必须在持有相同锁的情况下进行。在这种情况下，我们称该变量受该锁保护。（p. 28）

JCIP 为此目的提供了 `@GuardedBy` 注解，而 SureLogic 提供了 `@RegionLock` 注解。应用 `@GuardedBy` 注解的字段或方法只有在持有特定锁或动态锁（如 `java.util.concurrent.Lock`）时才能被访问。

例如，下面的 `MovablePoint` 类实现了一个可以使用 `memo` 数组列表记住过去位置的移动点：

```java
@ThreadSafe
public final class MovablePoint {

    @GuardedBy("this")
    double xPos = 1.0;
    @GuardedBy("this")
    double yPos = 1.0;
    @GuardedBy("itself")
    static final List<MovablePoint> memo = new ArrayList<MovablePoint>();

    public void move(double slope, double distance) {
      synchronized(this) {
        rememberPoint(this);
        xPos += (1 / slope) * distance;
        yPos += slope * distance;
      }
    }

    static void rememberPoint(MovablePoint value) {
      synchronized(memo) {
        memo.add(value);
      }
    }
}
```

`xPos` 和 `yPos` 字段上的 `@GuardedBy` 注解表示对这些字段的访问受持有 `this` 锁的保护。`move()` 方法也对 `this` 进行同步并修改了这些字段。`memo` 列表上的 `@GuardedBy` 注解表示 `ArrayList` 的锁保护其内容。`rememberPoint()` 方法也对 `memo` 列表进行了同步。

`@GuardedBy` 注解的一个问题是它无法指示类字段之间是否存在关系。这种限制可以通过使用 `@RegionLock` 注解来克服，该注解为应用于它的类声明了一个新的区域锁。该声明创建一个新锁，将特定锁与类的某个区域关联起来。只有在持有锁时才能访问该区域。例如，`SimpleLock` 锁策略指示对实例进行同步保护了其所有状态：

```java
@RegionLock("SimpleLock is this Instance")
class Simple { ... }
```

与 `@GuardedBy` 不同，`@RegionLock` 注解允许程序员为锁策略赋予一个显式的、并尽可能有意义的名字。

除了为锁策略命名外，`@Region` 注解还允许为被保护的状态区域命名。该名称能够清楚地表明状态和锁策略是归属于在一起的，如下例所示：

```java
@Region("private AircraftPosition")
@RegionLock("StateLock protects AircraftPosition")
public final class Aircraft {
    private final Lock stateLock = new ReentrantLock();

    @Region("AircraftPosition")
    private long x, y;

    @Region("AircraftPosition")
    private long altitude;
    // ...
    public void setPosition(long x, long y) {
        stateLock.lock();
        try {
            this.x = x;
            this.y = y;
        } finally {
            stateLock.unlock();
        }
    }
    // ...
}
```

在示例中，`stateLock` 保护了 `AircraftPosition`。

## 25. 尽可能记录线程安全性

### 可变对象的构造
