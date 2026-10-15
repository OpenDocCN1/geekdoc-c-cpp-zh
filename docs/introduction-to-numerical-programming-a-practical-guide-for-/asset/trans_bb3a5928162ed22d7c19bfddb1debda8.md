

ipass += 1                                          # increase pass counter
swap = 0                                            # initialize swap flag
for i in range(1,n-ipass+1):                        # loop over unsorted sublists
    ncomp += 1  #--------------------------------------------
    if (x[i] > x[i+1]):                             # compare neighbors
        nsaves += 3  #----------------------------------------
        xi = x[i]; x[i] = x[i+1]; x[i+1] = xi            # swap neighbors
        swap = 1                                        # set swap flag

#==================================================================
def InsertSort(x, n):
#------------------------------------------------------------------
# Ascending sort of array x[1..n] by direct insertion
#------------------------------------------------------------------

global ncomp, nsaves                                   # no. of compares and saves
for ipiv in range(2,n+1):                              # loop over pivots
    nsaves += 1  #--------------------------------------------
    xpiv = x[ipiv]                                     # save pivot to free its location
    i = ipiv - 1                                       # initialize sublist counter
    ncomp += 1  #--------------------------------------------
    while ((i > 0) and (x[i] > xpiv)):                 # scan to the left of pivot
        nsaves += 1  #----------------------------------------
        x[i+1] = x[i]                                   # item > pivot: shift to the right
        i -= 1

    nsaves += 1  #--------------------------------------------
    x[i+1] = xpiv                                      # insert pivot into last freed location

#==================================================================
def QuickSort(x, l, n):
#------------------------------------------------------------------
# Ascending sort of array x[1..n] by Quicksort
#------------------------------------------------------------------

global ncomp, nsaves                                   # no. of compares and saves
if (l >= n): return
                                                    # pivot = x[n]; create "<" and ">=" lists
m = l                                               # upper index in "<"-list
for i in range(l,n):                                # scan entire list, excepting pivot
    ncomp += 1  #--------------------------------------------
    if (x[i] < x[n]):                               # compare current value with pivot
        nsaves += 3  #----------------------------------------
        t = x[i]; x[i] = x[m]; x[m] = t              # swap < value to end of "<"-list
        m += 1                                      # extend "<"-list: increase upper index

nsaves += 3  #--------------------------------------------
t = x[m]; x[m] = x[n]; x[n] = t                      # swap pivot between "<" and ">=" lists

QuickSort(x,l,m-1)                                  # sort "<"-list

QuickSort(x,m+1,n)                                  # sort ">="-list

与第一个任务相关的完整程序分别可在文件 P04-SortComp0.py 和 P04-SortComp0.cpp 中找到，它们将输出打印到文件 sort.txt。文件 P04-SortComp1.py 和 P04-SortComp1.cpp 中包含的程序变体已添加图形功能，并生成第二项任务要求的绘图。通过运行这些程序得到的运算次数随序列长度的变化典型依赖关系如图 4.3 所示。

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_104_0.png)

FIGURE 4.2 Original and sorted sequence of random numbers, as returned by routine InsertSort and indexed by routine Index.

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_104_1.png)

FIGURE 4.3 Comparison of operation counts for random sequences (compares and compares+swaps) for bubble sort, insert sort, and Quicksort.

## References and Suggested Further Reading

Hoare, C. A. R. 1961. Algorithm 64: Quicksort. Communications of the ACM 4(7), 321.
Knuth, D. E. 1998. The Art of Computer Programming (2nd ed.), vol. 3: Sorting and Searching. Reading, MA: Addison-Wesley Professional.
Press, W. H., S. A. Teukolsky, W. T. Vetterling, and B. P. Flannery. 2007. Numerical Recipes (3rd ed.): The Art of Scientific Computing. Cambridge: Cambridge University Press.
Sedgewick, R. 1978. Implementing Quicksort programs. Communications of the ACM 21(10), 847–857.

## Evaluation of Functions

