
- 7. 它不是。但是，调用了一个递归方法——节点类的大小。

- 8. A=10, L=0000, O=001, H=0001，因此 ALOHA = 1000000010010

- 9. 在根节点。

- 10. 

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_849_1.png)

- 11. 图 4：6 个叶子节点，5 个内部节点。
  图 5：13 个叶子节点，12 个内部节点。
  图 6：3 个叶子节点，2 个内部节点。
  你可能从这些数据中推出叶子节点的数量始终等于内部节点数 + 1。如果所有内部节点都有两个孩子，那么就是正确的，否则不是——考虑这棵树的根只有一个孩子。

```java
public class Tree {
  public int height() {
    if (root == null) return 0;
    else return root.height();
  }
  class Node {
    public int height() {
      int leftHeight = 0;
      if (left != null) {
        leftHeight = left.height();
      }
      int rightHeight = 0;
      if (right != null) {
        rightHeight = right.height();
      }
      return 1 + Math.max(leftHeight, rightHeight);
    }
  }
}
```
该解决方案调用了递归检查；在第 17.2.3 节只需要一个。

- 13. 在树中，每个节点可以有任意数量的孩子。在二叉树中，节点最多有两个孩子。在平衡树中，所有节点左右和右的后代数量大致相等。

- 14. 因为二叉搜索条件适用于树的所有节点，所以它也适用于所有子树的所有节点。（更正：它适用于子树的所有节点。）

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_849_2.png)

## 自测题答案

- 16. 例如，Sarah。Romeo 和 Tom 之间的任何字符串都可以。

- 17. “Tom”有一个孩子。该孩子在父节点“Julia”中替换了“Tom”。

- 18. 在包含 -1 的节点上调用 `inorder`。然后在 0 上调用 `visit`，返回 false。因此，在包含 1 的节点上没有调用 `inorder`，而包含 0 的节点上的 `inorder` 调用结束，返回到根节点的 `inorder`。现在在 2 上调用 `visit`，返回 true，尽管它不该如此。见练习 P7.18。

- 23. AIGIHBEC

- 24. 皇室家族树：George V、George VI、Mary、Henry、John、Elizabeth II。（注：此处原文似乎存在乱码或OCR错误）

- 19. “Julia”有两个孩子。我们在右子树中寻找最小的孩子，“Romeo”。数据替换了“Julia”，节点从其父节点“Tom”中移除。

- 20. 对于两棵树，中序遍历均为 3 + 4 * 5。

- 21. 否——例如，考虑 + 的孩子。即使查找 3、4 和 + 的 Unicode 值，显然 + 并不在 3 和 4 之间。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_850_2.png)

- 22. 因为我们需要调用 `v.counter` 来获取结果。

- . 当方法返回给调用者时，调用者可以继续遍历树。例如，假设树是

- 27. 顶部的红色节点可以是黑色父节点的左孩子或右孩子，底部的红色节点可以是其（红色）父节点的左孩子或右孩子，产生四种配置。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_850_3.png)

- 28. 否，看第一棵树。在开始时，必须插入了 n2。因为这棵树是一个有效的红黑树插入，它不可能是红色根节点。现在考虑双红色删除后的步骤。图 22 中 n2 的父节点可能是红色的，但那样 n2 就没有红色兄弟——这将不再是红黑树。假设我们一旦遇到 0 就停止访问，因此在接收到 0 时返回 false。我们首先在包含 2 的节点上调用 `inorder`。它调用了包含 0 的节点上的 `inorder`，这

- 29. 考虑这种场景，X 是要删除的黑色叶子节点。

- 34. 
![](img/6a52d1dde3a219cfa39d548e31d0e6ce_851_0.png)

- 35. 上浮（Bubble up）：
![](img/6a52d1dde3a219cfa39d548e31d0e6ce_851_1.png)

- 36. 修复负红色：
![](img/6a52d1dde3a219cfa39d548e31d0e6ce_851_2.png)

- 37. 堆排序需要的存储较少，因为它不需要辅助数组。最小堆为了让公式更直观而浪费了空间。在排序数组时，我们不想浪费空间，所以我们调整公式。

- 38. 以树的形式表示，即
![](img/6a52d1dde3a219cfa39d548e31d0e6ce_851_4.png)

- 30. 它消失了。假设图 21 中红色孙子的兄弟也是红色的。这意味着其中一个 $t_i$ 有一个红色根节点。然而，它们都变成了图 22 中黑色节点 $n_1$ 和 $n_2$ 的孩子。记住，这是一个最大堆！

