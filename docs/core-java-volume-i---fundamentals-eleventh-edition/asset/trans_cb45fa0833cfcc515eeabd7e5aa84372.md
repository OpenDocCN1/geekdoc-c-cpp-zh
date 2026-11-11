
当程序运行时，Java 运行时系统会注意到这个被破坏的承诺，并生成一个 ClassCastException。如果你不捕获该异常，程序就会终止。因此，良好的编程实践是在尝试强制类型转换之前先判断它是否会成功。只需使用 instanceof 运算符即可。例如：

```java
if (staff[1] instanceof Manager)
{
    boss = (Manager) staff[1];
    . . .
}
```

最后，如果强制类型转换没有成功的机会，编译器就不会让你进行转换。例如，下面这个转换

```java
String c = (String) staff[1];
```

是一个编译时错误，因为 String 不是 Employee 的子类。

总结如下：

- 只能在继承层次结构内进行强制类型转换。
- 从超类转换为子类之前，使用 instanceof 进行检查。

**注意：** 测试

`x instanceof C`

在 x 为 null 时不会生成异常。它只会返回 false。这很合理：null 不指向任何对象，因此它当然不指向类型为 C 的对象。

实际上，通过强制类型转换来转换对象的类型通常并不是好主意。在我们的示例中，大多数情况下你不需要把 Employee 对象转换为 Manager 对象。getSalary 方法在这两个类的对象上都能正确工作。使多态得以工作的动态绑定会自动定位到正确的方法。

进行强制类型转换的唯一原因是要使用 Manager 特有的方法，例如 setBonus。如果由于某种原因你发现自己想在 Employee 对象上调用 setBonus，请想一想这是否表明超类存在设计缺陷。重新设计超类并添加一个 setBonus 方法可能是合理的。请记住，只需一个未捕获的 ClassCastException 就能终止你的程序。一般来说，最好尽量减少强制类型转换和 instanceof 运算符的使用。

**C++ 注意：** Java 使用 C 语言“糟糕旧时代”的强制类型转换语法，但其工作方式类似于 C++ 中安全的 dynamic_cast 操作。例如，

```java
Manager boss = (Manager) staff[1]; // Java
```

等同于

```cpp
Manager* boss = dynamic_cast<Manager*>(staff[1]); // C++
```

但有一个重要区别。如果转换失败，它不会产生 null 对象，而是抛出异常。从这个意义上说，它类似于 C++ 的引用转换。这很麻烦。在 C++ 中，你可以在一次操作中完成类型测试和类型转换。

```cpp
Manager* boss = dynamic_cast<Manager*>(staff[1]); // C++
if (boss != NULL) {
    ...
}
```

在 Java 中，你需要结合使用 instanceof 运算符和强制类型转换。

```java
if (staff[1] instanceof Manager)
{
    Manager boss = (Manager) staff[1];
    ...
}
```

## 5.1.9 抽象类

随着你在继承层次结构中向上移动，类会变得更通用，也可能更抽象。到了某个时候，祖先类会变得如此通用，以至于你更多地把它看作其他类的基础，而不是一个拥有你想使用的具体实例的类。例如，考虑一下我们 Employee 类层次结构的一个扩展。员工是人，学生也是人。让我们扩展类层次结构，加入 Person 和 Student 类。图 5.2 展示了这些类之间的继承关系。

为什么要费心使用这么高的抽象层次呢？有些属性对每个人来说都是有意义的，例如姓名。学生和员工都有姓名，引入一个共同的超类可以让我们把 getName 方法提取到继承层次结构中更高的层次。

现在让我们添加另一个方法 getDescription，它的用途是返回该人的简要描述，例如

```text
an employee with a salary of $50,000.00
a student majoring in computer science
```

为 Employee 和 Student 类实现这个方法很容易。但是，在 Person 类中你能提供什么信息呢？Person 类除了姓名之外对该人一无所知。当然，你可以实现

```java
return name;
}
}
```

**提示：** 有些程序员没有意识到抽象类可以有具体方法。你应当始终把公共字段和方法（无论是否为抽象）移到超类（无论是否为抽象）中。

