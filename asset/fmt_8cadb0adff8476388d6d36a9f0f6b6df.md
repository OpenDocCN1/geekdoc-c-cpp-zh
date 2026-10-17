
```java
abstract String sound();

public String speak() {
    return name + " says " + sound();
}
}
```

```java
class Horse extends Animal {
    public Horse(String name) {
        super(name);
    }
    @Override String sound() {
        return "neigh";
    }
}
```

```java
class Cow extends Animal {
    public Cow(String name) {
        super(name);
    }
    @Override String sound() {
        return "mooooo";
    }
}
```

```java
class Sheep extends Animal {
    public Sheep(String name) {
        super(name);
    }
    @Override String sound() {
        return "baaaa";
    }
}
```

```java
public class AnimalsApp {
    public static void main(String[] args) {
        Animal s = new Horse("CJ");
        assert s.speak().equals("CJ says neigh");
        Animal c = new Cow("Bessie");
        assert c.speak().equals("Bessie says mooooo");
        assert(new Sheep("Little Lamb").speak().equals("Little Lamb says baaaa"));
    }
}
```

# Java 127

动物层级结构的版本与之前的章节有很大不同。期望子类实现特定方法（在我们在本例中为 `sound`）的父类必须显式地声明该抽象方法。扩展抽象类的类要么实现其父类的所有方法，要么声明自己本身是抽象的。在之前的任何章节中，都需要这种声明。我们本可以在 CoffeeScript、Python、Ruby 或 Julia 中调用没有实现 `sound` 方法的 `speak` 方法，这会导致运行时错误。在 Java 中，这样的子类是不存在的——尝试在不重写抽象方法的情况下创建具体子类将产生编译错误。

继承适用于字段和方法。子类不继承父类的构造函数；然而，它们可以在自己的构造函数内部通过 `super` 关键字引用父类构造函数。重定义具体父类方法或为抽象父类提供抽象方法实现的子类被称为重写（override）了该方法。程序员可以使用 `@Override` 注解来标记方法重写。

## 7.3 接口

Java 接口定义了一组相关的常量和方法，提供了一个合约或程序接口（API），实现类必须遵循该合约。接口的作用（非常！）非常像抽象类；它定义了一个新的引用类型，可以包含抽象方法，并且不能实例化。虽然抽象类可以定义属于具体子类实例的（非静态）字段以及非公共方法，但接口不能。接口始终是 public、static 和 final 的（无论是否使用了这些修饰符），并且所有接口方法都是 public 的（无论是否写了该修饰符）。未标记为 `default` 或 `static` 的都是抽象的。

以下接口定义了两个抽象方法：

```java
interface Drawable {
    void outline(Color color);
    void fill(Color color);
}
```

最初，Java 接口只能包含抽象方法。因此，一个接口意味着会破坏实现该接口的现有类。现代 Java 允许接口定义默认方法和静态方法，并且都带有实现，因此库维护者可以将这些方法添加到接口中。虽然 `@Override` 注解是可选的，但它被认为是最佳实践。即使没有注解，方法名或签名中的拼写错误也会导致子类中产生一个新方法，从而导致运行时难以调试的错误。

### 编程语言探索

```java
interface Drawable {
  void outline(Color color);
  void fill(Color color);
  default void render(Color outlineColor, Color fillColor) {
    fill(fillColor);
    outline(outlineColor);
  }
}
```

Java 类最多扩展一个父类，尽管它允许类实现任意数量的接口。将扩展限制在单个子类很好地防止了一个类继承两个或多个相同名称和类型的（实例）字段，或两个或多个同名不同签名的方法——这种情况被称为多重继承。这是一个明智的举措，也许多重继承会引发问题：两个字段都被继承了吗？还是只有第一个？两个方法都被继承了吗？如果只一个，是哪一个？是否存在像我们在 Python 中看到的那种方法解析顺序？

但 Java 允许实现多个接口。这是否会导致带有所有消除歧要求的的多重继承？让我们看看给定：

