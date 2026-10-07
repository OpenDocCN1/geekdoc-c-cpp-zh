
在调用和获取结果之间，调用进程可以自由执行其他工作。当不需要等待中间工作时，调用者可以使用 `remotall_fetch`（代替 `remotall` 和 `fetch`）或 `@fetch`（代替 `@spawn` 和 `fetch`）来结合调用和获取。

跨核并行编程的一个常见示例是通过在正方形 `(0,0)...(1,1)` 中生成随机点来计算 $\pi$ 的近似值。计算内切弧内（图 6.3 中 `x^2+y^2 < 1` 的点 `(x,y)`）的随机点数量，除以正方形内的点总数，即可近似值 $\frac{\pi}{4}$。让我们在三个核心上并行生成百万个随机点：

![](img/2cd8452ff5a372a7459559ad)

# 练习

现在轮到你了。请通过下方的活动和研究问题继续探索 Julia，并随时根据自己的想法进行扩展。

- 6.1 找到首页。下载最新的发行版本并尝试 `REPL`。
- 6.2 查阅 `http://julia-demo.readthedocs.org/en/latest/stdl/base.html` 上的标准库文档。
- 6.3 研究并通过有趣的例子解释 `==`、`===` 和 `is` 之间的区别。`==` 运算符是浅层测试还是深层的质量测试？
- 6.4 Julia 使用什么运算符进行字符串拼接？
- 6.5 比较并对比 Python 和 Julia 在位置参数、可选参数和关键字参数及其对应参数方面的处理方法。针对每种语言提出此类问题，例如：位置参数和关键字可以是可选的吗？位置和关键字参数以及参数可以以任何顺序出现吗？
- 6.6 定义一个函数 `fib` 来计算第 `n` 个斐波契数，使用尾递归和可选参数。调用 `fib(7)` 应该返回 `13`，通过以下调用：`fib(7) ⇒ fib(6,0,1) ⇒ fib(5,1,1) ⇒ fib(4,1,2) ⇒ fib(3,2,3) ⇒ fib(2,3,5) ⇒ fib(1,5,8) ⇒ fib(0,8,13) ⇒ 13`。
- 6.7 如果你在在线文档和公共仓库中浏览 Julia 源码，你可能会发现 `local` 关键字相当少见。为什么要这样做？在什么情况下你会认为 `local` 关键字是必要的？
- 6.8 Julia 表达式 `[1 2]` 和 `[1 2 3]` 具有相同的类型吗？如果是，类型是什么？
- 6.9 给定两个表达式 `[1 3]` 和 `[1;3]`，它们的类型分别是什么？(b) 画出这些表达式所代表的数组（或矩阵）。
- 6.10 表达式 `isa(e,Irrational) && isa(π,Irrational)` 求结果为 `true`，而 `type(e)==typeof(π)` 结果为 `false`。为什么？
- 6.11 为什么 Julia 类型 `Type{T}` 是一个参数化类型？`Type{Int64}` 到底是什么类型？在何时或何处类型 `Type{Type}` 是用？
- 6.12 `Any` 被称为“顶类型”（top type）。查出这意味着什么。Julia 有“底类型”（bottom type）吗？如果有，它是什么？
- 6.13 计算以下每个表达式的值并解释每个结果：
    - a. `isa([0, 1], Array)`
    - b. `isa([0, 1], Array{Integer})`
    - c. `isa([0, 1], Array{Int64})`
    - d. `isa([0, 1], Array{int64,1})`
    - e. `isa([0, 1], Array{int64,2})`
- 6.14 表达式 `[i+j/k for i=1:4, j=1:3, k=5]` 的类型是什么？Julia 如何推断出这个类型？
- 6.15 在你使用的 Julia 版本中，对于以下泛型函数 `+`、`convert`、`length` 和 `and`，存在多少不同的方法。

## 编程语言探索

