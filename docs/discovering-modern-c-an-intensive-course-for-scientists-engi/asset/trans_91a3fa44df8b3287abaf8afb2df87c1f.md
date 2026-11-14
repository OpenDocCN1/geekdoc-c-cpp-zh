

- 指针和引用：指向对象类型的任何指针都可以转换为 void*（虽然这是邪恶的旧式技巧）。相比之下，指向函数或成员的指针不能转换为 void*。派生类的指针/引用可以隐式转换为（无歧义的）基类的指针/引用。0（或产生 0 的表达式）可以转换为任何指针类型，结果为空指针。nullptr 更可取。T* 可以转换为 const T*，同样 T& 可以转换为 const T&。

- 布尔型：指针、整型和浮点型值可以转换为 bool：零值变为 false，其他所有值变为 true。这些转换都没有助于理解程序。

- 整型<->浮点型：当浮点型转换为整型时，小数部分被舍弃（向 0 舍入）。如果值太大无法表示，行为是未定义的。当整型可以在目标类型中表示时，从整型到浮点型的转换是精确的。否则，会取下一个更低或更高的浮点型值（哪一个取决于实现）。在不太可能的情况下，如果它对于浮点型来说太大，行为是未定义的。

来源：[43, §10.5.2] 和标准。

## C.3.3 通常算术转换

这些转换在二元运算符的操作数上执行，将它们转换为一个公共类型，然后用作结果类型：

1. 如果任一操作数是 long double，则另一个转换为 long double；
- 否则，如果任一操作数是 double，则另一个转换为 double；
- 否则，如果任一操作数是 float，则另一个转换为 float；
- 否则，对两个操作数执行第 C.3.1 节中的整型提升。

2. 否则，如果任一操作数是 unsigned long long，则另一个转换为 unsigned long long；
- 否则，如果一个操作数是 long long 而另一个是 unsigned long，则当后者能表示前者的所有值时，unsigned long 转换为 long long；否则，两者都转换为 unsigned long long。
- 否则，如果一个操作数是 long 而另一个是 unsigned int，则当后者能表示前者的所有值时，unsigned int 转换为 long；否则，两者都转换为 unsigned long。
- 否则，如果任一操作数是 long，则另一个转换为 long；
- 否则，如果任一操作数是 unsigned，则另一个转换为 unsigned；
- 否则，两个操作数都转换为 int。

因此，混合有符号和无符号整数的程序具有平台相关的行为，因为转换规则取决于整型类型的大小。来源：[43, §10.5.3]。

## C.3.4 窄化转换

窄化转换是一种隐式转换：

- 从浮点型到整型；或
- 从 long double 到 double 或 float，或从 double 到 float，除非源是常量表达式且转换后的实际值在可表示值的范围内（即使无法精确表示）；或
- 从整型或无作用域枚举类型到浮点型，除非源是常量表达式且转换后的实际值能适合目标类型，并且转换回原始类型时会产生原始值；或
- 从整型或无作用域枚举类型到不能表示原始类型所有值的整型，除非源是常量表达式且转换后的实际值能适合目标类型，并且转换回原始类型时会产生原始值。

来源：ISO 标准。

## 参考文献

- [1] D. Abrahams 和 A. Gurtovoy，《C++ 模板元编程：来自 Boost 及更远的概念、工具和技术》。Addison-Wesley，2004年。

- [2] D. Adams，“生命、宇宙以及一切”，《银河系搭车客指南》，Pan Macmillan，1980年。

- [3] M. H. Austern，《泛型编程与 STL：使用和扩展 C++ 标准模板库》。专业计算系列。Addison-Wesley，1998年。

- [4] J. J. Barton 和 L. R. Nackman，《科学与工程 C++》。Addison-Wesley，1994年。

- [5] L. S. Blackford, A. Petitet, R. Pozo, K. Remington, R. C. Whaley, J. Demmel, J. Dongarra, I. Duff, S. Hammarling, G. Henry 等人，“一组更新的基本线性代数子程序 (BLAS)”，《ACM 数学软件事务》，第 28 卷，第 2 期，第 135–151 页，2002年。

