
```cpp
old_cross_entropy = new_cross_entropy;

c++;

} while(diff_entropy > 0.01);

cout << "Number of iterations: " << c << "\n";

cout << "Final entropy: " << old_cross_entropy << "\n";

}
```

```cpp
int main(void)

{

    int t;

    HMM hmm(3, 2);

    string training = "HHTHHH";

    string test = "HTH";

    hmm.maximize(training, test);

    return 0;

}
```

一种用于语音识别的C++ 实现方案由 Becchetti 和 Ricotti [22] 描述。解决问题3的完整伪代码由 Mark Stamp [23] 提供。

# 第17章 离散隐尔马尔可夫模型

## 17.7 习题

(1) $\omega > 0$ 固定，且 $t \geq 0$。该 $4 \times 4$ 矩阵

$$P(t) = \frac{1}{4} \begin{pmatrix} 1+3e^{-\omega t} & 1-e^{-\omega t} & 1-e^{-\omega t} & 1-e^{-\omega t} \\ 1-e^{-\omega t} & 1+3e^{-\omega t} & 1-e^{-\omega t} & 1-e^{-\omega t} \\ 1-e^{-\omega t} & 1-e^{-\omega t} & 1+3e^{-\omega t} & 1-e^{-\omega t} \\ 1-e^{-\omega t} & 1-e^{-\omega t} & 1-e^{-\omega t} & 1+3e^{-\omega t} \end{pmatrix}$$

是一个随机矩阵（概率矩阵）吗？求它的特征值。设

$$\pi = \frac{1}{2}(1 \ 0 \ 0 \ 1).$$

求向量 $\pi P(t)$、$(\pi P(t))P(t)$ 等。是否存在 $P(t_1+t_2) = P(t_1)P(t_2)$？

(2) $\alpha \in [0,1]$。考虑随机矩阵

$$P(\alpha) = \begin{pmatrix} \alpha & 1-\alpha \\ 1-\alpha & \alpha \end{pmatrix}.$$

设 $n=1, 2, \dots$ 证明

$$P^n(\alpha) = \frac{1}{2} \begin{pmatrix} 1+(2\alpha-1)^n & 1-(2\alpha-1)^n \\ 1-(2\alpha-1)^n & 1+(2\alpha-1)^n \end{pmatrix}.$$

# 第 18 章

# 模糊集与模糊逻辑

## 18.1 引言

经典集合 $X$（也称为清晰集）被定义为元素或对象 $x \in X$ 的集合，这些元素可以是有限的、可计数的或不可计数的。每个元素元素属于或不属于集合 $A, A \subset X$。在第一的情况下，陈述 $x$ 属于 $A$ 为真，而在后一种，该陈述为假。经典集合可以通过不同的方式描述：可以列举（列出）属于集合的元素；可以通过分析方法描述它，例如陈述成员条件；或者通过使用特征函数定义元素，其中 1 表示成员，0 表示不成员。

**示例。** 集合

> $A := \{ x : x \text{ 是英文字母表中的字母}, x \text{ 是元音} \}$

给出如下：

> $A = \{ a, e, i, o, u \}$

该集合是有限的。

**示例。** 集合

> $$\mathbb{N}_0 := \{ 0, 1, 2, 3, \dots \}$$

是所有非负整数的集合。该集合是可计数的。整数集 $\mathbb{Z}$ 也是可计数的，因为它可以通过方式 1-1 映射到 $\mathbb{N}_0$

> $0 \mapsto 0, 1 \mapsto 1, -1 \mapsto 2, 2 \mapsto 3, -2 \mapsto 4, \dots$

集合 $\mathbb{N}_0 \times \mathbb{N}_0$ 和 $\mathbb{Z} \times \mathbb{Z}$ 也是可计数的。

**示例。** 所有实数用 $\mathbb{R}$ 表示。该集合是不可计数的。闭区间 $[0, 1]$ 内的实数集也是不可计数的。

## 第 18 章：模糊集与模糊逻辑

使用 STL 中 `set` 类的 C++ 和使用 `TreeSet` 类的 Java 均允许集合论操作。我们可以找到两个有限集的并集、交集和差集。我们还可以找到有限集的基数（即元素数量）。此外，我们可以确定一个有限集是否是另一个有限集的子集，以及一个有限集是否包含某个特定元素。

在 C++ 中，`set` 类是一个排序的关联容器，它存储类型为 `Key` 的对象。`set` 类是一个简单的关联容器，这意味着它的值类型和键类型都是 `key`。它还是一个唯一关联容器，意味着没有两个元素是相同的。`set` 类适用于集合算法：

```
includes
set_union
set_intersection
set_difference,
set_symmetric_difference
```

其原因有两点。首先，集合算法要求其参数为排序的范围，由于 `set` 类是排序的关联容器，它们的元素总是按升序排列的。其次，这些算法的输出范围总是排序的，而将一个排序范围插入到集合中具有一个重要属性：向集合中插入新元素不会使指向现有元素的迭代器失效。从集合中删除元素也不会使任何迭代器失效，当然，除了那些实际上指向被删除元素的迭代器除外。

以下 C++ 程序展示了该类的应用。

