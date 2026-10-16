

# 练习

5.1 获取 Smalltalk 的一个实现并输入第 5.2 节中讨论的 Complex 类，然后添加方法来加减复数（你只需分别计算实部和虚部的和与差）。

5.2 Smalltalk 的 Integer 类包含一个使用循环计算两个整数最大公约数的 gcd: 方法。向 Integer 类添加一个名为 recursiveGcd: 的新方法。此方法应使用递归策略计算两个整数的最大公约数。请注意 Smalltalk 使用 \ 运算符表示整数余数。

5.3 向 Smalltalk 的 Collection 层次结构中添加一个 ArrayQueue 类。此类应具有第 5.2 节中开发的 LinkedQueue 类相同的功能。然而，新类应使用 OrderedCollection 对象来包含元素。

5.4 在 Smalltalk 中实现一个 LinkedPriorityQueue 类。添加到这种队列中的对象必须识别 <、= 和 > 运算符。对象在队列中按从小到大排序，从队首到队尾。如果两个对象相等，则按标准 FIFO 队列顺序插入。你的实现应最大程度地利用第 5.2 节中开发的 LinkedQueue 类。

5.5 举出至少两个示例问题，对比说明函数式编程语言和面向对象编程语言最适合解决的问题类型。

5.6 Java 的设计者将原始类型（标量）与引用类型（所有其他类型的值）区分开来。讨论这一决策对程序员的成本和收益。

5.7 在集合类的设计中，一些集合是其他集合的子类（“is-a”关系），而其他集合在其实现中包含或使用其他集合（“has-a”关系）。分别举出每种类型的设计示例并解释为什么该设计决策优于替代方案。

5.8 在 Smalltalk 中，Dictionary 类是 Set 类的子类，而在 Java 中，Map 类未作为子类包含在 Collection 类层次结构中。比较和对比这两种设计决策的成本和收益。

5.9 描述 Smalltalk 中实例方法和类方法之间的区别，并分别给出一个示例。

5.10 类变量对类的所有实例可见并由其共享。在应用程序中，这种变量将如何使用？

5.11 Java 中的构造函数是什么？构造函数如何重载以支持代码重用？

5.12 Java 中的静态方法类似于 Smalltalk 中的类方法（参见第 5.3.4 节的示例）。在第 5.3 节中开发的 Complex 类中定义一个静态方法 getInstance。此方法期望两个浮点数作为参数并返回包含这些值的新复数。然后，编写一段代码片段来展示如何使用此方法。

5.13 解释 Smalltalk 中 == 和 = 运算符之间的区别。它们如何说明引用语义？

5.14 描述抽象类和具体类之间的区别，并分别给出一个示例。

5.15 解释为什么 equals 和 toString 方法定义在 Java 的 Object 类中。

5.16 解释为什么程序员在定义新类时可能会包含 Java 的 equals 和 toString 方法。

5.17 完成第 5.3.4 节中讨论的 Iterators 类中的 Java filter 方法的实现，然后运行示例应用程序（在添加该节中开发的其他资源之后）。

5.18 描述面向对象语言中方法的动态绑定是如何工作的，并给出 Smalltalk、Java 或 C++ 中的具体示例。

5.19 在面向对象语言中何时可能进行方法的静态绑定？给出 Java 和 C++ 的具体示例。

5.20 比较和对比 Smalltalk、Java 和 C++ 中数据的封装和信息隐藏方式。

5.21 使用至少一个示例解释 Java 中类和接口之间的区别。

5.22 研究 Sun 的 Java 文档中的 Comparable 接口，并修改第 5.3 节中开发的 Complex 类以实现此接口。解释为什么此举将使程序员能够使用 Java 的 Arrays 或 Collections 类中的方法对 Complex 数字的数组或列表进行排序。

5.23 Java 和 C++ 支持带类型参数的泛型集合，而 Smalltalk 不支持。这种事实是否使 Smalltalk 程序员处于劣势？为什么或为什么不？

5.24 图 5.6 和 5.7 的类图显示了 Java 的 List 接口及其实现类。在第 5.3 节中，我们将 LinkedStack 类作为 AbstractCollection 的子类开发。一种替代实现称为 ArrayStack，包含与 LinkedStack 相同的方法。绘制一个类图，将这两个类和一个新的接口 TrueStack 放置在层次结构中的适当位置。（提示：TrueStack 接口应扩展 Collection 接口。栈类应扩展 AbstractCollection 类并实现 TrueStack 接口。）

5.25 修改 LinkedStack 类并实现 ArrayStack 类和上一练习中提到的 TrueStack 接口。