函数求值在数值编程中几乎无处不在，其*准确性*和*效率*在很大程度上决定了计算机代码的整体性能。对于单个求值而言，预定义精度通常已是充分要求，而对于大规模计算，效率可能决定计算是否可行。尽管有时相同的技术可能同时有益于两个方面，但准确性和效率通常是通过不同的方法实现的。

计算所表达和编码的具体形式至关重要，因为由于纯粹的数值现象，完全等价的数学公式可能导致截然不同的结果，或者再次导致相似的结果，但所需时间却相差甚远。事实上，由于数字的有限机器表示（见第 1 章讨论），鉴于不可避免地有限的可行算法步骤数量，数值计算本质上是近似的。从这个角度来看，不经深入分析可能存在的冗余和误差传播而直接对数学公式进行编程，很少是首选方法。恰恰相反，具有良好数学基础的公式，避免了易出错且耗时的运算，有利于实现准确和高效的编程。下一节揭示了常见函数求值方法的陷阱并提供了补救措施。

### 5.1 Evaluation of Polynomials by Horner’s Scheme

多项式是数值应用中最常求值的函数之一。由于其概念上的明显简单性，它们却容易因过度使用内置幂函数而导致低效编码，而幂函数已知耗时。将幂表示为重复乘法可能会略微提高效率，但缺乏优雅性和通用性。

正是霍纳方案使得多项式能够从单项式形式（单项式的线性组合）转换为计算高效的形式，仅涉及基本算术运算。

具有实系数的 n 次多项式

$$P(x)=\sum_{i=0}^{n}a_i x^{n-i}=a_0x^n+a_1x^{n-1}+\cdots+a_{n-1}x+a_n,$$  (5.1)

可通过逐步提出自变量 x 重写为

$$P(x)=((\cdots((a_0x+a_1)x+a_2)x+\cdots+a_{n-1})x+a_n).$$

基于此因子化形式，多项式在特定自变量 x 处的求值在霍纳方案中简化为数 p_i 的递归计算：

\begin{cases} p_0 = a_0, \\ p_i = p_{i-1}x + a_i, \quad i = 1,2,\dots,n \end{cases} \tag{5.2}

其中最后一个表示所求的多项式值：

P(x) = p_n. \tag{5.3}

霍纳方案说明了简单算法公式与使用仅基本运算获得的效率的良好结合。它不仅减少了必要的乘法次数，而且还导致数值不稳定性更小，而这种不稳定性否则可能由涉及量级相当的大单项式的减法引起。

可以证明，对于特定 x = x_0，数 p_0, p_1, …, p_{n-1} 是将 P(x) 除以二项式 (x − x_0) 进行综合除法时商多项式 Q(x) 的系数，其中 p_n 是相应的余数且 P(x_0) = p_n，即

P(x) = (x − x_0)Q(x) + p_n, \tag{5.4}

Q(x) = p_0 x^{n-1} + … + p_i x^{n-i-1} + … + p_{n-1}. \tag{5.5}

事实上，将公式 5.5 代入公式 5.4，可得到：

P(x) = p_0 x^n + … + (p_i − p_{i-1} x_0) x^{n-i} + … + (p_n − p_{n-1} x_0).

将系数与公式 5.1 中的 P(x) 的系数进行识别可得到递推式

\begin{cases} a_0 = p_0, \\ a_i = p_i − p_{i-1} x, \quad i = 1,2,\dots,n \end{cases} \tag{5.6}

这显然等价于公式 5.2 并证明了该陈述。因此，公式 5.2 对于 x = x_0 给出了多项式 P(x) 除以二项式 (x − x_0) 的除法商多项式 Q(x) 的系数。

多项式的导数可从

P'(x) = \sum_{i=0}^{n-1} (n − i) a_i x^{n-i-1} \tag{5.7}

同样基于霍纳方案计算，可单独计算，或与多项式 P(x) 本身的求值并行计算。

任意有理分式 R(x) 可表示为两个多项式的分式，

R(x) = \frac{P(x)}{Q(x)}, \tag{5.8}

其中 P(x) 和 Q(x) 可分别使用霍纳方案计算。或者，多项式分式可转换为连分式，其求值方法在第 5.3 节中描述。

