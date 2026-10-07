
```java
point.print_xy();

// 获取原始对象的拷贝

Point pointCopy = point.clone();

// pointCopy 现在持有指向

// 新克隆 Point 实例的唯一引用

// 修改拷贝对象的 x,y 的值

pointCopy.set_xy(5, 6);

// 原始值保持不变

point.print_xy();

}
}
```

`clone()`方法返回原始对象的拷贝，该拷贝反映了克隆瞬间原始对象的状态。这个新对象可以在不暴露原始对象的情况下使用。由于调用者仅持有指向新克隆实例的引用，调用者无法通过其操作更改实例变量。这种对`clone()`方法的使用允许该类保持安全的可变性。（参见“CERT® Oracle® Secure Coding Standard for Java” [Long 2012, “OBJ04-J. Prevent mutable classes with copy functionality to safely passing instances to untrusted code.)）

该类被声明为`final`，以防止子类通过重写`clone()`方法进行破坏。这使得该类适用于各种场景，而不会对原始对象产生任何意外修改。

## 73. 不要将引用的不可变性与被引用对象的不可变性混淆

### 不合规代码示例（数组）

此不合规代码示例使用了公有的静态`final`数组`items`：

```java
public static final String[] items = {/**/* . . */};
```

尽管将数组引用声明为`final`可以防止引用本身被修改，但客户端仍然可以修改数组的内容。

### 合规解决方案（索引 Getter）

此合规解决方案将数组设为私有，并提供公共方法来获取单个项目和数组大小：

```java
private static final String[] items = {/**/* . . */};

public static final String getItem(int index) {
    return items[index];
}

public static final int getItemCount() {
    return items.length;
}
```

直接访问数组对象本身是安全的，因为`String`是不可变的。

### 合规解决方案（拷贝数组）

此合规解决方案定义了一个私有数组以及一个返回数组拷贝的公共方法：

```java
private static final String[] items = {/* . . .*/};
public static final String getItems() {
  return items.clone();
}
```

由于返回的是数组的拷贝，客户端无法修改原始数组的值。注意，在处理对象数组时，可能需要手动深拷贝。这通常发生在对象没有导出`clone()`方法时。更多信息请参阅“OBJ06-J. Defensively copy mutable inputs and internal components” [Long 2012]。

与之前一样，该方法提供了对数组对象的直接访问，但这是因为`String`是不可变的。如果数组包含可变对象，`getItems()`方法可以返回一个包含克隆对象的数组。

### 合规解决方案（不可变包装器）

此合规解决方案声明了一个私有数组，并基于其构造了一个公有的不可变列表：

```java
private static final String[] items = {/* . . .*/};
public static final List<String> itemsList =
  Collections.unmodifiableList(Arrays.asList(items));
```

原始数组的值和公共列表都无法被客户端修改。关于不可变包装器的更多细节，请参阅指南 3，“Provide sensitive mutable classes with unmodifiable wrappers.” 当数组包含可变对象时，也可以使用此解决方案。

#### 适用性

错误地认为`final`引用会导致被引用对象的内容保持不可变，可能会导致攻击者修改被认为是不可变的对象。

因此，`writeUnShared()`和`readUnShared()`方法不适用于包含引用循环的数据结构的往返序列化。

考虑以下代码示例：

```java
public class Person {
    private String name;
    Person() {
        // 什么都不做 - 序列化需要
    }
    Person(String theName) {
        name = theName;
    }
    // 其他与此示例无关的细节
}

public class Student extends Person implements Serializable {
    private Professor tutor;
    Student() {
        // 什么都不做 - 序列化需要
    }
    Student(String theName, Professor theTutor) {
        super(theName);
        tutor = theTutor;
    }
    public Professor getTutor() {
        return tutor;
    }
}

public class Professor extends Person implements Serializable {
    private List<Student> tutees = new ArrayList<>();
    public boolean checkTutees() {
        boolean result = true;
        for (Student stu : tutees) {
            if (stu.getutor() != this) {
                result = false;
                break;
            }
        }
        return result;
    }
    public void addStudent(Student s) {
        tutees.add(s);
    }
}

Professor jane = new Professor("Jane");
Student able = new Student("Able", jane);
Student baker = new Student("Baker", jane);
Student charlie = new Student("Charlie", jane);
jane.addStudent(able);
jane.addStudent(baker);
jane.addStudent(charlie);

System.out.println("checkTutees returns: " + jane.checkTutees());
// 输出 "checkTutees returns: true"
```
```
// 使用 readShared 反序列化
try (ObjectInputStream ois = new ObjectStream(new FileInputStream(filename))) {
    Professor jane2 = (Professor)ois.readObject();
    System.out.println("checkTutees returns: " + jane2.checkTutees());
} catch (Throwable e) {
    // 处理错误
}
```

#### 适用性

在使用`readUnShared()`和`readUnShared()`方法对包含引用的数据结构进行循环序列化时，可能会产生意外的结果。

### 参考文献

+ [API 2013] Class ObjectOutputStream Class ObjectInputStream

# 75. 不要尝试通过将本地引用变量设置为 null 来帮助垃圾回收器

将本地引用变量设置为`null`以“帮助垃圾回收器”是没有必要的。这会增加代码的冗余并使维护变得困难。Java 即时编译器（JIT）可以执行等效的活跃性分析且无需实现。

一个相关的坏习惯是使用`finally`块将引用置空。更多细节请参见 Java CERT® 安全编码标准 [Long 2012], "MET12-J. Do not use finalizers"。

此准则专门适用于本地变量。对于显式删除对象有用的情况，请参见准则 49，“从长寿命容器对象中移除短寿命对象”。

## 不合规代码示例

在这个不合规的代码示例中，`buffer`是一个持有临时数组引用的本地变量。程序员试图在`buffer`数组不再需要时通过给其赋值`null`来帮助垃圾回收器。

```
// 本地作用域
int[] buffer = new int[100];
doSomething(buffer);
buffer = null;
```

### 合规解决方案

程序逻辑有时要求对本地变量引用的对象的生命周期进行严密控制。在需要此类控制的特殊情况下，请使用词法块来限制变量范围，因为当对象超出范围时，垃圾回收器可以立即回收该对象 [Bloch 2008]。

此合规解决方案使用词法块来控制`buffer`对象的生命周期：

```
// 限制 buffer 的范围
int[] buffer = new int[100];
doSomething(buffer);
```
