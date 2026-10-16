

表 5.2 中的方法头现在可以通过包含传递给每个方法的策略/对象类型来完成。表 5.3 显示了这些更改。

**表 5.3** `map`、`filter` 和 `reduce` 的完成语法

| Method |
|---|
| `public static<E, R> Collection<R> map(MapStrategy<E, R> strategy, Collection<E> c)` |
| `public static<E> Collection<E> filter(FilterStrategy<E> strategy, Collection<E> c)` |
| `public static<E> E reduce(E baseElement, ReduceStrategy<E> strategy, Collection<E> c)` |

这三个策略接口的使用告诉迭代器的实现者，她可以期望一个识别适当策略方法（`transform`、`accept` 或 `combine`）的对象。同样，它们也告诉迭代器的使用者，他只需提供一个实现了这些接口之一的类的对象即可正确使用它们。我们现在介绍迭代器的实现，然后给出一个示例应用。

如前所述，三个迭代器方法的主体是一个名为 `Iterators` 的新类。最简单的方法是 reduce，它将一组对象组合成单个对象。代码如下：

```
public static<E> E reduce(E baseElement,
                         ReduceStrategy<E> strategy,
                         Collection <E> c){
    for (E element : c)
        baseElement = strategy.combine(baseElement, element);
    return baseElement;
}
```

正如你所见，实现者对用于组合结果的具体操作一无所知，除了其目标对象（此处命名为 `strategy`）实现了 ReduceStrategy 接口之外。在这方面，`strategy.combine` 的方法调用类似于高阶函数中形式函数参数的调用。

map 方法稍微复杂一些，因为它必须创建与输入集合相同类型的新的集合。幸运的是，Java 方法 getClass() 和 newInstance() 来拯救我们了。第一个方法返回一个对象的类，第二个方法使用类的默认构造函数返回该类的一个新实例。代码必须嵌入到 Java 的 try/catch 异常处理语法中，以进行这些方法所需<|message|> 的错误检查。map 的代码如下。filter 的实现留作练习。

```
public static<E, R> Collection<R> map(MapStrategy<E, R> strategy,
                                      Collection<E> c){
    try{
        Collection<R> results = c.getClass().newInstance();
        for (E element : c)
```
```
results.add(strategy.transform(element));
return results;
}catch(Exception e){
    System.out.println(e);
    return null;
}
}
```

如前所述，我们的新迭代器的使用者负责提供一个集合和相应的策略接口的一个实例。程序员可以定义一个实现 MapStrategy、FilterStrategy 或 ReduceStrategy 的新类，但没有必要费这个劲。Java 允许程序员在使用的点上创建一个匿名类的实例，其方式与函数式程序员创建 lambda 形式的方式非常相似。语法如下：

```
new <interface name>(){
    <method implementations>
}
```

表 5.4 显示了 MapStrategy 接口和一个示例实例化。该实例化通过取整数的平方根将整数值转换为 double 值。

**表 5.4  MapStrategy 接口和一个实例化**

| Interface | Instantiation |
|---|---|
| `public interface MapStrategy<E, R>{`<br>&nbsp;&nbsp;&nbsp;&nbsp;`public R transform(E element);`<br>`}` | `new MapStrategy<Integer, Double>(){`<br>&nbsp;&nbsp;&nbsp;&nbsp;`public Double transform(Integer i){`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`return Math.sqrt(i);`<br>&nbsp;&nbsp;&nbsp;&nbsp;`}`<br>`}` |

下一个代码段显示了一个完整的应用程序，对我们新的迭代器进行测试。注意使用了两种不同的特定映射策略，然后使用了一种过滤策略和一种归约策略。相同的代码可用于整数集或任何其他集合类（如第 5.3.2 节中研究的 LinkedStack）上的整数。

```
import iterators.*;
import java.util.*;

/*
Tests the map, filter, and reduce iterators with array lists.
Creates strategy objects as anonymous instances of the appropriate interfaces.
*/

public class TestIterators{

    static public void main(String[] args){
```

