
# 第 5 章 程序员的误解

`volatile`关键字在此线程与任何设置`done`的线程之间建立了先行发生关系。

## 合规解决方案（Thread.interrupt()）

对于调用`sleep()`方法，更好的解决方案是使用线程中断，这会导致睡眠线程立即唤醒。

```java
final class ControlledStop implements Runnable {

    @Override public void run() {

    // 记录当前线程以便其他线程中断

    myThread = currentThread();

    while (!Thread.interrupted()) {

        try {

            Thread.sleep(1000);

        } catch (InterruptedException e) {

            Thread.currentThread().interrupt();

        }

    }

}

    public void shutdown(Thread th) {

        th.interrupt();

    }

}
```

中断线程必须知道中断哪个线程；此解决方案省略了这种跟踪逻辑。

## 不合规代码示例（getState()）

此不合规代码示例包含一个启动线程的`do()`方法。线程通过检查标志并等待通知来支持中断。`stop()`方法检查线程是否被阻塞；如果是，则将标志设为`true`并通知线程可以终止。

```java
public class Waiter {
    private Thread thread;
    private boolean flag;
    private final Object lock = new Object();

public void doSomething() {
    thread = new Thread(new Runnable() {
        @Override
        public void run() {
            synchronized (lock) {
                while (!flag) {
                    try {
                        lock.wait();
                        // ...
                    } catch (ruptedException e) {
                        // 转发给处理器
                    }
                }
            }
        }
    });
    thread.start();
}

public boolean stop() {
    if (thread != null) {
        if (thread.getState() == Thread.State.WAITING) {
            synchronized (lock) {
                flag = true;
                lock.notifyAll();
            }
            return true;
        }
    }
    return false;
}
```

遗憾的是，`stop()`方法错误地使用`getState()`方法来检查线程是否阻塞且在通知前终止。使用`getState()`方法进行同步控制是不恰当的。Java虚拟机（JVM）允许使用自来实现阻塞；因此，线程可以阻塞但不进入`WAITING`或`TIMED_WAITING`状态 [Goetz 2006]。因为线程可能永远不会进入`WAITING`状态，`stop()`方法可能无法终止线程。
即使`doSomething()`先调用，`stop()`方法也无法看到初始化的线程。如果这两个方法由同一个线程调用，它们自动具有先行发生关系，因此无法遇到此问题。

### 合规解决方案

此合规解决方案移除了判断线程是否处于`WAITING`状态的检查。这种检查是没有必要的，因为调用`notifyAll()`只影响阻塞在`wait()`调用之上的线程：

```java
public class Waiter {
    //...
    private Thread thread;
    private volatile boolean flag;
    private final Object lock = new Object();
    public boolean stop() {
        if (thread != null) {
            synchronized (lock) {
                flag = true;
                lock.notifyAll();
            }
            return true;
        }
        return false;
    }
}
```

### 适用性

依赖`Thread`类的`sleep()`、`yield()`和`getState()`方法进行同步控制可能会导致意外行为。

### 参考文献

- [Goetz 2006]
- [JLS 2013]

§17.3, “Sleep and Yield”

> 68. 不要假设余数运算符对于整数操作数总是返回非负结果

JLS, §15.17.3, “余数运算符 %” [JLS 2013] 规定：

对于经过二进制提升后为整数的操作数 (§5.6.2)，其余数操作产生一个结果值，使得 `(a/b)*b+(a%b)` 等于 `a`。即使在被除数为该类型最大可能绝对值的负整数，且除数为 `-1` 的特殊情况下（余数为 `0`），该等式依然成立。

# 68. 不要假设余数运算符总是返回非负结果

根据此规则，余数操作的结果只有在被除数为负数时才可能为负，在被除数为正数时可能为正；此外，结果的绝对值始终小于除数的绝对值。

余数运算符的结果与被除数（表达式中的第一个操作数）符号相同：

```
5 % 3 produces 2
5 % (-3) produces 2
(-5) % 3 produces -2
(-5) % (-3) produces -2
```

因此，依赖余数操作始终返回正结果的代码是错误的。