```java
interface A {
  int X = 1; // 隐式 static final
  default void f() {} // 隐式 public
}
```

```java
interface B {
  int X = 2; // 隐式 static final
  default void f() {} // 隐式 public
}
```

我们可以定义类

```java
class C implements A, B {
```

如果尝试继承两个默认方法将会报错；如果类 `C` 证明它自己重写了 `f()` 实现，一切都是正常的。现在关于字段 `X` 的不同定义呢？对于类 `C` 这没有问题，你可以引用 `A.X` 和 `B.X`，但如果你没有用原始接口名称来限定 `X`，将得到编译时错误。

Java 根本不允许任何多重继承。

只有一个抽象方法的接口被称为函数式接口。Java 为实现函数式接口的类实例提供了很好的语法糖：你可以直接定义接口，而无需指定实现类！

```java
@FunctionalInterface
interface Function {
  double apply(double x);
}
```

```java
public class TwiceApp {
    private static double twice(Function f, double x) {
        return f.apply(f.apply(x));
    }
    public static void main(String[] args) {
        assert twice(x->x*2, 10) == 14;
        assert twice(Math::floor, -11.77) == -12;
    }
}
```

我们用 `@FunctionalInterface` 注解标记了我们的 `Function`；虽然它是可选的，但是一种良好的get。接口中的抽象方法定义了一个具有单个参数和 `double` 返回值的函数。表达式 `x->x*2` 符合此类型规范，并作为我们 `twice` 方法的可接受第一个参数。`Math::floor` 也是如此，它是一个函数对象，其求值结果返回类中静态 `floor` 方法的值。

## 7.4 静态类型

Java 与之前章节中的语言不同之处在于，它在执行前通过静态方式捕捉几乎所有的类型错误。将一个 `Animal` 乘以一个布尔值？Java 永远不会让你的程序运行。相比之下，Python 在运行时抛出 `TypeError`，而 JavaScript 则会转换操作数的数字。Java 的编译时类型检查甚至涵盖涉及变量的表达式；例如，在声明 `int x = 3;` 的作用范围内，我们可以推断出表达式 `x + 5` 的类型为 `double`。在第 125 页的示例中，声明 `Animal s = new Horse("CI")` 意味着表达式 `s.speak()` 的类型为 `String`，而表达式 `s` 本身的类型为 `Animal`。Java 要求对变量本身进行类型约束，限制它们仅包含兼容类型的值。

我们使用**静态类型**（static typing）一术语来指代执行前的类型检查，并使用**动态类型**（dynamic typing）一术语来指代运行时的类型检查。诚然，文献中存在更正式的定义，并且可以在关于类型和编程语言的文献中找到，Pierce [9] 是其中的经典参考。“静态”完美契合了 Pierce 对类型系统的定义，即类型系统是一种通过对所使用的值的种类进行分类来自动检查是否存在错误行为的语法方法。它告诉我们可以说什么或不能说什么。例如在 Java 中，将变量与类型 `Animal` 关联限制了我们使用 `Animal` 操作，即使它持有的是 `Cow` 类的对象。Harper 甚至认为“动态类型是静态类型的一种特例”。为什么？对比这些等效的 Java 和 Ruby 代码：

```java
// Java
Object x;
if (Math.random() < 0.5) {
    x = "string";
} else {
    x = 5;
}
System.out.println(x.getClass());
```

```ruby
# Ruby
x
if rand < 0.5
  x = "string"
else
  x = 5
end
puts x.class
```

Harper 正确地指出了类型与类的区别（见图 7.1）。这在 Java 侧显而易见，变量被限制为 `Object` 类型，可以轻松持有 `String` 或 `Integer` 的值。在 Ruby 侧，发生了相同的情况，但没有显式地为 `x` 绑定类型。这就像只有一种静态类型，事实上，包括 Harper 在内的一些作者将“动态类型语言”称为无类型语言。注意，静态类型和动态类型指的是机制，而非语言本身。Java 的大部分类型检查在编译时完成，但也会出现类型检查发生在运行时的情况。例如，数组是协变的，将一个羊数组赋值给动物数组变量是完全没问题的。但一个任意的动物数组包含牛，因此编译器不会阻止你将一头牛添加到类型为 `Animal[]` 的对象上。