6.16 Julia 在任何地方使用了逆变（contravariance）吗？如果有，在哪里？如果没有，找到另一种使用了该特语言并给出示例。
6.17 研究多重分发（multiple dispatch）优于单重分发（single dispatch）的优缺点。为什么 Julia 采用多重分发？
6.18 类型注解是在程序运行前检查还是运行期间检查？写一个程序证明你的答案。
6.19 我们在本章涵盖了三种表示 `Expr` 对象的技巧。还有第四种方法，即 `quote...` 构造器。它与其他三个有何不同？因为它更复杂，什么时候该用它？由于它更复杂，什么时候使用它更有优势？
6.20 如果你在在线文档和公共仓库中浏览 Julia 源码，你可能会发现 `local` 关键字相当少见。为什么要这样做？在什么情况下你会认为 `local` 关键字是必要的？
6.21 Julia 表达式 `[1 2]` 和 `[1 2 3]` 具有相同的类型吗？如果是，类型是什么？
6.22 给定两个表达式 `[1 3]` 和 `[1;3]`，它们的类型分别是什么？(b) 画出这些表达式所代表的数组（或矩阵）。
6.23 表达式 `isa(e,Irrational) && isa(π,Irrational)` 求结果为 `true`，而 `type(e)==typeof(π)` 结果为 `false`。为什么？
6.24 为什么 Julia 类型 `Type{T}` 是一个参数化类型？`Type{Int64}` 到底是什么类型？在何时或何处类型 `Type{Type}` 是用？
6.25 `Any` 被称为“顶类型”（top type）。查出这意味着什么。Julia 有“底类型”（bottom type）吗？如果有，它是什么？
6.26 计算以下每个表达式的值并解释每个结果：
    - a. `isa([0, 1], Array)`
    - b. `isa([0, 1], Array{Integer})`
    - c. `isa([0, 1], Array{Int64})`
    - d. `isa([0, 1], Array{int64,1})`
    - e. `isa([0, 1], Array{int64,2})`
- 6.27 表达式 `[i+j/k for i=1:4, j=1:3, k=5]` 的类型是什么？Julia 如何推断出这个类型？
- 6.28 在你使用的 Julia 版本中，对于以下泛型函数 `+`、`convert`、`length` 和 `and`，存在多少不同的方法。
6.29 Julia 在任何地方使用了逆变（contravariance）吗？如果有，在哪里？如果没有，找到另一种使用了该特性的语言并给出示例。
6.30 研究多重分发（multiple dispatch）优于单重分发（single dispatch）的优缺点。为什么 Julia 采用多重分发？
6.31 类型注解是在程序运行前检查还是运行期间检查？写一个程序证明你的答案。
6.32 我们在本章涵盖了三种表示 `Expr` 对象的技巧。还有第四种方法，即 `quote...` 构造器。它与其他三个有何不同？因为它更复杂，什么时候该用它？

# Java

| 特性 | 细节 |
| :--- | :--- |
| 设计者 | James Gosling |
| 首次出现 | 1995 |
| 平台 | 机器无关、高性能 |
| 哲学 | 一次编写，随运行 |
| 版本 | 1.1 (1997), 5 (2004), 8 (2014) |
| 特性 | 多线程、安全、企业级 |

Java 是一种极其流行的语言，其力量不仅源于语言本身，还源于其庞大的生态系统。由于其可用性、机器无关的平台和性能，许多额外的语言目标目标虚拟机（JVM）。

Sun Microsystems 的团队在万维网早期创建了 Java。Java 并没有内置语言并发。Java 在服务器端作为 applet 获得了巨大的人气。虽然它的名字可能让你误以为，但虚拟机并不知道其二进制格式。编译后的 Java 代码可以在任何系统上运行。

## 7.1 HELLO JAVA

让我们通过熟悉的三角形程序开始对 Java 的探索：

```java
public class TripleApp {
    public static void main(String[] args) {
        for (int c = 1; c <= 40; c++) {
            for (int b = 1; b < c; b++) {
                for (int a = 1; a < b; a++) {
                    if (a * a + b * b == c) {
                        System.out.printf("%d, %d, %d\n", a, b, c);
                    }
                }
            }
        }
    }
}
```

```java
private static void generatePermutations(char[] a, int n) {
  if (n == 0) {
    System.out.println(String.valueOf(a));
  } else {
    for (int i = 0; i < n; i++) {
      generatePermutations(a, n-1);
      swap(a, n % 2 == 0 ? i, n);
    }
    generatePermutations(a, n-1);
  }
}
private static void swap(char[] a, int i, int j) {
  char saved = a[i];
  a[i] = a[j];
  a[j] = saved;
}
```

现在我们开始看到 Java 冗长的首要原因了：几乎所有内容都被标记了——变量类型、方法参数类型、返回类型，以及类和类成员的访问级别。这些标记带来了一些好处。它们为代码阅读者提供了额外的文档说明，并使工具（如开发环境中的工具）能够很好地静态分析，帮助程序员在运行之前检测某些类型的错误。

脚本本身突出了感兴趣的行，也许是因为 (1) 数组参数不包含程序名，以及 (2) 字符串是不可变的，因此需要一个可变的数组来进行交换。

接下来，是字计数应用程序。

