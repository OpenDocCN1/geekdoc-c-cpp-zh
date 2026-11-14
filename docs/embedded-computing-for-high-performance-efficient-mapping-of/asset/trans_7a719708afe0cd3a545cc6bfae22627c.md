

```
aspectdef CloningAndTransformations

  Input
    funcName = 'fun1';
  end

  /* The names of the new functions */
  var newName = funcName + '_new';
  var newName = funcName + '_new';

  /* Clone functions */
  select function(funcName) end
  apply
    exec Clone(newName);
  end

  /* Perform optimizations */
  select function(newName).loop end
  apply
    exec Tiling(32);
  end
  condition $loop.is_outermost end

  /* Change calls to the function */
  select file.call(newName) end
  apply
    var originalCode = $call.code + ';';
    var tiledCode = originalCode.split(funcName).join(tiled);

    insert before '/*';
    insert after '*/';

    insert after %{
      switch (get_version(/* ... */) ) {
        case 1: [[originalCode]] break;
        case 2: [[tiledCode]] break;
        default: [[originalCode]] break;
      }
    %}
  end
end
```

图 5.16
LARA 中的函数克隆与优化。

```
aspectdef CompoundLoopTrans

  select function().($11-loop).($12-loop) end
  apply
    exec Coalescing($11, $12);
  end
  condition $12.is_innermost end

  select function().loop end
  apply
    exec Unroll(2);
  end
  condition $loop.is_innermost end
end
```

图 5.17
在 LARA 中组合循环变换序列。

```
aspectdef SimpleUnrollAndJam

  var LoopsToMerge = [];

  select function.($11-loop).($12-loop) end
    apply
      exec Unroll($11, 2);
    end
  condition $12.is_innermost end

  select function.loop end
    apply
      LoopsToMerge.push($loop);
    end
  condition $11.is_innermost end

  select function end
    apply
      exec Merge(LoopsToMerge);
    end
  end
```

## 图 5.18

在 LARA 中使用循环展开和循环合并指定的循环展开与合并。

## 5.13 小结

本章介绍了几种通常被认为可以提升性能、降低功耗或能耗的代码变换。代码变换的组合多样且庞大，据我们所知，不存在能够自动执行所有这些变换的编译器或源码到源码编译器。事实上，大多数编译器（包括 GCC）仅支持本章介绍的代码变换中的有限集合。这使得用户对它们的了解变得更加重要。然而，应用这些变换中的大多数的决策并不容易，需要特定的专业知识和/或尝试-评估方法。在大多数情况下，如果没有实际测量，很难理解特定代码变换在性能/能耗/功耗方面的影响，以及应用该变换可能带来的任何进一步优化机会。尽管如此，代码分析工具提供的信息、对代码的手动分析或运行时分析通常有助于指导开发者选择使用哪些代码变换。

## 5.14 延伸阅读

关于代码变换的文献非常庞大，因为它们在许多应用领域中被使用。代码变换的一个重要方面是用于代码分析的底层技术，不仅用于确定其合法性，还用于确定其潜在盈利能力。代码分析技术是任何编译器的一部分，如文献中广泛描述的那样（参见，例如，[29,30,31,32]）。

大多数已提出的循环变换通常与特定的出版物相关联，循环版本化 [33] 就是一个例子。然而，我们建议感兴趣的读者参考 Ref. [34] 中提出的侧重于循环变换的代码变换综述。对于有兴趣了解特定主题更多信息的读者，存在相关参考文献。例如，Ref. [16] 中关于 JavaScript 代码上下文中 JIT 特化的工作包括对特化的非常通用和全面的概述。

其他代码变换，例如代码特化，是高级 JIT 编译器的一部分，例如用于执行 Java 字节码或 JavaScript 代码的编译器（参见，例如，[16,53,36]）。虽然 JIT 编译器没有昂贵的编译时静态分析的优势，但它们有使用运行时数据知识的优势（参见，例如，[37]），因此能更好地评估特化对性能或功耗等指标的影响。即使在生成的代码中折叠了有限的静态编译时信息，也能让它们动态调整代码的执行。

代码变换也可能对于满足本书未涉及的其他非功能性需求很重要。例如，安全要求可能从软件技术中获益，因此适合进行代码变换（参见，例如，[38,39]）。一个例子是通过在软件代码级别应用三模冗余（TMR）技术来提高韧性。

## 参考文献