```cpp
// sets1.cpp
#include <iostream>
#include <set>
#include <algorithm>
#include <string>
#include <iterator>
using namespace std;
int main(void)
{
    const int M = 4; const int N = 3;
    const string a[M] = { "Jones", "Miller", "Steeb", "Smith" };
    const string b[N] = { "Hardy", "Copper", "Steeb" };
    set<string> s1(a,a+M);
    set<string> s2(b,b+N);
    set<string> s3;
    cout << "union of the sets s1 and s2: " << endl;
    set_union(s1.begin(),s1.end(),s2.begin(),s2.end(),
    ostream_iterator<string>(cout, " ")); cout << endl;
    cout << "Intersection of the sets s1 and s2: " << endl;
    set_intersection(s1.begin(),s1.end(),s2.begin(),s2.end(),
    ostream_iterator<string>(cout, " ")); cout << endl;
    cout << "difference of the sets s1 and s2: " << endl;
    set_difference(s1.begin(),s1.end(),s2.begin(),s2.end(),
    inserter(s3,s3.begin()));
    copy(s3.begin(),s3.end(),ostream_iterator<string>(cout," " ")); cout << endl;
    cout << "subset of s1? " << endl;
    bool ss = includes(s1.begin(),s1.end(),s2.begin(),s2.end());
    cout << ss << endl;
    cout << "subset of s2? " << endl;
    const string c1[] = { "Hardy" };
    set<string> s4(c1,c1+1);
    ss = includes(s2.begin(),s2.end(),s4.begin(),s4.end());
    cout << ss << endl;
    cout << "size of set s1: " << s1.size() << " elements " << endl;
    cout << "is s2 empty? " << endl;
    bool empty = s2.empty();
    cout << empty << endl;
    return 0;
}
```

在 Java 中，`Set` 接口是不包含重复元素的 `Collection`。`Set` 接口模拟了数学抽象。`Set` 接口扩展了 `Collection` 并包含了除自其继承以外的方法。JDK 提供了通用实现。`HashSet` 在哈希表中存储元素。`TreeSet` 在黑树中存储元素。这保证了迭代顺序。集合的并集通过 `addAll()` 方法提供，交集通过 `retainAll()` 方法提供。以下 Java 程序展示了 `TreeSet` 类的应用。

```java
import java.util.*;
public class SetOperation
{
    public static void main(String[] args)
    {
        String[] A = { "Steeb", "C++", "80.00" };
        TreeSet<String> S1 = new TreeSet<>();
        for(int i=0; i<A.length;i++) S1.add(A[i]);
        System.out.println("S1 = " + S1);
        String[] B = { "Solms", "Java", "80.00" };
        TreeSet<String> S2 = new TreeSet<>();
        for(int i=0; i<B.length;i++) S2.add(B[i]);
        System.out.println("S2 = " + S2);
        // union
        TreeSet<String> S3 = new TreeSet<>();
        boolean b1 = S3.addAll(S2);
        System.out.println("S3 = " + S3);
        System.out.println("S1 = " + S1);
        // intersection
        TreeSet<String> S4 = new TreeSet<>(S1);
        boolean b2 = S4.retainAll(S2);
        System.out.println("S4 = " + S4);
        System.out.println("S2 = " + S2);
        // asymmetric difference
        TreeSet<String> S5 = new TreeSet<>(S1);
        boolean b3 = S5.removeAll(S2);
        System.out.println("S5 = " + S5);
        // test for subset
        TreeSet<String> S6 = new TreeSet<>(S1);
        boolean b4 = S6.containsAll(S2);
        System.out.println("b4 = " + b4);
        // is element of set (contains)
        boolean b = S1.contains("80.00");
        System.out.println("b = " + b);
        b = S2.contains("Steeb");
        System.out.println("b = " + b);
    }
}
```

输出是：
```
S1 = [80.00, C++, Steeb]
S2 = [80.00, Java, Solms]
S3 = [80.00, C++, Java, Solms, Steeb]
S1 = [80.00, C++, Steeb]
S4 = [80.00]
S2 = [80.00, Java, Solms]
S5 = [C++, Steeb]
b4 = false
b = true
b = true
```

### 18. 引言

在模糊逻辑（Yager and Zadeh [276], Bojadiev [26], Bandemer [14], Ross [210], Zimmermann (286)）中，二值成员的概念被扩展以适应实数连续区间 $[0, 1]$ 上的各种成员程度，其中 0 和 1 的端点分别对应不成员和完全成员，正如指示函数对于清晰集所做的那样，但端点之间的无限多个值可以代表元素 $x$ 在宇宙 $X$ 上某个集合中的各种成员程度。在宇宙 $X$ 上能够容纳成员程度的集合被称为*模糊集*。对于模糊集，特征函数允许元素具有各种成员程度。*论域*（universe of discourse）被定义为所有可用信息的宇宙。一旦定义了宇宙，我们就可以在这个信息空间上定义某些事件。我们将集合描述为这些事件以及宇宙本身的数学抽象。

模糊逻辑和模糊集是强大的数学工具，用于建模工业、自然和人类中的不确定系统，作为在缺乏完整和精确信息的情况下进行决策常识推理的促进者。

让我们给出一个定义模糊集的示例。

**示例。** 如果我们谈论热和冷，可能会将高于 $25^{\circ}C$ 或低于该温度的所有温度归类为冷。这为我们提供了一个清晰二值集，任何温度都被归类为热或冷。或者，我们可能想通过以下映射指定热/冷的程度：

```
$0^{\circ}C \leq T \leq 0^{\circ}C \rightarrow$ 非常冷
$0^{\circ}C < T \leq 18^{\circ}C \rightarrow$ 中等冷
$18^{\circ}C < T \leq 25^{\circ}C \rightarrow$ 恰好
$25^{\circ}C < T \leq 30^{\circ}C \rightarrow$ 中等热
$T > 30^{\circ}C \rightarrow$ 非常热
```
