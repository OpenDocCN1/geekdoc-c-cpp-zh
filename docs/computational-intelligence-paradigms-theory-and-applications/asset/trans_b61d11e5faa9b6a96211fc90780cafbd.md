
**具有相同父代的交叉操作**

**父代**

![](img/d9a4cc12c48f7466f309cbd3c4549c73_633_0.png)

**子代**

![](img/d9a4cc12c48f7466f309cbd3c4549c73_633_1.png)

**图 14.5：** *（续）* 可以产生不同的后代，而在遗传算法中，相同的父代会生成相同的后代。加粗的选择表示被交换的子树。

### 14.4.9 用于交叉的 MATLAB 例程

```matlab
function [tree1,tree2] = recombinate_trees(treein1,treein2, mode, symbols)
% Recombines two trees
% [tree1,tree2] = recombinate_trees(treein1,treein2, mode, symbols)
% tree1,tree2 <- two childs
% treein1,treein2 -> two parents
% mode -> 1: one-point- 2: two-point crossover
% symbols -> cell arrays of operator and terminator node strings
%
% Begin
tree1 = treein1;
tree2 = treein2;
nn = [length(symbols1), length(symbols2)];
% Calculate indexes
switch mode,
  case 1,
    [n,v1] = tree.size(tree1);
    [n,v2] = tree.size(tree2);
    n = max([tree1.maxsize, tree2.maxsize]);
    dummy1 = zeros(n,1);
    dummy2 = zeros(n,1);
    dummy1(v1) = 1;
    dummy2(v2) = 1;
    v = find((dummy1+dummy2)==2);
    ix1 = v(floor(rand*(length(v))+1));
    ix2 = ix1;
  case 2,
    [n,v] = tree.size(tree1);
    ix1 = v(floor(rand*(length(v))+1));
    [n,v] = tree.size(tree2);
    ix2 = v(floor(rand*(length(v))+1));
  otherwise,
    return;
end
% Replace subtrees (recombinate)
sub1 = tree.getsubtree(treein1,ix1);
sub2 = tree.getsubtree(treein2,ix2);
tree1 = tree.inserttree(sub2,tree1,ix1,nn(2));
tree2 = tree.inserttree(sub1,tree2,ix2,nn(2));
```

### 14.4.10 变异操作

在遗传编程中，变异有两种可能的方式。在第一种技术中，函数始终替换函数，终结符只替换终结符。而在第二种技术中，整个子树可以替换另一个子树。图 14.6 解释了变异的概念：

**变异操作**

*原始个体*

![](img/d9a4cc12c48f7466f309cbd3c4549c73_636_0.png)

*变异个体*

![](img/d9a4cc12c48f7466f309cbd3c4549c73_636_1.png)

**图 14.6：** 变异操作

### 14.4.11 用于变异的 MATLAB 例程

```matlab
function tree = tree_mutate(treein,symbols);
% Mutates a tree (mutates one randomly selected node)
% tree = tree_mutate(treein,symbols)
% tree <- the output tree
% treein -> the input tree
% symbols -> cell arrays of operator and terminator node strings
%
% Begin
tree = treein;
nn = [length(symbols1), length(symbols2)];
% Mutate one node
[n,v] = tree.size(tree);
i = v(floor(rand*length(v))+1);
if i<(tree.maxsize+1)/2 & rand<0.5,
    [tree.nodetyp(i) tree.node(i)] = tree.genrndsymb((tree.nodetyp(i)==1),nn);
else
    while tree.node(i)==treein.node(i) & tree.nodetyp(i)==treein.nodetyp(i),
        [tree.nodetyp(i) tree.node(i)] = tree.genrndsymb((tree.nodetyp(i)==1),nn);
    end
end
%------------------------------------------------------------
function [nodetyp,node] = tree.genrndsymb(p0,nn)
% Generate a random symbol (terminate or operate)
% [nodetyp,node] = tree.genrndsymb(p0,nn)
% nodetyp,node <- results
% p0 -> probability of terminate node
% nn -> vector [number of operators, variables]
%
if rand<p0,
    nodetyp = 2;
else
    nodetyp = 1;
end
node = floor(nn(nodetyp)*rand)+1;
```

