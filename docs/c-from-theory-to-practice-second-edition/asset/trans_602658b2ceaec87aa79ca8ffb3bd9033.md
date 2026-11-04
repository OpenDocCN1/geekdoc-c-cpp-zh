
```java
class MainClass {
    public static void main(String[] args) {
        Test t1 = new Test();
        Test t2 = new Test(5, 10);

        System.out.println(t1.a + " " + t1.b);
        System.out.println(t2.a + " " + t2.b);
    }
}
```

我们稍后会讨论重载，但很容易观察到，`Test` 类有两个重载构造函数，名称完全相同，但参数不同。编译器会检查参数并调用相应的构造函数。因此，当创建 `t1` 实例时，会调用第一个构造函数，程序显示 no-param constructor called。当创建 `t2` 时，会调用第二个构造函数，程序显示 param constructor called。

类的未初始化字段会用默认值初始化（例如，算术类型为 0，……），而方法中未初始化的局部变量会被赋予随机值。因此，程序显示 `t1` 字段的值为 0 和 0，`t2` 字段的值为 5 和 10。

`this` 关键字用于类的方法和构造函数中，指代当前实例，即其方法或构造函数已被调用的实例。由于第二个构造函数的参数与 `a` 和 `b` 字段同名，我们使用 `this` 来引用它们。例如，`this.a` 引用 `t2` 实例的字段 `a`。当然，如果我们使用不同的名称，就不需要 `this`。例如：

```java
Test(int i, int j) {
    System.out.println("param constructor called");
    a = i;
    b = j;
}
```

尽管使用不同的名称完全合法，但常见的做法是使用相同的名称，并使用 `this` 引用类字段。

你可能想知道我们什么时候会讨论 Java 中的析构函数。答案是永远不会！如前所述，垃圾回收器是 Java 的原生机制，会自动负责释放不再使用的内存。因此，与 C++ 不同，Java 程序员无法定义析构函数来按需销毁对象，因为 Java 垃圾回收器会自行完成这项工作。

## 访问修饰符和非访问修饰符

Java 访问修饰符应用于类、接口和类成员，即字段、方法和构造函数，以定义对它们的访问权限。

`public` 访问修饰符可应用于类或接口，并声明它可以被任何其他类或接口访问。如果未使用访问修饰符，则该类或接口只能被同一包中的类或接口访问。因此，缺少访问修饰符也称为包私有或友好访问。

同样，有四种访问修饰符可应用于类的成员。`public` 修饰符使成员可被任何其他类访问，而缺少访问修饰符则使成员只能被同一包中的类访问。`private` 修饰符声明该成员只能在其自身类内访问。最后，`protected` 修饰符声明该成员只能被同一包中的类或其子类访问，即继承包含该成员的类的类。表 19.1 描述了根据所应用的访问修饰符，类成员的访问权限。

即使未应用 `public` 修饰符，接口的成员也可以被任何类访问。我们稍后会讨论接口。

非访问修饰符的目的是为类、接口、字段、方法和构造函数定义除可访问性之外的额外属性。非访问修饰符如下：`static`、`final`、`abstract`、`synchronized`、`native`、`strictfp`、`transient` 和 `volatile`；如果存在访问修饰符，它们必须位于访问修饰符之后。我们将简要介绍前三个。其余修饰符较为专用，超出入门章节的范围。

`static` 修饰符只能应用于类的字段和方法，或应用于必须嵌套在其他类中的类。静态字段属于类，而不属于类的实例。因此，即使我们创建同一个类的多个实例，静态字段也只创建一次，并且所有实例共享同一个字段。

> 由于静态字段属于类而不属于类的实例，因此即使尚未创建任何实例，也可以访问它。另一方面，要访问非静态字段，必须先创建实例。这就是非静态字段也称为实例字段的原因。

例如，在以下程序中，无需创建 `A` 的实例即可访问静态字段 `x`：

```java
class A {
    public static int x = 5;
    public int y = 55;
}

class MainClass {
    public static void main(String[] args) {
        System.out.println(A.x);
        System.out.println(A.y);
    }
}
```

### 表 19.1
访问修饰符

