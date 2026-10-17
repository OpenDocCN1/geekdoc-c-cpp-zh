
- 开发工程师可以基于已测试并获批的规格进行工作。

图 17.21 结构设计技术

### 17.10 WRAPPING UP

我们讨论了面向对象分析与设计的各个方面。请记住，没有一种方法永远是绝对正确的。您必须将本文所呈现的思想视为仅供参考，并结合自身经验、创新和创造力进行应用。

下面是一些供您思考和创新的要点：

- 设定清晰的目标和具体的目标。
- 尝试使用现有系统作为示例或模型，以分析您的系统。
- 使用类来表示概念。
- 记住拟议系统必须灵活、便携且可扩展。
- 保持对系统所有组成部分的清晰文档记录。
- 尽可能重用现有的函数和类。
- 尽可能使用强类型函数。
- 尽可能使用原型。
- 使设计与编程风格保持一致。
- 使系统尽可能简洁、简单、小巧且高效。

## SUMMARY

- 经典的系统开发生命周期最广泛用于面向过程的开发，包含以下步骤：
  - 问题定义
  - 分析
  - 设计
  - 编码
  - 测试
  - 维护
- 在面向对象范式中，系统可以视为一组相互作用的实体，用于实现特定目标。
- 在面向对象分析（OOA）中，这些实体被称为对象。OOA 指的是以真实世界中的对象、它们的行为以及它们相互之间的交互来指定软件需求的方法。
- 面向对象设计（OOD）将软件需求转化为对象的规格，并从中推导出类层次结构，以便可以创建这些对象。
- 面向对象编程（OOP）是使用对象实现程序的过程，常用于 `C++` 等面向对象编程语言。

## 492 Object Oriented Programming with C++

面向对象分析（OOA）方法包括以下步骤：

- 定义问题
- 估算用户和软件的需求
- 识别对象及其属性
- 识别每个对象应提供的接口服务
- 在服务需求与服务提供之间建立对象之间的关联

面向对象设计（OOD）方法包括以下步骤：

- 回顾在分析阶段创建的对象
- 规范类之间的依赖
- 组织类层次结构
- 设计类
- 设计成员函数
- 设计驱动程序

理解系统设计及其影响的一种方式是构建并测试一个工作模型。该模型即为原型，相关过程为原型开发。

使用原型方法的好处包括：

- 您可以生成尽可能正确且完整的可理解规格
- 用户可以了解系统提供的内容
- 系统安装后所需的维护更改得以最小化
- 开发工程师可以基于已测试并获批的规格进行工作

## KEY TERMS

`abstract class` | `abstract nouns` | `a-kind-of` | `analysis` | `a-part-of` | `being verbs` | `bubble chart` | `class hierarchies` | `classes` | `classic life cycle` | `classification relationship` | `client-server relationship` | `coding` | `collaborations` | `common nouns` | `compare verbs` | `composition relationship` | `containment relationship` | `context diagrams` | `data dictionary` | `data flow diagrams` | `decision table` | `decision tree` | `design` | `development tools` | `doing verbs` | `driver program` | `entities` | `relationship diagram` | `entity-relationship` | `generation` | `forecasts` | `forest` | `fountain model` | `functional decomposition` | `grid charts` | `has-a-relationship` | `having verbs` | `hierarchical forms` | `loop` | `maintenance` | `mass nouns` | `member functions` | `message communications` | `methods` | `modular approach` | `object-oriented analysis` | `object-oriented design` | `object-oriented programming` | `objects` | `paradigm` | `problem definition` | `priority` | `space` | `prototype` | `prototyping` | `instances of objects` | `is-relationship` | `layout tools` | `procedures` | `process layering` | `program flowcharts` | `proper nouns` | `prototype` | `prototyping` | `second generation` | `selection` | `single-tree model` | `software life cycle` | `solution space` | `static verbs` | `structure chart` | `structured design` | `structured tools` | `system flowcharts` | `testing` | `textual analysis` | `third generation` | `tools` | `top-down approach` | `traditional tools` | `use relationship` | `Warnier diagrams` | `water-fall model`

## REVIEW QUESTIONS

### Cognitive Domain