```java
import java.util.Scanner;
import java.util.SortedMap;
import java.util.TreeMap;
import java.util.regex.Pattern;
import java.util.regex.Matcher;
public class TraditionalWordCountApp {
  public static void main(String[] args) {
    SortedMap<String, Integer> counts = new TreeMap<>();
    Pattern wordPattern = Pattern.compile("[a-z]+");
    Scanner scanner = new Scanner(System.in);
    while (scanner.hasNext()) {
      String line = scanner.nextLine().toLowerCase();
      Matcher matcher = wordPattern.matcher(line);
      while (matcher.find()) {
        String word = matcher.group();
        counts.put(word, counts.getOrDefault(word, 0) + 1);
      }
    }
  }
}
```

```java
for (SortedMap.Entry<String, Integer> e : counts.entrySet()) {
    System.out.printf("%s %d\n", e.getKey(), e.getValue());
}
```

此脚本使用了 Java 标准库中的几个类（例如 `package.util.regex` 和来自 `java.util` 包的 `TreeMap`）。与 Python 不同，Java 不需要 `import` 语句；导入一个类可以让我们避免在整个代码中使用这些类的完全限定名。`String` 类来自一个特殊的包 `java.lang`，其类默认是被导入的。

Java 的标准库需要大量的代码来遍历文件的行（如果我们必须将标准输入包装在 `scanner` 中且可以使用 `while` 循环的话）、匹配正则表达式（我们无法直接获得匹配项数组）。Java 程序员经常使用第三方库，例如 Google Guava 或 Apache Commons 来简化代码。我们的脚本要么是可读的并将每行转为小写，使用 `matcher` 进行处理，遍历匹配项并填充排序映射，然后遍历映射打印其内容。

许多程序员倾向于使用流（streams）编写此脚本：

```java
import java.util.TreeMap;
import java.util.regex.Pattern;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.function.Function;
import java.util.stream.Collectors;
public class WordCountApp {
    public static void main(String[] args) {
        Pattern nonWord = Pattern.compile("[^a-z']+");
        new BufferedReader(new InputStreamReader(System.in))
            .lines()
            .flatMap(line -> 
                nonWord.split(line.toLowerCase()))
            .filter(word -> !word.isEmpty())
            .collect(Collectors.groupingBy(Function.identity(),
                TreeMap::new, Collectors.counting()))
            .forEach((word, count) ->
                System.out.printf("%s %d\n", word, count));
    }
}
```

# Java 125

| 类修饰符 (Class Modifier) | 说明 |
| --- | --- |
| 无修饰符 | 仅在当前包内可见 |
| public | 在其包所在的任何地方均可见 |
| abstract | 不可实例化（可能包含抽象方法） |
| final | 不可被继承（子化） |
| static | 指定一个嵌套顶层类（参见章节末练习） |

| 成员或构造函数修饰符 (Member or Constructor Modifier) | 说明 |
| --- | --- |
| 无修饰符 | 仅在当前包内可见 |
| private | 仅在当前类内可见 |
| protected | 仅在包内和子类中可见 |
| public | 在其类所在的任何地方均可见 |
| 字段修饰符 (Field Modifier) | 说明 |
| --- | --- |
| final | 赋值后值可能不可更改 |
| static | 类的所有对象共享该字段的唯一实例 |
| transient | 不被序列化 |
| volatile | 值可能会异步变化，因此编译器必须避免某些优化 |
| 方法修饰符 (Method Modifier) | 说明 |
| --- | --- |
| final | 不可重写 |
| static | 方法不适用于特定的实例 |
| abstract | 无方法体；由子类实现 |
| synchronized | 执行前锁定对象 |
| native | 实现未用 Java 编写，而是用某种依赖于平台的方式 |

表 7.1 Java 修饰符

```java
public class CircleApp {
    public static void main(String[] args) {
        Circle c1 = new Circle(3, 5, 1);
        Circle c2 = Circle.create(2, 8, 10);
        assert c1.area() == Math.PI && c2.area() == 100*Math.PI;
        assert c2.area() == 4*Math.PI;
    }
}
```

注意静态方法的调用方式，就像它们定义在类 `Class` 中（Circle 是该类的实例）一样，但技术上讲，并非如此。静态方法和实例方法都属于 `Circle`，尽管只有实例方法拥有接收者（receiver）。
像 Julia 一样，Java 既有抽象类也有具体类。Java 允许抽象类和具体类拥有子类（与 Julia 不同，只有抽象类型拥有子类型）。我们反复使用的动物示例说明了 Java 中的继承：

```java
abstract class Animal {
    private String name;
    public Animal(String name) {
        this.name = name;
    }
}
```