| 访问修饰符 | 类内 | 包内 | 被子类访问 | 被任何类访问 |
|---|---|---|---|---|
| public | ✓ | ✓ | ✓ | ✓ |
| protected | ✓ | ✓ | ✓ | × |
| （无） | ✓ | ✓ | × | × |
| private | ✓ | × | × | × |

然而，对于非静态字段 `y` 并非如此。因此，编译器将产生错误消息。在另一个示例中，以下程序的输出是什么？

```java
class A {
    public static int x = 5;
    public int y = 55;
}

class MainClass {
    public static void main(String[] args) {
        A a1 = new A();
        A a2 = new A();

        System.out.println(A.x + " " + a1.x + " " + a2.x);
        System.out.println(a1.y + " " + a2.y);

        a2.x = 2;
        a2.y = 22;
        System.out.println(A.x + " " + a1.x + " " + a2.x);
        System.out.println(a1.y + " " + a2.y);
    }
}
```

起初，程序显示 5 5 5 和 55 55。然后，`a2` 实例更改了静态字段 `x` 的值，而该字段是类 `A` 及其所有实例共有的字段。由于 `y` 是非静态字段，其值的任何更改都不会影响其他实例中的 `y` 字段。因此，程序输出：2 2 2 和 55 22。

`static` 修饰符也用于声明静态方法，也称为类方法，因为它属于类而不属于类的实例。与静态字段一样，调用静态方法不需要创建类的实例。`main()` 方法就是静态方法的一个示例，因为它可以在未创建 `MainClass` 实例的情况下被调用。

`final` 修饰符可应用于类、类的字段和方法，或方法的局部变量。尽管我们尚未讨论继承和多态，但理解其工作方式并不难。`final` 类被视为最终类；也就是说，它不能被扩展并拥有子类。换句话说，`final` 类不能被继承。例如：

```java
final class A { ... }

class B extends A { ... } /* Not allowed. */
```

不允许重写 `final` 方法。例如：

```java
public class A {
    public int m1(int x, int y) {
        return x+y;
    }
    public final void m2(String s) {
        System.out.println("Method m2 in class A prints: "+s);
    }
}
```

```java
public class B extends A { /* Class B is a subclass of class A. */
    public int m1(int x, int y) {
        return x-y;
    }
    public void m2(String s) {
        System.out.println("Method m2 in class B prints: "+s);
    }
}
```

类 `B` 继承类 `A`；也就是说，`B` 是 `A` 的子类。由于类 `A` 的 `m1()` 未声明为 `final`，因此允许被子类 `B` 的 `m1()` 方法重写。另一方面，由于 `m2()` 是 `final`，因此不允许被子类 `B` 的 `m2()` 重写。因此，编译器将产生错误消息。

`final` 字段或方法中的 `final` 局部变量只能被赋值一次，并且该值之后不能更改。在以下代码中，字段 `C_STR` 的值将是常量，等于 "Constant_String"。请注意，该值在类 `A` 的所有实例中都相同。

```java
public class A {
    public final String C_STR = "Constant_String";
}
```

由于 `final` 字段的值不能更改，常见的做法是同时将其声明为 `static`，以使其属于类而不属于类的实例。`final` 字段通常所有字母都大写命名。如果字段声明为 `final` 但未初始化，则必须在类的构造函数中初始化；否则，编译器将引发错误消息。

`abstract` 修饰符可应用于方法、类和接口。抽象方法没有实现，只有签名（在 C/C++ 术语中称为原型）。由于它未实现，因此不能声明为 `final`。在以下示例中，有两个方法声明为抽象方法：

```java
public abstract class A {
    public int m1(int x, int y) {
        return x*y;
    }
    public abstract float m2(float f1, float f2);
    public abstract void m3();
}
```

请注意，`m1()` 已实现，而只提供了 `m2()` 和 `m3()` 的签名。

![](img/b8da5dcf9ba7f1fad5213c453d095246_639_0.png)

包含一个或多个抽象方法的类必须声明为抽象类。

抽象类的每个子类都必须通过实现父类的抽象方法来重写它们。否则，该子类也必须声明为抽象类，并让其自己的子类重写它们。考虑到这一点，以下代码中的类 `B` 能否成为前面类 `A` 的子类？

```java
public abstract class B extends A {
    public float m2(float f1, float f2) {
```