- 17.1 根据您的看法，列出五项软件开发人员在设计系统时应牢记的最重要特征。
- 17.2 说明软件测试的重要性。
- 17.3 列出程序化与面向对象范式之间的关键差异。
- 17.4 阐述软件维护，以及何时以及如何进行维护的一般化描述。
- 17.5 解释系统开发生命周期的每个阶段的主要参与者。
- 17.6 阐明在分析阶段研究现有系统的必要性，并适当论证您的答案。
- 17.7 回顾经典软件开发生命周期的局限性。
- 17.8 “软件开发过程是迭代的”。进行讨论。
- 17.9 区分“waterfall”模型与“fountain”模型。
- 17.10 说明案例图（Case Diagram）的意义，并绘制出批发商-零售商关系的案例图。
- 17.11 区分对象导向的系统分析与系统设计。指出哪一阶段对系统开发人员的才能要求更高。
- 17.12 区分以下内容：
  (a) 分类关系与组合关系。
  (b) 继承关系与客户端-服务器关系。
  (c) 问题空间中的对象与解决空间中的对象。
  (d) 数据流图与层次图。
- 17.13 讨论结构化设计技术在面向对象编程中的应用。
- 17.14 列出在设计驱动程序时需要考虑的关键问题，并回顾每个问题的重要性。
- 17.15 “程序第一次就不能运行正确”。进行回顾。
- 17.16 回顾原型开发，并描述它如何帮助改进系统设计。

### Affective Domain

- 17.17 为以下陈述的正确性进行辩护：
  (a) 设计新系统时，一个重要的考虑因素是最终用户。
  (b) 用户在系统的分析与设计中不承担任何角色。
  (c) 决策表是数据流的图形化表示。
  (d) 数据流图的唯一目的是文档化。
  (e) 数据流图强调数据的逻辑流而非物理流。
  (f) 计算机输出可以设计成一种人性化的力量。
  (g) 结构化编程技术在面向对象程序设计中没有位置。
  (h) 原型不能改进为最终产品。

**Legend**

精确值/响应/组织/应用/记忆/理解

## MULTIPLE-CHOICE QUESTIONS

1. 哪一个不是瀑布模型 SDLC 的阶段？
- (a) 设计
- (b) 讨论
- (c) 编码
- (d) 测试

6. 为了展示系统不同模块之间的关系，我们使用：
- (a) 剧本
- (b) 结构图
- (c) 网格图
- (d) 决策树

2. 功能分解技术也被称为：
- (a) 自顶向下方法
- (b) 自底向上方法
- (c) 线性方法
- (d) 并行方法

7. 面向对象软件开发模型的组成部分：
- (a) 面向对象分析
- (b) 面向对象设计
- (c) 面向对象编程
- (d) 以上全部

3. 系统流程图在系统开发工具的哪一代被使用？
- (a) 第一代
- (b) 第二代
- (c) 第三代
- (d) 以上都不是

8. 不是面向对象分析的活动：
- (a) 问题定义
- (b) 要求规格
- (c) 识别对象
- (d) 识别模式

4. 哪一个与第三代系统开发无关？
- (a) 对象字典
- (b) 继承图
- (c) 数据流图
- (d) 结构图

9. 在面向对象设计的上下文中，下列关系中哪一个不相关：
- (a) 继承关系
- (b) 使用关系
- (c) 审查关系
- (d) 包含关系

5. Warnerier 图用于：
- (a) 表示程序结构
- (b) 表示条件
- (c) 表示结构存储库
- (d) 表示关系

10. 哪一个不是类层次结构？
- (a) 第一级
- (b) 单树
- (c) 森林
- (d) 多树

## APPENDIX

## A Implementation of Abstract Data Types

## INTRODUCTION

如第 1.5 节所述，抽象化是指在不包含背景细节或解释的情况下，表示关键特征的行为。类使用抽象化概念，定义为一组抽象属性（如大小、重量和成本）以及对这些属性进行操作的函数。它们封装了将要创建的对象的所有必要属性。这些属性有时被称为数据成员，因为它们保存信息。对这些属性进行操作的函数有时称为方法或成员函数。

由于类使用了数据抽象概念，它们被称为抽象数据类型（ADT）。数据抽象是面向对象编程的关键特征之一。

## DATA STRUCTURE

数据结构是用于存储数据所需的空间以及执行如插入、检索等操作所需的逻辑的组合。从用户想要使用和访问数据结构的角度来看，其关注点在于访问数据，而不是实现与之相关的逻辑的细节。数据抽象是一种过程，它使用户只关注数据，而无需关注维护数据的复杂细节。

数据结构主要分为两类：原始型和非原始型。原始型数据结构包括可以直接由机器级指令操作的基本数据结构。常见的原始型数据结构有整数、字符、实数、布尔值等。