```
// The list contains [1 2 3 4 5 6 7 8]
List<Integer> list = new ArrayList<Integer>();
for (int i = 1; i <= 8; i++)
    list.add(i);

// Compute the square roots
Collection<Double> squareRoots =
    Iterators.map(new MapStrategy<Integer, Double>(){
        public Double transform(Integer i){
            return Math.sqrt(i);
        }
    }, list);
System.out.println(squareRoots);

// Convert to string representations
Collection<String> stringReps =
    Iterators.map(new MapStrategy<Integer, String>(){
        public String transform(Integer i){
            return i + "";
        }
    }, list);
System.out.println(stringReps);

// Keep the even numbers
Collection<Integer> evens =
    Iterators.filter(new FilterStrategy<Integer>(){
        public boolean accept(Integer i){
            return i % 2 == 0;
        }
    }, list);
System.out.println(evens);

// Sum the numbers
int sum = Iterators.reduce(0, new ReduceStrategy<Integer>(){
    public Integer combine(Integer first, Integer second){
        return first + second;
    }
}, list);
System.out.println(sum);
}
```

我们的 Java 版本的 map、filter 和 reduce 与函数式语言和 Smalltalk 中的对应版本相比如何？函数式版本很简单，因为它们是接受其他函数作为参数的函数。这里没有什么新东西需要学习。然而，map、filter 和 reduce 仅限于列表集合。Smalltalk 版本更通用，因为它们是关于任何集合的多态的。Smalltalk 块的语法实际上并不比 lambda 形式复杂。Java 版本的语法稍微复杂一些，但其中大部分复杂性可以被视为 lambda 形式或匿名代码块的本质等价物的样板。Java 版本相对于 Smalltalk 版本的真正好处在于静态类型检查。正如 always，类型错误（使用非集合对象或非策略对象）在编译时被及早捕获，并且所有错误总是被捕获。这使得在 Java 中使用 map、filter 和 reduce 几乎是万无一失的，尽管有点笨重。

## 5.4 C++

C++ 最初由 Bjarne Stroustrup 在 AT&T Bell Labs 开发，C++ 是对 C 的扩展，具有类似 Simula 的类，但在 1980 年代后期和 1990 年代，它远远超出了其起源，成为包含大量特性、部分面向对象、部分非面向对象的语言。它是一种折中语言，因为它包含大部分 C 语言作为子集，就像 Simula 包含 Algol60 作为子集一样。C++ 也被设计为一种高效、实用的语言，源于其用户的需求。因此，它成为 1990 年代初的主要面向对象语言，并且在非 Web 应用中仍然极受欢迎。自 1986 年发布第一本参考手册以来，添加了许多新特性，包括多重继承、模板、运算符重载和异常。自 1998 年采用国际标准（C++98）并于 2003 年修订（C++03）以来，该语言已稳定下来。正在进行新标准（C++0x）的工作，其出版预计在本书印刷时附近。

### 5.4.1 C++ 的基本元素：类、数据成员和成员函数

C++ 包含与 Java 类似的类和对象声明。实例变量和方法都称为类的成员：实例变量被称为数据成员，方法被称为成员函数。子类被称为派生类，超类被称为基类。C++ 与大多数其他面向对象语言，包括 Java 的一个基本区别是，对象不是自动的指针或引用。事实上，除了继承和成员函数的动态绑定之外，C++ 中的类数据类型与 C 的 struct（或 record）数据类型本质上是相同的。

与 Java 类似，C++ 为类成员提供了三个保护级别：public、private 和 protected。Public 成员可供客户端代码以及派生类访问。Protected 成员对客户端代码不可访问，但对派生类仍然可访问。Private 成员既不可供客户端访问，也不可供派生类访问。在类声明中，默认保护是 private，而在 struct 声明中，默认是 public。此外，关键字 private、public 和 protected 在类声明中建立块，而不是像 Java 中那样仅适用于单个成员声明：

