
在莱斯大学[4]，以及由 Allen 在 IBM Research 领导的 PTRAN 项目[2]。

McKellar 和 Coffman[19]首次讨论了利用分块来改善数据局部性。Lam、Rothberg 和 Wolf[12]首次对现代体系结构上缓存分块进行了深入的实证分析。Wolf 和 Lam[27]使用线性代数技术来计算循环中的数据重用。Sarkar 和 Gao[24]引入了数组收缩优化。

Lamport[13]首次将循环建模为迭代空间，并使用超平面法（仿射变换的一种特殊情况）为多处理器寻找并行性。仿射变换源于脉动阵列算法设计[11]。脉动阵列原本是直接在 VLSI 中实现的并行算法，因此要求在并行化的同时最小化通信。人们发展了代数技术，将计算映射到空间和时间坐标上。仿射调度的概念以及 Farkas 引理在仿射变换中的使用由 Feautrier[8]引入。这里描述的仿射变换算法基于 Lim 等人[15, 14, 16]的工作。

Porterfield[22]提出了最早的编译器预取数据算法之一。Mowry、Lam 和 Gupta[20]应用重用分析来最小化预取开销，并获得整体性能提升。

## 11.13. 第11章参考文献

- 1. Abu-Sufah, W.、D. J. Kuck 和 D. H. Lawrie，“通过程序分析与变换提升分页系统性能”，*IEEE Trans. on Computing* C-30:5 (1981), pp. 341–356.
- 2. Allen, F. E.、M. Burke、P. Charles、R. Cytron 和 J. Ferrante，“用于多处理的 PTRAN 分析系统概述”，*J. Parallel and Distributed Computing* 5:5 (1988), pp. 617–640.
- 3. Allen, F. E. 和 J. Cocke，“优化变换目录”，载于 *Design and Optimization of Compilers*（R. Rustin 编），pp. 1–30, Prentice-Hall, 1972.
- 4. Allen, R. 和 K. Kennedy，“将 Fortran 程序自动转换为向量形式”，*ACM Transactions on Programming Languages and Systems* 9:4 (1987), pp. 491–542.
- 5. Banerjee, U.，*普通程序中的数据依赖*，硕士论文，伊利诺伊大学厄巴纳-香槟分校计算机科学系，1976。
- 6. Banerjee, U.，*普通程序的加速*，博士论文，伊利诺伊大学厄巴纳-香槟分校计算机科学系，1979。
- 7. Dantzig, G. 和 B. C. Eaves，“Fourier-Motzkin 消元及其对偶”，*J. Combinatorial Theory, A* 14 (1973), pp. 288–297.
- 8. Feautrier, P.，“仿射调度问题的一些高效解法：I. 一维时间”，*International J. Parallel Programming* 21:5 (1992), pp. 313–348.
- 9. Hennessy, J. L. 和 D. A. Patterson，*计算机体系结构：量化研究方法*，第三版，Morgan Kaufmann，旧金山，2003。
- 10. Kuck, D.、Y. Muraoka 和 S. Chen，“类 Fortran 程序中可同时执行的操作数量及其带来的加速”，*IEEE Transactions on Computers* C-21:12 (1972), pp. 1293–1310.
- 11. Kung, H. T. 和 C. E. Leiserson，“脉动阵列（用于 VLSI）”，载于 Duff, I. S. 和 G. W. Stewart（编），*Sparse Matrix Proceedings*，pp. 256–282。Society for Industrial and Applied Mathematics，1978。
- 12. Lam, M. S.、E. E. Rothberg 和 M. E. Wolf，“分块算法的缓存性能与优化”，*Proc. Sixth International Conference on Architectural Support for Programming Languages and Operating Systems* (1991), pp. 63–74.
- 13. Lamport, L.，“DO 循环的并行执行”，*Comm. ACM* 17:2 (1974), pp. 83–93.
- 14. Lim, A. W.、G. I. Cheong 和 M. S. Lam，“一种最大化并行性并最小化通信的仿射划分算法”，*Proc. 13th International Conference on Supercomputing* (1999), pp. 228–237.
- 15. Lim, A. W. 和 M. S. Lam，“利用仿射变换最大化并行性并最小化同步”，*Proc. 24th ACM SIGPLAN-SIGACT Symposium on Principles of Programming Languages* (1997), pp. 201–214.
- 16. Lim, A. W.、S.-W. Liao 和 M. S. Lam，“使用仿射划分在任意嵌套循环上进行分块与数组收缩”，*Proc. ACM SIGPLAN Symposium on Principles and Practice of Parallel Programming* (2001), pp. 103–112.
- 17. Loveman, D. B.，“通过源到源变换改进程序”，*J. ACM* 24:1 (1977), pp. 121–145.
- 18. Maydan, D. E.、J. L. Hennessy 和 M. S. Lam，“一种精确依赖分析的高效方法”，*Proc. ACM SIGPLAN 1991 Conference on Programming Language Design and Implementation*, pp. 1–14.
- 19. McKellar, A. C. 和 E. G. Coffman，“分页多道程序设计环境中的矩阵组织与矩阵运算”，*Comm. ACM* 12:3 (1969), pp. 153–165.
- 20. Mowry, T. C.、M. S. Lam 和 A. Gupta，“一种预取编译器算法的设计与评估”，*Proc. Fifth International Conference on Architectural Support for Programming Languages and Operating Systems* (1992), pp. 62–73.
- 21. Padua, D. A. 和 M. J. Wolfe，“面向超级计算机的高级编译器优化”，*Comm. ACM*，**29**:12 (1986), pp. 1184–1201.
- 22. Porterfield, A.，*改善超级计算机应用缓存性能的软件方法*，博士论文，莱斯大学计算机科学系，1989。
- 23. Pugh, W. 和 D. Wonnacott，“使用 Omega 测试消除误报”，*Proc. ACM SIGPLAN 1992 Conference on Programming Language Design and Implementation*, pp. 140–151.
- 24. Sarkar, V. 和 G. Gao，“通过集体循环变换优化数组访问”，*Proc. 5th International Conference on Supercomputing* (1991), pp. 194–205.
- 25. Shostak, R.，“通过计算循环剩余量判定线性不等式”，*J. ACM*，**28**:4 (1981), pp. 769–779.
- 26. Towle, R. A.，*程序变换中的控制依赖与数据依赖*，博士论文，伊利诺伊大学厄巴纳-香槟分校计算机科学系，1976。
- 27. Wolf, M. E. 和 M. S. Lam，“一种数据局部性优化算法”，*Proc. SIGPLAN 1991 Conference on Programming Language Design and Implementation*, pp. 30–44.
- 28. Wolfe, M. J.，*改善程序固有并行性的技术*，硕士论文，伊利诺伊大学厄巴纳-香槟分校计算机科学系，1978。

## 附录 A

## 一个完整的前端

本附录中完整的编译器前端基于第2.5～2.8节中非形式化描述的简单编译器。与第2章的主要区别在于，该前端为布尔表达式生成跳转代码，如第6.6节所述。我们首先给出源语言的语法，该语法由文法描述，需要针对自顶向下分析进行调整。

该翻译器的 Java 代码由五个包组成：`main`、`lexer`、`symbols`、`parser` 和 `inter`。包 `inter` 包含抽象语法中语言构造对应的类。由于解析器的代码与其余包交互，因此最后讨论它。每个包存储为单独的目录，每个类对应一个文件。

进入解析器时，源程序由记号流组成，因此面向对象与解析器代码关系不大。离开解析器时，源程序由语法树组成，其中构造或节点实现为对象。这些对象要处理以下所有工作：构造语法树节点、检查类型，以及生成三地址中间代码（见包 `inter`）。

### A.1  源语言

该语言中的程序由一个带有可选声明和语句的块组成。记号 `basic` 表示基本类型。

```
program → block
block   → { decls stmts }
decls   → decls decl | ε
decl    → type id ;
type    → type [ num ] | basic
stmts   → stmts stmt | ε
```

将赋值视为语句，而不是表达式中的运算符，可以简化翻译。