- 39. 节点与 3 交换，堆进行上修复，产生

- 31. 优先级队列是合适的，因为我们想要获取最大的元素，即使它们已经被插入。

- 40. 遗憾的是，最大的元素首先被移除，它必须移动到根节点，需要 $O(\log n)$ 步。次大的元素仍在数组末尾，再次需要 $O(\log n)$ 步，以此此类推。

- 32. 大于 100 的下一个 2 的幂是 128，完全填充的树有 127 个节点。

- 33. 通常不是。例如，图 30 中前序为 20 75 84 90 96 91 93 43 57 71 的堆。

## 第 18 章 ## 泛型类

## 本章目标

- 理解泛型编程的目标
- 实现泛型类和方法
- 解释泛型方法在虚拟机中的执行
- 描述 Java 泛型编程的局限性

### 目录

- 18.1 泛型类和类型参数 818
- 18.2 实现泛型类型 819
  语法 18.1：声明泛型类 820
- 18.3 泛型方法 823
  语法 18.2：声明泛型方法 824
- 18.4 类型参数 825
  常见错误 18.1：泛型与继承 827
- 常见错误 18.2：数组存储异常 827
  特殊主题 18.1：通配符类型 828
- 18.5 类型擦除 829
  常见错误 18.3：在静态上下文中使用泛型类型 832
  特殊主题 18.2：反射 832
  实例示例 18.1：制作泛型二叉搜索树类

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_852_0.png)

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_853_0.png)

在超市里，通用产品可以从多个供应商处获得。在计算机科学中，泛型编程涉及适用于多种类型的数据结构和算法的设计与实现。你已经见过泛型 `ArrayList` 类可以用于收集数组类型的元素。在本章中，你将学习如何实现自己的泛型类。

# 18.2 实现泛型 819

`ArrayList` 类的方法更安全。你无法向 `ArrayList<BankAccount>` 中添加 `String` 对象，但你可能会意外地向一个用于存储银行账户的 `LinkedList` 中添加 `String`。

```
BankAccount accounts1 = new ArrayList<BankAccount>();
LinkedList accounts2 = new LinkedList<>(); //应该持有 BankAccount 对象
accounts1.add("my savings"); // 编译错误
accounts2.add("my savings"); // 编译时不检到
```

当代码的某部分获取该字符串并认为它是银行账户时，后者会导致类型转换异常（cast exception）：

```
BankAccount account = (BankAccount)accounts.get(0); // 运行时错误
```

使用泛型 `ArrayList` 类的代码也更容易易读。当你放入 `ArrayList<BankAccount>` 时，你立刻知道它必须包含银行账户。当你看到 `LinkedList` 时，你必须研究代码才能找出它包含什么。

在第 16 章和第 17 章中，我们使用继承来实现泛型链表、哈希表和二叉树；你已经熟悉了继承的概念。使用类型参数需要新的语法和高级技术——这些是本章的主题。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_854_0.png)

- 1. 标准库提供了一个类型为 K、值类型为 V 的 `HashMap<K,V>`。声明一个映射字符串到整数的哈希映射。
- 2. 第 17 章中的二叉树类是泛型编程的一个示例，因为你可以配合任何实现该接口的类使用它。它是通过继承还是类型参数实现泛型的？
- 3. 以下代码是否包含错误？如果是，是编译错误还是运行时错误？

```
ArrayList<Integer> a = new ArrayList<Integer>();
String s = a.get(0);
```

- 4. 下列代码是否包含错误？如果是，是编译错误还是运行时错误？

```
ArrayList<Double> a = new ArrayList<Double>();
a.add("3.14");
```

- 5. 下列代码是否包含错误？如果是，是编译错误还是运行时错误？

```
LinkedList a = new LinkedList();
a.add("3.14");
double x = (Double)a.removeFirst();
```

现在练习：你可以尝试章节末尾的练习：R18.4, R18.5, R18.6。

# 18.2 实现泛型

在本节中，你将学习如何实现自己的泛型类。我们将编写一个简单的泛型类来存储对象对，每个对象都可以是任意类型。例如：

```
Pair<String, Integer> result = new Pair<String, Integer>("Harry Morgan", 1729);
```

## 语法 18.1 声明泛型类

```
语法 修饰符 类泛型ClassName<类型变量1, 类型变量2, ..>
{
    实例变量
    构造函数
    方法
}
```