# 不合规代码示例

此不合规代码示例使用整数`hashKey`作为数组的索引：

```java
private int SIZE = 16;
public int[] hash = new int[SIZE];
public int lookup(int hashKey) {
    return hash[hashKey % SIZE];
}
```

负的`hash key`会导致余数运算符产生负结果，导致`lookup()`方法抛出`java.lang.ArrayIndexOutOfBoundsException`。

### 合规解决方案

此合规解决方案调用`imod()`方法，该方法始终返回正余数：

```java
// 方法 imod() 给出非负结果
private int SIZE = 16;
public int[] hash = new int[SIZE];
```

```java
private int imod(int i, int j) {
    int temp = i % j;
    // 一元负操作不会产生溢出
    // 因为 temp 不可能是 Integer.MIN_VALUE
    return (temp < 0) ? -temp : temp;
}
```

```java
public int lookup(int hashKey) {
    return hash[imod(hashKey, SIZE)];
}
```

### 适用性

错误地假设余数操作会返回正余数会导致错误的代码。

### 参考文献

[JLS 2013] §17.3, "Remainder Operator %"

# 69. 不要混淆抽象对象的相等性与引用相等

Java 定义了相等运算符`==`和`!=`来测试引用相等性，但使用`Object`及其子类中定义的`equals(Object)`方法来测试抽象对象的相等性。初级程序员经常混淆`==`操作意图与`Object.equals(Object)`方法意图。这种混淆在处理字符串的上下文中非常常见。

一条通用规则是：使用`Object.equals()`方法检查对象是否具有等效内容，使用相等运算符`==`和`!=`测试两个引用是否具体指向同一个对象。后者被称为引用相等性（referential equality）。对于重写了默认`equals()`实现的类，必须同时重写`hashCode()`方法。“Java CERT™ 安全编码标准” [Long 2012], “MET09-J. 定义了 equals() 的类也必须定义 hashCode()”