## 14.5 机器学习中的遗传编程

在人工智能、机器学习或符号处理等若干领域中，许多问题的求解可以被视为：在能够根据输入产生一些期望输出的可行程序空间中，搜索一个计算机程序。这种搜索的执行方式应使所搜索到的程序对所考虑的问题尽可能有能力。遗传编程（GP）范式为实现这类搜索提供了合适框架，能够以高效且灵活的方式实现，因为它可以适应任何问题类型。

遗传编程范式基于适者生存原则（C. Darwin）。它从随机生成的初始种群开始，采用这一原则获得种群。新个体是当前种群中较优个体经过遗传操作产生的。与遗传算法（GA）相联系，GP 贡献了启发式和随机性的哲学与特性。

在机器学习领域中，各种范式都集中于解决问题。每种范式所应用的结构各不相同。

### 连接主义模型

在这里，信号的值会以称为权重的强度被放大或缩小，权重为实数值。问题的解由一组实值权重给出。

应用领域：神经网络

### 进化模型

在该模型中，解是定长字符串。每条染色体表示问题的一个可能解。应用传统遗传算法，在所有可能解中获得最优解（或足够好的解）。

应用领域：遗传算法

### 归纳模型

根据该范式，某个问题的解由决策树给出。每棵决策树都将问题的每个实例分类到若干类别中，对于这些类别存在一个可能的解。

应用领域：分类器系统

上述所有模型在解决某一问题类型时可能或多或少有效。用于确定一种方法效率的途径，首先是其适应多种问题类型的灵活性，其次是其以自然且用户可理解的方式表示该问题解的容易程度。计算机程序提供了灵活性：

- 使用不同类型的变量执行操作。
- 执行以中间点所得结果为条件的操作。
- 执行迭代和递归。
- 定义以后可以使用的例程。

解的灵活性包括解在大小、形式和结构复杂度方面的灵活性概念。用户应避免对结果的大小或形式表达任何解释或预先设定。GP 的真正能力在于其适应问题类型的能力，因此关于结果大小、复杂度或形式的条件应在其自身求解过程中产生。解表示的重要性在于：遗传算法直接保持表示的结构，而不是保持其自身的解。

字符串表示不能直接提供程序的层次数据结构。同样，个体形式、大小和复杂度的适应也变得非常困难。因此，GP 已扩展到更复杂的表示，以提供必要的灵活性。

GP 使用类似于个体的程序，但不同观点会随着其实现而出现。Cramer 使用类似解析树的代码表示，并指定合适的操作（例如，为重组交换子树）。Fujiki 和 Dickinson 开发了一个系统，该系统基于生成使用 LISP 简单条件语句（COND）的程序。

许多问题的求解可以被建模为一个进化过程，其中适者生存。该进化过程的模拟从生成初始种群开始，初始种群由表示个体的计算机程序组成。这些程序从最适合待解决问题的函数和终结符元素集合开始生成。在大多数情况下，终结符和非终结符（函数）集合的选择对于使算法正常工作至关重要。

例如，为了呈现复杂的数学函数，在非终结符集合中引入正弦、余弦等函数是很有意义的。对于图形应用，通常很自然地引入 Line、Circle、Torus 等图元，以多种方式图形化地表示图形。

每个程序的适当性根据其在特定问题环境中的表现来量化。该度量称为适应度函数。程序通常在多个代表性案例中进行测量，其适应度的最终度量将是所有度量的平均值。通常，遗传算法的结果是在第 n 代生成的最佳个体，其中 n 是最大代数。

## 14.6 遗传编程的基本步骤

识别待解决的任务，并形成问题的高层描述。该描述是遗传编程系统的输入。为了将高层描述与 GP 系统对应起来，用户需要指定若干准备步骤。这些步骤是：

- (1) 为每个分支设置终结符集合（例如，问题的自变量、零参数函数和随机常数）

