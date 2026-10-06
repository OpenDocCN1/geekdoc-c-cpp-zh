

# 第 13 章解答 | C++

13.9 编写一个智能指针（smart_ptr）类。

# 答案

Smart_ptr 与普通指针相同，但它通过自动内存提供安全性。它避免了悬空指针、内存泄漏、分配失败等问题。智能指针必须为所有实例维护单一的引用计数。

```cpp
template <class T> class SmartPointer {
public:
    SmartPointer(T * ptr) {
        ref = ptr;
        ref_count = (unsigned*)malloc(sizeof(unsigned));
        ref_count = 1;
    }
    SmartPointer(SmartPointer<T> sptr) {
        ref = sptr.ref;
        ref_count = sptr.ref_count;
        ++ref_count;
    }
    SmartPointer<T> &operator=(SmartPointer<T> &sptr) {
        if (this != &sptr) {
            ref = sptr.ref;
            ref_count = sptr.ref_count;
            ++ref_count;
        }
        return *this;
    }
    ~SmartPointer() {
        --ref_count;
        if (*ref_count == 0) {
            delete ref;
            free(ref_count);
        }
        ref = NULL;
        ref_count = NULL;
    }
    T getValue() { return *ref; }
protected:
    T * ref;
    unsigned *ref_count;
};
```

![](img/50974dc108b2978cf2cacf9397df9934_230_0.png)

14.1 从继承的角度来看，将构造函数私有有什么影响？

# 答案

将构造函数声明为私有将确保类外部的人无法直接实例化类。在这种情况下，创建类实例唯一方法是提供一个静态公共方法，就像在使用工厂方法模式时那样。

此外，由于构造函数是私有的，该类也无法被继承。

# 第 14 章解答 | Java

在 Java 中，如果我们在 try-catch-finally 的 try 块内部插入 return 语句，finally 块还会执行吗？

第 78 页

# 答案

是的，它会被执行。

当 try 块存在时，finally 块会被执行。即使我们尝试在 try 块中退出（正常退出、return、continue、break 或任何异常），finally 块仍然会被执行。

> 注意：在某些情况下 finally 块不会执行：如果虚拟机在 try-catch 块执行期间退出，或者执行 try/catch 块的线程被杀死。

# 第 14 章解答 | Java

14.3 final、finally 和 finalize 之间有什么区别？

# 答案

### Final

- 应用于变量（基本数据类型）时：变量的值不能改变。
- 应用于变量（引用类型）时：引用变量不能指向堆上的任何其他对象。
- 应用于方法时：该方法不能被重写。
- 应用于类时：该类不能被子化。

### Finally

在 try 块之后或 catch 块之后有一个可选的 finally 块。finally 块中的语句始终会被执行（JVM 从 try 块退出的除外）。finally 块用于编写清理代码。

### Finalize

这是 JVM 在运行垃圾回收之前运行的方法。

# 第 14 章解答 | Java

14.4 解释 C++ 模板（templates）与 Java 泛型（generics）之间的区别。第 78 页

# 答案

| C++ 模板 | Java 泛型 |
| :--- | :--- |
| 类和函数可以是模板。 | 类和方法可以是泛型的。 |
| 参数可以是任何类型或整数值。 | 参数只能是引用类型（不是基本数据类型）。 |
| 编译时可能会为每个类型参数生成类或函数的独立副本。 | 只编译一个类或函数版本，适用于所有类型参数。 |
| 不同类型参数的类对象在运行时是不同的类型。 | 类型参数在编译时被擦除；具有不同参数的类对象在运行时是相同类型。 |
| 必须包含模板类或函数的实现源码（仅有声明是不够的）。 | 来自编译类文件中的类或方法签名即可使用。 |
| 模板可以特化 - 可以为特定的模板参数提供单独的实现。 | 泛型不能特化。 |
| 不支持通配符。相反，返回类型通常作为嵌套类型定义可用。 | 如果类型参数只使用一次，则支持通配符作为类型参数。 |
| 不直接支持类型参数的边界，但元编程提供了这一点。 | 通过 "extends" 和 "super" 分别支持上界和下界边界；允许强制类型参数之间的关系。 |
| 允许实例化类型参数的类。 | 不允许实例化类型参数的类。 |
| 模板类的类型参数用于静态方法和变量。 | 模板类的类型参数不能用于静态方法和变量。 |
| 静态变量不在不同类型参数的类之间共享。 | 静态变量在不同类型参数类的实例之间共享。 |

源自 http://en.wikipedia.org/wiki/Comparison_of_Java_and_C%28%29BTamples_vs.Generics

# 第 14 章解答 | Java

14.5 解释 Java 中的反射（reflection）以及它为什么有用。第 78 页

# 答案

反射是 Java 中的一种特性，允许你检查和修改应用程序的运行时行为。它提供了一种方法：

- 在运行时获取有关类、方法和字段的信息。
- 在编译时不知道确切类型的情况下创建类的新实例。
- 动态调用方法并获取/设置字段。

```java
import java.lang.reflect.*;

public class Sample {
    public static void main(String[] args) {
        try {
            Class<?> c = Class.forName("Sample");
            Method[] m = c.getDeclaredMethods();
            for (Method method : m) {
                System.out.println(method);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

反射有用在于：
1. 开发需要分析其他代码的工具和 IDE。
2. 创建使用依赖注入或 ORM 的框架（如 Spring 或 Hibernate）。
3. 实现需要访问私方法的单元测试框架。

14.6 假设你在程序中使用了一个 map，你会如何统计它出现的次数？

# 答案

要统计出现次数，你可以遍历 map 并使用计数器。

```java
import java.util.HashMap;
import java.util.Map;

public class Counter {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("apple", 1);
        map.put("banana", 2);
        map.put("apple", 3);

        Map<String, Integer> counts = new HashMap<>();
        for (String key : map.keySet()) {
            counts.put(key, counts.getOrDefault(key, 0) + 1);
        }
        System.out.println(counts);
    }
}
```

# 第 15 章解答 | 数据库

15.1 编写一个查询查找每个部门的员工人数。第 80 页

# 答案

这个问题使用 LEFT JOIN 来确保我们包含 0 个员工的部门。

```sql
SELECT Departments.Dept_Name, COUNT(Employees.Employee_ID) AS num_employees
FROM Departments
LEFT JOIN Employees ON Departments.Dept_ID = Employees.Dept_ID
GROUP BY Departments.Dept_Name;
```

# 第 15 章解答 | 数据库

15.2 有哪些类型的连接？请解释它们之间的区别以及为什么某些类型在某些情况下更好。第 80 页

# 答案

JOIN 用于合并两个表的结果。要执行连接，每个表必须至少有一个字段用于查找另一个表中的记录。连接类型定义了哪些记录将进入结果集。

- INNER JOIN：返回在两个表中都具有匹配值的记录。
- LEFT OUTER JOIN：返回左表的所有记录，以及右表中的匹配记录。如果没有找到匹配项，则右侧返回 NULL。
- RIGHT OUTER JOIN：返回右表的所有记录，以及左表中的匹配记录。
- FULL OUTER JOIN：当左表或右表中存在匹配项时，返回所有记录。

情况：
- 当你只需要在两个表中都存在的数据时，使用 INNER JOIN。
- 当你需要主表中的所有条目，无论它们在辅助表中是否有相关项时（例如查找所有部门，即使没有员工），使用 LEFT JOIN。