数值包装类型（例如，Byte、Character、Short、Integer、Long、Float 和 Double）也应该使用`Object.equals()`进行比较，尽管`==`运算符对于范围在 -128 到 127 之间的 Integer 值似乎有效，但如果任一操作数在该范围之外，它可能会失效。相等以外的数值运算符（如 `<`, `<=`、>` 和 `>=`）可以安全地用于比较包装的原始类型（更多信息请参见“EXP03-J. 比较包装原始类型的值时不要使用相等运算符” [Long 2012]）。

# 69. 不要混淆抽象对象的相等性与引用相等

# 不合规代码示例

此不合规代码示例声明了两个包含相同值的 String 对象：

```java
public class StringComparison {
    public static void main(String[] args) {
        String str1 = new String("one");
        String str2 = new String("one");
        System.out.println(str1 == str2); // 打印 "false"
    }
}
```

引用相等性`==`仅在它们是同一个对象时才为 true。此示例中的引用是不相等的，因为它们指向不同的对象。

# 合规解决方案 (Object.equals())

此合规解决方案在比较字符串值时使用`Object.equals()`方法：

```java
public class StringComparison {
    public static void main(String[] args) {
        String str1 = new String("one");
        String str2 = new String("one");
        System.out.println(str1.equals(str2)); // 打印 "true"
    }
}
```

# 合规解决方案 (String.intern())

此合规解决方案使用`String.intern()`，当内存中只需要字符串副本时可以进行快速字符串比较。

```java
public class StringComparison {
    public static void main(String[] args) {
        String str1 = new String("one");
        String str2 = new String("one");
        str1 = str1.intern();
        str2 = str2.intern();
        System.out.println(str1 == str2); // 打印 "true"
    }
}
```

JLS 对`String.intern()`的实现提供的保证很少。例如：

- `String.intern()`的成本随着内部字符串数量增加而增加。性能不应差于 O(n log n)，但 JLS 缺乏具体的性能保证。
- 在早期 Java 虚拟机 (JVM) 实现中，内部字符串是永存的：它们不受垃圾回收的影响。这在内部化大量字符串时可能会出现问题。较新的实现会回收不再被引用的内部字符串所占空间。然而，JLS 缺乏对这种行为的规范。
- 在 Java 1.7 之前的 JVM 实现中，内部字符串分配在永久代区域（perm generation region），该区域通常比堆的其他部分小得多。因此，增加大量字符串会导致内存溢出。在许多 Java 1.7 实现中，内部字符串分配在堆上，消除了这一限制。再次，JLS 未规定分配的细节；因此，实现可能有所不同。

# 70. 理解位运算符与逻辑运算符之间的区别 225

当需要对对象进行规范化时，使用构建在`ConcurrentHashMap`之上的自定义规范化器可能更为明智；详情请参见 Joshua Bloch 的《Effective Java》第二版第 69 条 [Bloch 2008]。

### 适用性

混淆引用相等性和对象相等性会导致意外的。。只有在定义类保证了对于每个可能的对象值最多只有一个对象实例时，才允许用引用相等性代替对象相等性。使用静态工厂方法而非公共构造函数有助于实例控制；这是一项关键启用技术。另一种技术是使用枚举（enum）类型。

使用引用相等性来判断两个引用是否指向同一个对象。

### 参考文献

- [Bloch 2008] Item 69, "Prefer Concurrency Utilities to wait and notify" 
- [FindBugs 2008] ES, "Comparison of String Objects == or !="
- $3.10.5, "String Literals"
- [JLS 2013] $5.6.2, "Binary Numeric Promotion"
- [Long 2012] EXP03-J. Do not use the equality operators when comparing valued primitives
- MET09-J. Classes that define an equals() method must also define a hashCode() method

# 70. 理解位运算符与逻辑运算符之间的区别

条件与和条件或运算符（分别为`&&`和`||`）表现出短路行为。也就是说，只有当无法通过评估第一个操作数推导出条件运算符的结果时，才会评估第二个操作数。因此，当条件运算符的结果仅从第一个操作数就能推断时，第二个操作数保持不被评估；其副作用（如果有）将永远不会发生。

位与和位运算符（`&`和`|`）缺乏短路行为。与大多数 Java 运算符类似，它们会评估两个操作数。它们分别返回与`&&`和`||`相同的布尔结果，但根据第二个操作数是否存在副作用，可能会产生不同的影响。

# 第 5 章 | 程序员误区

因此，在执行布尔逻辑时，可以使用`&`或`&&`运算符。然而，在某些情况下倾向于短路行为，而在另一些情况下，短路行为又会导致微妙的错误。

## 不合规代码示例（不当的 &）

此不合规代码示例源自 Flanagan [Flanagan 2005]，包含两个未知值的变量。代码必须验证数据，并检查`array[i]`是否为有效索引。

```java
int array[]; // 可能为 null
int i; // 可能为 array 的无效索引
if (array != null && i >= 0) {
  if (i < array.length && array[i] >= 0) {
    // 使用 array
  } else {
    // 处理错误
  }
}
```

这段代码可能会由于它试图防止的相同错误而失败。当`array`为空或不是有效索引时，对`array`和`array[i]`的引用将导致抛出`NullPointerException`或`ArrayOutOfBoundsException`。异常的发生是因为`&`运算符未能防止右侧操作数的评估，即使对左侧操作数的评估已证明右侧操作数无关。

## 合规解决方案（使用 &&）

此合规解决方案通过使用`&&`缓解了问题，`&&`导致如果任何条件失败，条件表达式的评估立即终止，从而防止运行时异常：

```java
int array[]; // 可能为 null
int i; // 可能为 array 的无效索引
if (array != null && i >= 0) {
  if (i < array.length && array[i] >= 0) {
    // 处理 array
  } else {
    // 处理错误
  }
}
```

## 合规解决方案（嵌套 if 语句）

此合规解决方案使用多个`if`语句来实现正确的效果。

```java
int array[]; // 可能为 null
int i; // 可能为 array 的有效索引
if (array != null) {
    if (i >= 0 && i < array.length) {
        if (array[i] >= 0) {
            // 使用 array
        } else {
```
