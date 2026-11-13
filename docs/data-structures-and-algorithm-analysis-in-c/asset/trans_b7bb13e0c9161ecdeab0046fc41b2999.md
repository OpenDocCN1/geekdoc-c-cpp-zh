

- 20. D. W. Jones, “优先队列与事件集实现的实证比较,” *计算机通信*, 29 (1986), 300–311.

- 21. J. Karkkainen 和 P. Sanders, “简单线性工作后缀数组构建,” *第十三届自动机、语言与编程国际研讨会论文集* (2003), 943–955.

- 22. T. Kasai, G. Lee, H. Arimura, S. Arikawa, 和 K. Park, “后缀数组中线性时间最长公共前缀计算及其应用,” *第十二届组合模式匹配年会论文集* (2001), 181–192.

- 23. P. Ko 和 S. Aluru, “空间高效的线性时间后缀数组构建,” *第十四届组合模式匹配年会论文集* (2003), 203–210.

- 24. D. T. Lee 和 C. K. Wong, “多维二叉搜索树和平衡四叉树中区域和部分区域搜索的最坏情况分析,” *信息学报*, 9 (1977), 23–29.

- 25. U. Manber 和 G. Myers, “后缀数组：一种用于在线字符串搜索的新方法,” *SIAM 计算期刊*, 22 (1993), 935–948.

- 26. W. A. Martin 和 D. N. Ness, “基于排序算法生长的二叉树优化,” *计算机通信*, 15 (1972), 88–93.

- 27. E. McCreight, “优先搜索树,” *SIAM 计算期刊*, 14 (1985), 257–276.

- 28. E. M. McCreight, “一种节省空间的后缀树构建算法,” *ACM 期刊*, 23 (1976), 262–272.

- 29. B. M. E. Moret 和 H. D. Shapiro, “构建最小生成树算法的实证分析,” *第二届算法与数据结构研讨会论文集* (1991), 400–411.

- 30. J. Nievergelt 和 E. M. Reingold, “有界平衡二叉搜索树,” *SIAM 计算期刊*, 2 (1973), 33–43.

- 31. M. H. Overmars 和 J. van Leeuwen, “基于四叉树和 K-D 树的动态多维数据结构,” *信息学报*, 17 (1982), 267–285.

- 32. S. Pettie, “走向配对堆的最终分析,” *第四十六届 IEEE 计算机科学基础年会论文集* (2005), 174–183.

- 33. S. J. Puglisi, W. F. Smyth, 和 A. Turpin, “后缀数组构建算法分类学,” *ACM 计算机调查*, 39 (2007), 1–31.

- 34. H. Samet, “四叉树及相关层次数据结构,” *计算机调查*, 16 (1984), 187–260.

- 35. R. Sedgewick 和 K. Wayne, *算法*, 第 4 版, Addison-Wesley Professional, Boston, Mass, 2011.

- 36. D. D. Sleator 和 R. E. Tarjan, “自调整二叉搜索树,” *ACM 期刊*, 32 (1985), 652–686.

- 37. J. T. Stasko 和 J. S. Vitter, “配对堆：实验与分析,” *计算机通信*, 30 (1987), 234–249.

- 38. C. J. Stephenson, “通过在根节点插入构建二叉搜索树的方法,” *计算机与信息科学国际期刊*, 9 (1980), 15–29.

- 39. E. Ukkonen, “后缀树的在线构建,” *算法学*, 14 (1995), 249–260.

- 40. J. Vuillemin, “数据结构的统一视角,” *计算机通信*, 23 (1980), 229–239.

- 41. P. Weiner, “线性模式匹配算法,” *第十四届 IEEE 开关与自动机理论年会论文集* (1973), 1–11.

## 类模板的分离编译

如果我们在类模板的声明中完全实现它，那么如前面所见，语法非常少。事实上，许多类模板都是以这种方式实现的，因为编译器对模板分离编译的支持历来较弱且具有平台特定性。因此，在许多情况下，整个类及其实现都放在一个头文件中。标准库的流行实现遵循此策略来实现类模板。