5.26 列出 Smalltalk 支持的迭代器类型并解释它们的工作原理。

5.27 Java 中的增强 for 循环依赖于迭代器。解释其工作原理。

5.28 Maps 和 filters 存在于函数式语言和 Smalltalk 中。解释这些软件构造在这两种上下文中的工作原理。

5.29 如果 x 是类 A 的对象，y 是类 B 的对象且 B 是 A 的子类，在赋值 x = y 之后，为什么当 m 是 B 的方法但不是 A 的方法时，x.m() 是非法的？

5.30 描述文本中讨论的 C++ 中关键字 virtual 的两种含义。

5.31 类型和类有什么区别？

5.32 有人声称深层的继承层次结构使系统维护更困难而不是更容易。解释为什么可能如此。

5.33 打印操作是动态绑定方法的良好候选。为什么？

5.34 给出以下 Java 代码：

```
class A{
    public void p(){
        System.out.println("A.p");
    }
    public void q(){
        System.out.println("A.q");
    }
    public void r(){
        p();
        q();
    }
}
class B extends A{
    public void p(){
        System.out.println("B.p");
    }
}
class C extends B{
    public void q(){
        System.out.println("C.q");
    }
    public void r(){
        q();
        p();
    }
}
...
A a = new B();
a.r();
a = new C();
a.r();
```

这段代码打印什么？为什么？

5.35 给出以下 C++ 代码：

```cpp
class A{

    public:

        virtual void p(){
            cout << "A.p" << endl;
        }

        void q(){
            cout << "A.q" << endl ;
        }

        virtual void r(){
            p();
            q();
        }
};

class B : public A{

    public:

        void p(){
            cout << "B.p" << endl;
        }
};

class C : public B{

    public:

        void q(){
            cout << "C.q" << endl;
        }

        void r(){
            q();
            p();
        }
};
```

(continued)

```
---
A a;
C c;
a = c;
a.r();
A* ap = new B;
ap->r();
ap = new C;
ap->r();
```

这段代码打印什么？为什么？

5.36 详细解释为什么 Java 中的多接口继承不会像 C++ 中的多类继承那样遭受相同的问题。

5.37 Meyer [1997] 将重载与参数多态区分如下（Ibid., p. 38）：“重载是为客户端程序员提供的设施：它使得在使用不同模块提供的不同数据结构实现时编写相同的客户端代码成为可能。泛型[参数化]是为模块实现者提供的：它允许他们编写相同的模块代码来描述同一数据结构的所有实例，应用于各种类型的对象。” 讨论这种对多态的观点。

## 注释和参考文献

面向对象编程技术的良好通用参考是 Meyer [1997]，它使用了有趣的面向对象语言 Eiffel，你尚未在本章中学习。Budd [1997] 和 Booch [1994] 以语言无关的方式描述了面向对象原则。Bruce [2002] 提供了对类型和类的原则性考察。Java 当然有很多参考资料，但其中强调面向对象原则的两本是 Arnold et. al [2000] 和 Horstmann [2006]。C++ 在 Stroustrup [1997] 和 Lippman 和 Lajoie [1998] 中有所描述。关于 Smalltalk 本身的书籍包括 Lalonde [1994]、Lewis [1995]、Sharp [1997] 以及 Lambert 和 Osborne [1997]。

以下参考资料描述了未在此研究的其他有趣的面向对象语言。Dylan 语言在 Feinberg 等人 [1996] 中描述。Eiffel 是一种精心设计的语言，具有类似 Pascal 的语法（Meyer [1997]）。Modula-3 是具有面向对象扩展的 Modula-2 派生语言（Cardelli 等人 [1989]、Nelson [1991] 和 Cardelli 等人 [1992]）。Objective C 是 Cox [1984, 1986] 设计的具有面向对象功能的 C 扩展。Tesler [1985] 描述了 Pascal 的面向对象扩展。LISP 的面向对象版本包括 CLOS（Gabriel、White 和 Bobrow [1991]；Bobrow 等人 [1988]）；Loops（Bobrow 和 Stefik [1983]）；和 Flavors（Moon [1986]）。

关于 C++ 模板的使用及其与面向对象技术的交互的信息可在 Alexandrescu [2001]、Koenig 和 Moo [1996]、Josuttis [1999] 和 Stroustrup [1997] 中找到。

许多研究论文以及关于面向对象编程技术的报告已出现在 OOPSLA [1986ff] 中。Sethi [1996] 给出了 C++ 中埃拉托斯特尼筛法的面向对象技术的有趣应用。

