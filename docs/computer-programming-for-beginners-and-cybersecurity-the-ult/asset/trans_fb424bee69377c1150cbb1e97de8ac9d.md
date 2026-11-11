
许多设计者会交替使用“类型参数”和“类型实参”这两个词，但它们的定义并不相同。编码时，要生成参数化类型，需要提供类型实参。因此，Foo<T> 中的 T 是类型参数，而 Foo<String> 中的 String 是类型实参。本书在使用这些词时遵循这一惯例。

与任何其他变量声明一样，这条语句并不会创建 Box 类型的新对象。它只是声明 integerBox 将持有一个对“Integer Box”的引用，也就是它读作 Box<Integer> 的方式。泛型类型调用通常被称为参数化类型。

要实例化这个类，照常使用 new 关键字，但要把 <Integer> 放在类名和圆括号之间：

```java
Box<Integer> integerBox = new Box<Integer>();
```

### 菱形运算符

在最新版本的 Java 中，只要编译器能够确定或从上下文推断出类型实参，就可以用一组空的类型实参（<>）替换调用泛型类构造函数所需的类型实参。这对尖括号 <> 被称为“菱形”（宽泛地说）。例如，你可以使用以下声明来创建 Box<Integer> 的实例：

```java
Box<Integer> integerBox = new Box<>();
```

### 泛型方法

泛型方法是引入自己的类型参数的方法。这类似于泛型类型声明，但类型参数的作用域仅限于声明它的方法。除了泛型类构造函数之外，还允许使用静态和非静态泛型方法。

泛型方法的语法包括一个位于尖括号内的类型参数列表，它出现在方法的返回类型之前。对于静态泛型方法，类型参数部分必须出现在方法的返回类型之前。例如，Util 类包含一个比较两个 Pair 对象的泛型方法。

```java
Pair<Integer, String> ex1 = new Pair<>(49, "string1");
```

```java
Pair<Integer, String> ex2 = new Pair<>(64, "string2");
```

```java
boolean comparison = Util.<Integer, String>compare(ex1, ex2);
```

### 有界类型参数

有时你想限制参数化类型中可用作类型实参的类型。例如，一个对数字进行操作的方法可能只接受 Number 或其子类的实例。有界类型参数正是为此而设。

要声明有界类型参数，请列出类型参数的名称，后跟 extends 关键字，再跟上界；在此示例中上界是 Number。请注意，在此上下文中，extends 用于表示“继承”（如类中的 extends）或“实现”（如接口中的 implements）。

### 多重边界

类型参数可以有多个边界。具有多个边界的类型变量是边界中列出的所有类型的子类型。如果其中一个边界是类，则必须首先指定它。例如：

```java
class X { /* ... */ }
```

```java
interface Y { /* ... */ }
```

```java
interface Z { /* ... */ }
```

```java
class R<T extends X & Y & Z> { /* ... */ }
```

如果边界 X 不是首先指定的，就会出现编译时错误：

```java
class R<T extends Y & X & Z> { /* ... */ } // compile-time error
```

## 第11章：集合

### 集合的函数式化

当我们把代码外部化时，我们暴露了每一步。这是命令式编程的标志。然而，函数式编程反复出现的主题之一，是采取完全相反的做法：将代码内部化。将代码内部化，就是把细节隐藏在函数内部。但函数式编程进一步推进了这一理念，把日常编程中的微观模式转变成函数。例如，遍历数据——无论是使用迭代器、for 循环还是 while 循环——就是这些微观模式之一。函数式编程改变了我们思考它们的方式。

Java 的函数式化努力，如果不改造其集合库（即 Collection、Map、List 和 Set 接口），就不会完整。这是因为迭代通常是在集合上进行的，而集合正是 Java 程序的构成基础。这里是函数式化努力发生的自然场所。但是，进行任何重大更改，例如向 Collection 接口添加新方法，都会破坏 Java 8 之前编写的所有程序的向后兼容性。这不仅包括 JDK 自身扩展 Collection 接口的层次结构，还包括任何开源或闭源的第三方库以及内部类。Java 的设计者从未也永远不会采用这种策略。然而，变化是必要的；该库于 1998 年引入，在软件行业的时间尺度上已经很久远，并且已显老态。

引入默认方法的动机，是由现代化和函数式化集合库的需要所引导的。默认方法正是合适的良方，因为它们允许在层次结构的根部添加行为，而不会干扰依赖类。子类可以继承或重写该行为。与添加新的接口方法不同，子类可以自动接受新的默认方法，而无需重新编译。即时兼容性得以实现。默认方法本身已被证明很有用，但它们的出现归因于函数式化集合库的需要。

函数式编程中第二个反复出现的主题是并行化。简单地说，函数式编程为并行处理提供了一种更好的捕鼠器。因此，集合库得到了增强，以便在处理集合时受益于多核 CPU。集合库与 Streams 一起，处于将函数式风格的并行处理引入 Java 的中心舞台。

既然我们已经学习了 Java 的标准函数式接口，就可以开始把这些知识应用到集合上。让我们看看 Java 8 中的集合库变成了什么样。

### Collection 接口

我们先来看 Collection 接口中一个全新的默认方法，它可供列表和集合使用。这就是 forEach() 方法：

```java
// Defined in the Iterable interface and extended in Collection
default void forEach(Consumer<? super T> action)
```

该方法遍历整个集合，让 Consumer 决定对每个元素做什么。这是内部迭代的概念，也是声明式编程的一种体现。如何迭代的细节并未指定。这与外部迭代相反；在外部迭代中，如何迭代以及如何处理每个元素都在代码中指定。

我们将用好莱坞电影黄金时代的闹剧喜剧三人组——著名的《三个臭皮匠》中的 Larry、Moe 和 Curly——来展示这些函数式化集合方法的示例。首先，让我们打印一个集合的内容：

```java
Collection<String> stooges = Arrays.asList("Larry", "Moe", "Curly");
// Print the contents of the stooges collection
stooges.forEach(System.out::println);
```

forEach() 方法具有非常广泛的适用性。它是遍历集合的一种方便得多的方式，应该成为你的事实标准。然而，作为一种声明式结构，有些事情你无法做到。最值得注意的是，你不能像在 while 循环中那样改变局部变量的状态。算法必须从函数式角度重新思考。目前，只需知道 forEach() 非常适合不改变状态的迭代。

现在我们来看 Collection 中可用的另一个新方法：

```java
default boolean removeIf(Predicate<? super E> filter)
```

removeIf() 方法将迭代、测试和删除的整个过程内部化。它只需要被告知删除条件是什么。

使用现在熟悉的 predicate 函数式接口，我们可以轻松确定要使用哪种 lambda。

```java
// Remove all people not part of the Three Stooges comedy trio
List<String> theThreeStooges = new ArrayList<>(
    Arrays.asList("Larry", "Moe", "Curly", "Tom", "Dick", "Harry"));

// Create the predicate that determines who is a stooge
Predicate<String> isAStooge =
    s -> "Larry".equals(s) || "Moe".equals(s) || "Curly".equals(s);

// Negate the condition to remove non-stooges
theThreeStooges.removeIf(isAStooge.negate());
```

要替换 List 的所有内容，我们可以使用 replaceAll()：

```java
List<String> theThreeStooges = new ArrayList<>(
    Arrays.asList("Larry", "Moe", "Curly"));

// Create the lambda to feminize the names
UnaryOperator<String> feminize =
    s -> "Larry".equals(s) ? "Lara" : "Moe".equals(s) ? "Maude" : "Shirley";

// Replace all male names with their female counterparts
theThreeStooges.replaceAll(feminize);
```