为每个类型参数提供一个变量。

```java
public class Pair<T, S>
{
    private T first;
    private S second;
    public T getFirst() { return first; }
}
```

### 带有变量返回类型的方法

`getFirst` 和 `getSecond` 方法获取对的第一个和第二个值：
```
String name = result.getFirst();
Integer number = result.getSecond();
```
当你实现一个同时计算两个值的方法时，这个类会非常有用。一个方法不能同时返回 `String` 和 `Integer`，但它可以返回一个类型为 `Pair<String, Integer>` 的单一对象。

泛型 `Pair` 类两个参数，一个用于第一个元素的类型，另一个用于第二个元素的类型。
我们需要为类型参数选择变量。使用小写字母命名类型变量被认为是良好的习惯，如下表：

| 类型变量 | 含义 |
| :--- | :--- |
| E | 集合中的元素类型 |
| K | 映射中的键类型 |
| V | 映射中的值类型 |
| T | 通用类型 |
| S, U | 其他通用类型 |

泛型类的类型变量紧跟类名，并括在角括号中。

将泛型类的类型变量放在类名后，用括号（`<` 和 `>`）括起来。

```java
public class Pair<T, S>
```
当你声明 `Pair` 类的实例变量和方法时，使用变量 `T` 作为第一个元素类型，使用 `S` 作为第二个元素类型：
```java
public class Pair<T, S>
{
    private T first;
    private S second;
    public Pair(T firstElement, S secondElement) {
        first = firstElement;
        second = secondElement;
    }
    public T getFirst() { return first; }
    public S getSecond() { return second; }
}
```

有些人发现从一个普通类开始，选择一些实际类型而不是泛型占符更简单。例如：

```java
public class Pair // 这里我们开始处理一个对
    private String first;
    private Integer second;
```
很容易地将所有的 `String` 替换为类型 `T`，将所有的 `Integer` 替换为 `S`。这就完成了泛型类的声明。下面的示例程序展示了如何使用它。

### Pair.java

```java
/**
 * 此类收集不同类型的对。
 */
public class Pair<T, S> {
    private T first;
    private S second;
    /**
     * 构造一个元素对。
     * @param firstElement 第一个元素
     * @param secondElement 第二个元素
     */
    public Pair(T firstElement, S secondElement) {
        first = firstElement;
        second = secondElement;
    }
    /**
     * 获取第一个值。
     * @return 第一个元素
     */
    public T getFirst() {
        return first;
    }
    /**
     * 获取第二个值。
     * @return 第二个元素
     */
    public S getSecond() {
        return second;
    }
}
```

### Demo.java

```java
public class PairDemo {
    public static void main(String[] args) {
        String[] names = {"Tom", "Diana", "Harry"};
        Pair<String, Integer> result = firstContaining(names, "a");
        System.out.println(result.getFirst());
        System.out.println(result.getSecond());
    }
    /**
     * 获取包含给定字符串的字符串及其索引。
     * @param names 字符串数组
     * @param sub 字符串
     * @return 如果没有匹配则返回 pair(null, -1)
     */
    public static Pair<String, Integer> firstContaining(String[] names, String sub) {
        for (int i = 0; i < names.length; i++) {
            if (names[i].contains(sub)) {
                return new Pair<>(names[i], i);
            }
        }
        return new Pair<>(null, -1);
    }
}
```

输出：
```
Diana
1
```

# 18.2 实现泛型 821

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_854_0.png)

- 6. 如何使用泛型类构造 "Hello" 和 "World" 的字符串对？
- 7. 如何使用泛型类构造包含 "Hello" 和 1729 的对？
- 8. `ArrayList<Pair<String, Integer>>` 和 `Pair<ArrayList<String>, Integer>` 有什么区别？
- 9. 编写一个带有 `double` 参数 `x` 的 `roots` 方法，当 `x >= 0` 时返回其正负平方根，否则如何。
- 10. 如何实现一个收集三个任意类型值的 `Triple` 类？

现在练习：你可以尝试章节末尾的练习：P18.1, P18.2, P18.9。

# 18.3 泛型方法

泛型方法是带有类型参数的方法。这种方法可以出现在一个本身不是泛型的类中。你可以将其视为一组仅在一个或多个类型上有方法的模板。例如，我们可能想要声明一个可以打印任意类型数组的方法：

```java
public class ArrayUtil {
    /**
     * 打印数组中的所有元素。
     * @param a 要打印的数组
```