图 A.1 显示了 MemoryCell 类模板的声明。这部分当然很简单，因为它只是我们已经见过的整个类模板的一个子集。

对于实现，我们有一组函数模板。这意味着每个函数都必须包含模板声明，并且在使用作用域运算符时，类名必须用模板参数进行实例化。因此，在图 A.2 中，类名为 MemoryCell<Object>。尽管语法看起来足够无害，但可能会变得相当繁琐。例如，在规范中定义 operator= 不需要额外的负担。在实现中，我们会有下面这段残酷的代码：

```
template <typename Object>
const MemoryCell<Object> &
MemoryCell<Object>::operator= ( const MemoryCell<Object> & rhs )
{
    if ( this != &rhs )
        storedValue = rhs.storedValue;
    return *this;
}
```

1 请注意，某些 MemoryCell<Object> 的出现（即 :: 之后的那些）可以省略，编译器会将 MemoryCell 解释为 MemoryCell<Object>。

```
#ifndef MEMORY_CELL_H
#define MEMORY_CELL_H

/**
 * A class for simulating a memory cell.
 */
template <typename Object>
class MemoryCell
{
 public:
    explicit MemoryCell( const Object & initialValue = Object{ } );
    const Object & read( ) const;
    void write( const Object & x );

 private:
    Object storedValue;
};

#endif
```

**图 A.1** MemoryCell 类模板接口

即便如此，现在的问题变成了如何组织类模板声明和成员函数模板定义。主要问题是，图 A.2 中的实现并非实际函数；它们只是等待展开的模板。但是，即使在实例化 MemoryCell 模板时，它们也不会被展开。每个成员函数模板仅在被调用时才会展开。

## A.1 所有内容都在头文件中

第一种选择是将声明和实现都放在头文件中。这对于类来说行不通，因为如果多个不同的源文件包含处理该头文件的 include 指令，可能会导致多重定义的函数；但由于这里的一切都是模板而不是实际类，因此没有问题。

采用此策略，为了便于阅读，可以简单地让头文件发出一条 include 指令（在 #endif 之前）以自动读入实现文件。采用此策略，存储模板的 .cpp 文件不会被直接编译。

## A.2 显式实例化

在某些编译器上，如果使用显式实例化，我们可以获得许多分离编译的好处。在这种情况下，我们像通常为类所做的那样设置 .h 和 .cpp 文件。因此，图 A.1 和图 A.2 将完全按当前所示。头文件将没有读取实现的 include 指令。主程序将只有针对头文件的 include 指令。图 A.3 显示了一个典型的测试程序。如果我们编译两个 .cpp 文件，会发现找不到已实例化的成员函数。我们通过创建一个包含我们使用的类型的 MemoryCell 显式实例化的单独文件来修复此问题。显式实例化的示例在图 A.4 中显示。此文件作为项目的一部分进行编译，而模板实现文件（图 A.2）不作为项目的一部分编译。我们使用此技术配合多个旧编译器取得了成功。缺点是程序员必须列出所有模板展开，并且当类模板使用其他类模板时，有时也必须列出那些模板。优点是，如果 MemoryCell 中成员函数的实现发生更改，只需重新编译 MemoryCellExpand.cpp。

```
1 #include "MemoryCell.h"
2 
3 /**
4  * Construct the MemoryCell with initialValue.
5  *
6  */
7 template <typename Object>
8 MemoryCell<Object>::MemoryCell( const Object & initialValue )
9   : storedValue{ initialValue }
10 {
11 }
12 
13 /**
14  * Return the stored value.
15  *
16  */
17 template <typename Object>
18 const Object & MemoryCell<Object>::read( ) const
19 {
20   return storedValue;
21 }
22 
23 /**
24  * Store x.
25  *
26  */
27 template <typename Object>
28 void MemoryCell<Object>::write( const Object & x )
29 {
30   storedValue = x;
31 }
```

**图 A.2 MemoryCell 类模板实现**