```java
public class CovariantArray {
    public static void main(String[] args) {
        Animal[] animals = new Sheep[10]; // 协变
        try {
            animals[0] = new Cow("Bessie");
        } catch (ArrayStoreException e) {
            System.out.println("Runtime type checking!");
        }
    }
}
```

虽然数组是协变的，但其他集合（列表、集合等）则不是。在静态类型语言中，使用参数化类型来实现这些集合是有意义的。Java 将这些称为**泛型**（generic types），而这些是我们接下来的巡检重点。

### 泛型

Java 倾向于使用静态类型，被称为泛型的参数化类型经常出现。列表和集合提供了一个典型的说明：

```java
import java.util.Arrays;
import java.util.List;
import java.util.Set;
import java.util.HashSet;
public class ListAndSetExample {
    public static void main(String[] args) {
        List<String> words = Arrays.asList("do", "while", "if", "a");
        Set<Integer> sizes = new HashSet<>();
        for (String word : words) {
            sizes.add(word.length());
        }
        assert sizes.equals(new HashSet<Integer>(Arrays.asList(5,2,1)));
    }
}
```

我们创建了两个变量，类型别为字符串列表和整数集合。`List<E>` 和 `Set<E>` 都是 `java.util` 包中的接口。`E` 是（正如我们在 Java 中看到的）一个类型参数。我们用一个 `HashSet<Integer>` 类的对象初始化了 `sizes`（注意类型参数 `Integer` 是推断出来的）。变量 `words` 被初始化为实现列表接口类的对象；我们并不确切知道、也不关心它是哪一个类——我们通过类型定义的方法来访问该对象。

Java 集合是不变变的（invariant），因此牛列表不能赋值给动物列表。为了创建一个操作动物列表的方法，同时接受羊列表或马列表作为参数，我们使用**通配符**（`?`）。

```java
import java.util.List;
import java.util.Arrays;
public class ChorusApp {
    public static void chorus(List<? extends Animal> animals) {
        for (Animal animal : animals) {
            System.out.println(animal.speak());
        }
    }
    public static void main(String[] args) {
        List<Cow> cows = Arrays.asList("Bessie");
        List<Sheep> sheep = Arrays.asList("Woolly");
        chorus(cows);
        chorus(sheep);
    }
}
```

`? extends Animal` 信号着上界通配符，意味着类型参数可以是 `Animal` 或其任何子类。`HashSet<E>` 是标准库中的八种实现之一，包括 `TreeSet<E>` 和 `ConcurrentSkipListSet<E>`。

### 语言探索

让我们简单看一眼下界通配符，一个简单的例子。我们可以向羊集合、动物集合甚至是对象集合添加羊：

```java
import java.util.Set;
import java.util.HashSet;
public class SheepAdder {
    public static void add(Set<? super Sheep> set, Sheep sheep) {
        set.add(sheep);
    }
    public static void main(String[] args) {
        Set<? super Object> s1 = new HashSet<>();
        Set<? super Animal> s2 = new HashSet<>();
        Set<? super Sheep> s3 = new HashSet<>();
        Sheep sheep = new Sheep("Rafe");
        add(s1, sheep);
        add(s2, sheep);
        add(s3, sheep);
    }
}
```

通配符不能用于实例化对象；但边界类型参数是为此目的。我们用一个示例来说明它们的用法：

```java
public class MinMax<C extends Comparable> {
    private C min;
    private C max;
    public MinMax(C x, C y) {
        min = x.compareTo(y) < 0 ? x : y;
        max = x.compareTo(y) > 0 ? x : y;
    }
    public C getMin() { return min; }
    public C getMax() { return max; }
}
```