非原始型数据结构则是指从一个或多个原始型数据结构中派生出的所有其他数据结构。创建非原始型数据结构的目的是形成集合化的同质或异质数据元素。

## LINEAR AND NON-LINEAR DATA STRUCTURES

非原始型数据结构进一步分为线性和非线性两类。在数据结构中，所有数据元素均以线性或顺序的方式排列。线性数据结构的示例包括数组、栈、队列、链表等。非线性数据结构则没有固定的顺序或序列，数据元素可以以层次结构方式排列。非线性数据结构的示例包括树和图。

数据项之间存在线性（一对一）关系的数据结构称为线性数据结构。该类包括列表（可实现为链表或数组）、栈和队列等。非线性数据结构则是指数据项之间存在非线性（一对多或多对多）关系的结构。示例包括树、二叉树、图等。

本节我们将实现栈和链表作为抽象数据类型。

## STACK

栈是一种线性数据结构，它以一种方式维护元素列表，使得元素只能从列表的一端进行插入或删除。这个端称为栈顶。栈基于后进先出（LIFO）原则，即最后加入栈的元素首先被移出。书本堆栈可以类比于栈数据结构，因为它只允许从栈顶端添加或移除书籍，而不能从中间进行操作。将元素压入栈的操作称为 `Push`，将元素弹出栈的操作称为 `Pop`。实现栈的最简单方式是使用数组存储元素，并使用一个整数变量 `top` 保存栈顶元素的下标。

下面给出 `MyStack` 类实现的伪代码（实际代码见 `mystack.h` 文件）。`MyStack` 使用模板，因此可以用于存储任意数据类型。

```
//mystack.h 文件

#include <iostream>
using namespace std;

template <class T = int> // 模板类
class MyStack
{
    T *arr;          // 指向元素数组的指针
    int size;        // 栈的最大容量
    int top;         // 栈顶元素的下标

public:
    MyStack()
    {
        size = 100;
        arr = new T[100];   // 默认大小为 100 的数组
        top = -1;
    }

    MyStack(int s)
    {
        size = s;
        arr = new T[s];     // 大小为 s 的数组
        top = -1;
    }

    ~MyStack()
    {
        delete[] arr;
    }

    void push(T d)                 // 将数据 d 压入栈
    {
        try {
            if (top == size - 1)
                throw size;          // 栈已满，抛出异常
            else arr[++top] = d;    // 否则在顶部位置存储元素
        }
        catch (int x) {
            cout << "The stack is full" << endl;
            exit(1);
        }
    }

    T pop()
    {
        try {
            if (top == -1)
                throw top;           // 栈为空，抛出异常
            else return arr[top--];  // 否则返回并移除顶部元素
        }
        catch (int x) {
            cout << "The stack is empty" << endl;
            exit(1);
        }
    }

    bool is_empty()
    {
        return top == -1;
    }

    bool is_full()
    {
        return top == size - 1;
    }

    int stackcount()
    {
        return top + 1;
    }
}
```

`MyStack` 类可以在任何程序中用于存储任意类型的数据。下面给出在 `demo.cpp` 文件中使用该类的示例代码。

```
//demo.cpp
#include <iostream>                     // 包含 MyStack 类的定义
#include "mystack.h"
using namespace std;

int main()
{
    MyStack <char> s1;                 // 创建字符类型的栈，默认大小 100
    s1.push('A');                      // 将字符 'A' 压入栈
    cout << s1.pop() << endl;          // 弹出并输出 'A'
    MyStack <> s2(5);                  // 创建默认整型栈，大小为 5
    s2.push(20);                       // 压入 20
    s2.push(30);                       // 压入 30
    s2.push(40);                       // 压入 40
    s2.push(50);                       // 压入 50
    s2.push(60);                       // 压入 60
    s2.push(70);                       // 尝试压入 70，会触发栈溢出
    Overflow message
    cout << s2.pop() << " " << s2.pop() << " " << s2.pop()
         << " " << s2.pop() << " " << s2.pop() << endl;   // 连续弹出 5 次
                                            // 执行 5 次连续弹出操作
    cout << s2.pop();                    // 尝试第 6 次弹出，会触发栈空异常
    Stack under message
    return 0;
}
```

程序 `demo.cpp` 的输出如下：

A  

The stack is full  

60 50 40 30 20  

The stack is empty  

下面的图展示了在对 `s2` 进行 5 次连续的 `push` 操作后，栈的内容以及每次插入后 `top` 的值。

## 后缀算术表达式的评估