抽象方法充当在子类中实现的方法的占位符。当你扩展一个抽象类时，有两种选择。你可以不定义部分或全部抽象方法；那么你必须把子类也标记为抽象。或者你可以定义所有方法，这样子类就不再是抽象类。

例如，我们将定义一个 Student 类，它扩展抽象类 Person 并实现 `getDescription` 方法。Student 类的方法都不是抽象的，因此它不需要声明为抽象类。

一个类即使没有抽象方法，也可以被声明为抽象类。

抽象类不能被实例化。也就是说，如果一个类被声明为抽象类，就不能创建该类的任何对象。例如，下面这个表达式

```java
new Person("Vince Vu")
```

是错误的。但是，你可以创建具体子类的对象。

注意，你仍然可以创建抽象类的*对象变量*，但这种变量必须引用非抽象子类的对象。例如：

```java
Person p = new Student("Vince Vu", "Economics");
```

这里，p 是抽象类型 Person 的变量，它引用非抽象子类 Student 的一个实例。

**C++ 注意：** 在 C++ 中，抽象方法称为*纯虚函数*，并用末尾的 `= 0` 标记，例如

```cpp
class Person // C++
{
public:
    virtual string getDescription() = 0;
    . . .
};
```

如果一个 C++ 类至少有一个纯虚函数，那么它就是抽象类。在 C++ 中，没有专门的关键字来表示抽象类。

让我们定义一个具体子类 Student，它扩展抽象类 Person：

```java
public class Student extends Person
{
    private String major;

    public Student(String name, String major)
    {
        super(name);
        this.major = major;
    }

    public String getDescription()
    {
        return "a student majoring in " + major;
    }
}
```

Student 类定义了 getDescription 方法。因此，Student 类中的所有方法都是具体的，该类不再是抽象类。

清单 5.4 所示的程序定义了抽象超类 Person（清单 5.5）和两个具体子类 Employee（清单 5.6）与 Student（清单 5.7）。我们用员工对象和学生对象填充一个 Person 引用数组：

```java
var people = new Person[2];
people[0] = new Employee(...);
people[1] = new Student(...);
```

然后，我们打印这些对象的姓名和描述：

```java
for (Person p : people)
    System.out.println(p.getName() + ", " + p.getDescription());
```

有些人对下面这个调用感到困惑

```java
p.getDescription()
```

这难道不是对未定义方法的调用吗？请记住，变量 p 从不引用 Person 对象，因为不可能构造抽象类 Person 的对象。变量 p 总是引用具体子类（例如 Employee 或 Student）的对象。对于这些对象，getDescription 方法是已定义的。

你能不能从 Person 超类中完全省略抽象方法，只在 Employee 和 Student 子类中定义 getDescription 方法呢？如果那样做，你就无法在变量 p 上调用 getDescription 方法。编译器会确保你只调用类中声明的方法。

抽象方法是 Java 编程语言中的一个重要概念。你最常会在*接口*中遇到它们。有关接口的更多信息，请参阅第 6 章。

### 清单 5.4 abstractClasses/PersonTest.java

```java
 1 package abstractClasses;
 2
 3 /**
 4  * This program demonstrates abstract classes.
 5  * @version 1.01 2004-02-21
 6  * @author Cay Horstmann
 7  */
 8 public class PersonTest
 9 {
10     public static void main(String[] args)
11     {
12         var people = new Person[2];
13
14         // fill the people array with Student and Employee objects
15         people[0] = new Employee("Harry Hacker", 50000, 1989, 10, 1);
16         people[1] = new Student("Maria Morris", "computer science");
17
18         // print out names and descriptions of all Person objects
19         for (Person p : people)
20             System.out.println(p.getName() + ", " + p.getDescription());
21     }
22 }
```

### 清单 5.5 abstractClasses/Person.java

```java
 1 package abstractClasses;
 2
 3 public abstract class Person
 4 {
 5     public abstract String getDescription();
 6     private String name;
 7
 8     public Person(String name)
 9     {
10         this.name = name;
11     }
12
13     public String getName()
14     {
15         return name;
16     }
17 }
```