- [1] Polychronopoulos CD. 面向并行机的循环合并：一种编译器变换。载于：国际并行处理会议论文集；1987. p. 235–42.
- [2] Kuck DJ, Kuhn RH, Leasure B, Wolfe M. 面向流水线处理器的高级向量化器结构。载于：IEEE 计算机学会第四届国际计算机软件与应用会议论文集，1980年10月。p. 709–15.
- [3] Glulum AM, Fisher AL. 不规则递归循环嵌套的扁平化与并行化。ACM SIGPLAN Not 1995;30(8):58–67.
- [4] Kennedy K, McKinley KS. 通过循环融合与分布最大化循环并行性并改善数据局部性。载于：第6届并行计算语言与编译器国际研讨会论文集。伦敦：Springer-Verlag；1994。p. 301–20.
- [5] Yi Q, Kennedy K, Adve V. 面向局部性的复杂嵌套循环变换。J SuperComput 2000;27(3):219–64.
- [6] Darte A, Huard G. 面向循环紧凑的循环移位。Int J Parallel Prog 2000; 28(5):499–534.
- [7] Wolfe M. 循环倾斜：波前方法再探。Int J Parallel Prog 1986; 15(4):279–93.
- [8] Lam M. 软件流水线：面向VLIW机器的有效调度技术。载于：Wexelblat RL（编）。ACM SIGPLAN 程序设计语言设计与实现会议论文集（PLDI’88）。纽约，NY：ACM；1988。p. 318–28.
- [9] Ramakrishna Rau B. 迭代模数调度：一种软件流水线循环算法。载于：第27届年度国际微架构研讨会论文集（MICRO 27）。纽约，NY：ACM；1994。p. 63–74.
- [10] Jeong Y, Seo S, Lee J. 面向含条件循环的高效流水线的求值器-执行器变换。ACM Trans Archit Code Optim 2013;10(4): Article 62, 23 pages.
- [11] Misailovic S, Sidiroglou S, Hoffmann H, Rinard M. 服务质量分析。载于：第32届ACM/IEEE国际软件工程会议论文集（ICSE’10），卷1。纽约，NY：ACM；2010。p. 25–34.
- [12] McKinley KS. 面向共存内存多处理器的编译器优化算法。IEEE Trans Parallel Distrib Syst 1998;9(9):769–87.
- [13] Davidson JW, Jinturkar S. 内存访问扩展：一种消除冗余内存访问的技术。载于：ACM SIGPLAN 1994程序设计语言设计与实现会议论文集（PLDI’94）。纽约，NY：ACM；1994。p. 186–95.
- [14] Rudy G, Khan MM, Hall M, Chen C, Chame J. 描述变换和代码生成的编程语言接口。载于：Cooper K, Mellor-Crummey J, Sarkar V（编）。第23届并行计算语言与编译器国际会议论文集（LCPC’10），柏林/海德尔堡：Springer-Verlag；2010。p. 136–50.
- [15] Jones ND, Gomard CK, Sestoft P. 部分求值与自动程序生成。第1版。上萨德尔河，NJ：Prentice-Hall；1993.
- [16] Costa IRdA, Santos HN, Alves PRO, Pereira FMQ. 即时值特化。Comput Lang Syst Struct 2014;40(2):37–52.
- [17] Weisstein EW. 泰勒级数。来自 MathWorld—Wolfram 网络资源。http://mathworld.wolfram.com/TaylorSeries.html [访问日期：2016年11月].
- [18] Weisstein EW. 牛顿法。来自 MathWorld—Wolfram 网络资源。http://mathworld.wolfram.com/NewtonsMethod.html [访问日期：2016年11月].
- [19] Lim AW, Liao S-W, Lam MS. 基于仿真分区的任意嵌套循环的分块与数组收缩。载于：第八届ACM SIGPLAN 并行编程原理与实践研讨会论文集（PPoPP’01）。纽约，NY：ACM；2001。p. 103–12.
- [20] Sarkar V, Gao GR. 通过集体循环变换优化数组访问。载于：Davidson ES, Hossfeld F（编）。第5届国际超级计算会议论文集（ICS ’91）。纽约，NY：ACM；1991。p. 194–205.
- [21] Franke B, O’Boyle MPF. 面向DSP应用的数组恢复与高级变换。ACM Trans Embed Comput Syst 2003;2(2):132–62.
- [22] Dolby J, Chien A. 自动对象内联及其评估。载于：ACM SIGPLAN 程序设计语言设计与实现会议论文集（PLDI’00）。纽约，NY：ACM；2000。p. 345–57.
- [23] Dobb J. 对象的自动内联分配。载于：Michael Berman A（编）。ACM SIGPLAN 程序设计语言设计与实现会议论文集（PLDI’97）。纽约，NY：ACM；1997。p. 7–17.
- [24] Thies W, Karczmarek M, Amarasinghe SP. StreamIt：一种面向流媒体应用的语言。载于：Nigel Horspool R（编）。第11届国际编译器构建会议论文集（CC’02）。伦敦：Springer-Verlag；2002。p. 179–96.
- [25] Hiranandani S, Kennedy K, Tseng C-W. 面向MIMD分布式存储机器的Fortran D编译。Commun ACM 1992;35(8):66–80.
- [26] Chapman B, Jost G, van der Pas R. 使用 OpenMP：可移植共存内存并行编程（科学与工程计算）。剑桥，MA：MIT Press；2007.
- [27] Kumar K, Liu J, Lu Y-H, Bhargava B. 移动系统计算卸载综述。Mob Netw Appl 2013;18(1):129–40.