- [6] W. E. Brown，“三个与 <random> 相关的提案，v2”，技术报告 N3742，ISO/IEC JTC 1，信息技术，SC 22 分委会，编程语言 C++，2013年8月。

- [7] “C++ 参考：隐式转换。” http://en.cppreference.com/w/cpp/language/implicit_cast.

- [8] K. Czarnecki 和 U. W. Eisenecker，《生成式编程：方法、工具和应用》。ACM Press/Addison-Wesley，2000年。

- [9] K. Czarnecki 和 U. Eisenecker，“用于模板元编程的元控制结构。” http://home.t-online.de/home/Ulrich.Eisenecker/meta.htm.

- [10] I. Danaila, F. Hecht 和 O. Pironneau，《C++ 中的数值模拟》。Dunod，巴黎，2003年。

- [11] L. Dionne，“Boost.hana。” http://ldionne.com/hana/index.html，2015年。

- [12] S. Du Toit，“C++ API 的沙漏接口。” http://de.slideshare.net/StefanusDuToit/cpp-con-2014-hourglass-interfaces-for-c-apis，2014年。

- [13] M. A. Ellis 和 B. Stroustrup，《C++ 参考手册注释版》。Addison-Wesley，1990年。

- [14] E. Gamma, R. Helm, R. Johnson 和 J. Vlissides，《设计模式：可复用面向对象软件的基础》。Addison-Wesley，1994年。

- [15] B. Ganter 和 R. Wille, *形式概念分析：数学基础*. Springer Science & Business Media, 2012年。

- [16] P. Gottschling, "类模板特化中的代码复用," Tech. Rep. N3596, ISO IEC JTC1/SC22/WG21, 2013年。http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2013/n3596.pdf.

- [17] P. Gottschling, *矩阵模板库 4*. SimuNova, 2014年. mtl4.org.

- [18] P. Gottschling, *混合复杂算术*. SimuNova, 2011年. https://simunova.zih.tu-dresden.de/mtl4/docs/mixed__complex.html, 矩阵模板库 4 的一部分。

- [19] P. Gottschling 和 A. Lumsdaine, "集成语义与编译：使用 C++ 概念开发健壮高效的可复用库," in *GPCE '08：第 7 届生成式编程与组件工程国际会议论文集*, pp. 67–76, ACM, 2008年。

- [20] P. Gottschling, D. S. Wise, 和 A. Joshi, "面向科学计算的算法和结构递归的泛型支持," *并行、新兴和分布式系统国际期刊 (IJPEDS)*, vol. 24, no. 6, pp. 479–503, 2009年12月。

- [21] D. Gregor, "ConceptGCC," 2007年. http://www.generic-programming.org/software/ConceptGCC/.

- [22] A. Gurtovoy 和 D. Abrahams, *Boost 元编程库*. Boost, 2014年. www.boost.org/doc/libs/1_56_0/libs/mpl.

- [23] E. Hairer, S. Norsett, 和 G. Wanner, *求解常微分方程 I：非刚性问题*. 计算数学 Springer 系列, Springer Berlin Heidelberg, 2008年。

- [24] M. R. Hestenes 和 E. Stiefel, "求解线性系统的共轭梯度方法," *国家标准局研究杂志*, vol. 49, no. 6, pp. 409–436, 1952年12月。

- [25] R. W. Hockney, *计算机基准测试科学*, vol. 2. SIAM, 1996年。

- [26] N. Josuttis, *C++ 标准库：教程与参考，第 2 版*. Addison-Wesley, 2012年。

- [27] B. Karlsson, *超越 C++ 标准库*. Addison-Wesley, 2005年。

- [28] KjellKod.cc, "数值运算：为什么你应该永远、永远、永远不要在代码中再次使用链表." http://www.codeproject.com/Articles/348797/Number-crunching-Why-you-should-never-ever-EVER-us, 2012年8月。

- [29] K. Meerbergen, *泛型线性代数软件*. K.U. Leuven, 2014年. http://people.cs.kuleuven.be/~karl.meerbergen/glas/.

