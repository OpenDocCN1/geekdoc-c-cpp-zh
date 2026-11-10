
## 9.2 Introduction to Data-Flow Analysis

All the optimizations introduced in Section 9.1 depend on *data-flow analysis*. “Data-flow analysis” refers to a body of techniques that derive information about the flow of data along program execution paths. For example, one way to implement global common subexpression elimination requires us to determine whether two textually identical expressions evaluate to the same value along any possible execution path of the program. As another example, if the result of an assignment is not used along any subsequent execution path, then we can eliminate the assignment as dead code. These and many other important questions can be answered by data-flow analysis.

### 9.2.1 The Data-Flow Abstraction

Following Section 1.6.2, the execution of a program can be viewed as a series of transformations of the program state, which consists of the values of all the variables in the program, including those associated with stack frames below the top of the run-time stack. Each execution of an intermediate-code statement transforms an input state to a new output state. The input state is associated with the *program point before* the statement and the output state is associated with the *program point after* the statement.

When we analyze the behavior of a program, we must consider all the possible sequences of program points (“paths”) through a flow graph that the program execution can take. We then extract, from the possible program states at each point, the information we need for the particular data-flow analysis problem we want to solve. In more complex analyses, we must consider paths that jump among the flow graphs for various procedures, as calls and returns are executed. However, to begin our study, we shall concentrate on the paths through a single flow graph for a single procedure.

Let us see what the flow graph tells us about the possible execution paths.

- Within one basic block, the program point after a statement is the same as the program point before the next statement.
- If there is an edge from block $B_1$ to block $B_2$, then the program point after the last statement of $B_1$ may be followed immediately by the program point before the first statement of $B_2$.

Thus, we may define an *execution path* (or just *path*) from point $p_1$ to point $p_n$ to be a sequence of points $p_1, p_2, \ldots, p_n$ such that for each $i = 1, 2, \ldots, n - 1$, either

1. $p_i$ is the point immediately preceding a statement and $p_{i+1}$ is the point immediately following that same statement, or
2. $p_i$ is the end of some block and $p_{i+1}$ is the beginning of a successor block.

In general, there is an infinite number of possible execution paths through a program, and there is no finite upper bound on the length of an execution path. Program analyses summarize all the possible program states that can occur at a point in the program with a finite set of facts. Different analyses may choose to abstract out different information, and in general, no analysis is necessarily a perfect representation of the state.

**Example 9.8:** Even the simple program in Fig. 9.12 describes an unbounded number of execution paths. Not entering the loop at all, the shortest complete execution path consists of the program points (1, 2, 3, 4, 9). The next shortest path executes one iteration of the loop and consists of the points (1, 2, 3, 4, 5, 6, 7, 8, 3, 4, 9). We know that, for example, the first time program point (5) is executed, the value of *a* is 1 due to definition $d_1$. We say that $d_1$ reaches point (5) in the first iteration. In subsequent iterations, $d_3$ reaches point (5) and the value of *a* is 243.

![](img/a29d16e454785bb105e96ef448ac07f6_602_0.png)

*Figure 9.12: Example program illustrating the data-flow abstraction*

In general, it is not possible to keep track of all the program states for all possible paths. In data-flow analysis, we do not distinguish among the paths taken to reach a program point. Moreover, we do not keep track of entire states; rather, we abstract out certain details, keeping only the data we need for the purpose of the analysis. Two examples will illustrate how the same program states may lead to different information abstracted at a point.

1. To help users debug their programs, we may wish to find out what are all the values a variable may have at a program point, and where these values may be defined. For instance, we may summarize all the program states at point (5) by saying that the value of *a* is one of {1, 243}, and that it may be defined by one of $\{d_1, d_3\}$. The definitions that may reach a program point along some path are known as *reaching definitions*.

2. Suppose, instead, we are interested in implementing constant folding. If a use of the variable *x* is reached by only one definition, and that definition assigns a constant to *x*, then we can simply replace *x* by the constant. If, on the other hand, several definitions of *x* may reach a single program point, then we cannot perform constant folding on *x*. Thus, for constant folding we wish to find those definitions that are the unique definition of their variable to reach a given program point, no matter which execution path is taken. For point (5) of Fig. 9.12, there is no definition that *must* be the definition of *a* at that point, so this set is empty for *a* at point (5). Even if a variable has a unique definition at a point, that definition must assign a constant to the variable. Thus, we may simply describe certain variables as “not a constant,” instead of collecting all their possible values or all their possible definitions.

Thus, we see that the same information may be summarized differently, depending on the purpose of the analysis. □

### 9.2.2 The Data-Flow Analysis Schema

In each application of data-flow analysis, we associate with every program point a *data-flow value* that represents an abstraction of the set of all possible program states that can be observed for that point. The set of possible data-flow values is the *domain* for this application. For example, the domain of data-flow values for reaching definitions is the set of all subsets of definitions in the program. A particular data-flow value is a set of definitions, and we want to associate with each point in the program the exact set of definitions that can reach that point. As discussed above, the choice of abstraction depends on the goal of the analysis; to be efficient, we only keep track of information that is relevant.

We denote the data-flow values before and after each statement *s* by $IN[s]$ and $OUT[s]$, respectively. The *data-flow problem* is to find a solution to a set of constraints on the $IN[s]$'s and $OUT[s]$'s, for all statements *s*. There are two sets of constraints: those based on the semantics of the statements (“transfer functions”) and those based on the flow of control.

#### Transfer Functions

The data-flow values before and after a statement are constrained by the semantics of the statement. For example, suppose our data-flow analysis involves determining the constant values of variables at points. If variable *a* has value *v* before executing statement *b = a*, then both *a* and *b* will have the value *v* after the statement. This relationship between the data-flow values before and after the assignment statement is known as a *transfer function*.

Transfer functions come in two flavors: information may propagate forward along execution paths, or it may flow backwards up the execution paths. In a forward-flow problem, the transfer function of a statement *s*, which we shall usually denote $f_s$, takes the data-flow value before the statement and produces a new data-flow value after the statement. That is,

$$OUT[s] = f_s(IN[s]).$$

Conversely, in a backward-flow problem, the transfer function $f_s$ for statement *s* converts a data-flow value after the statement to a new data-flow value before the statement. That is,

$$IN[s] = f_s(OUT[s]).$$

#### Control-Flow Constraints

The second set of constraints on data-flow values is derived from the flow of control. Within a basic block, control flow is simple. If a block $B$ consists of statements $s_1, s_2, \ldots, s_n$ in that order, then the data-flow value out of $s_i$ is the same as the data-flow value into $s_{i+1}$. That is,

$IN[s_{i+1}] = OUT[s_i]$, for all $i = 1, 2, \ldots, n - 1$.

However, control-flow edges between basic blocks create more complex constraints between the last statement of one basic block and the first statement of the following block. For example, if we are interested in collecting all the definitions that may reach a program point, then the set of definitions reaching the leader statement of a basic block is the union of the definitions after the last statements of each of the predecessor blocks. The next section gives the details of how data flows among the blocks.

### 9.2.3 Data-Flow Schemas on Basic Blocks

While a data-flow schema technically involves data-flow values at each point in the program, we can save time and space by recognizing that what goes on inside a block is usually quite simple. Control flows from the beginning to the end of the block, without interruption or branching. Thus, we can restate the schema in terms of data-flow values entering and leaving the blocks. We denote the data-flow values immediately before and immediately after each basic block $B$ by $IN[B]$ and $OUT[B]$, respectively. The constraints involving $IN[B]$ and $OUT[B]$ can be derived from those involving $IN[s]$ and $OUT[s]$ for the various statements $s$ in $B$ as follows.

Suppose block $B$ consists of statements $s_1, \ldots, s_n$, in that order. If $s_1$ is the first statement of basic block $B$, then $IN[B] = IN[s_1]$. Similarly, if $s_n$ is the last statement of basic block $B$, then $OUT[B] = OUT[s_n]$. The transfer function of a basic block $B$, which we denote $f_B$, can be derived by composing the transfer functions of the statements in the block. That is, let $f_{s_i}$ be the transfer function of statement $s_i$. Then $f_B = f_{s_n} \circ \cdots \circ f_{s_2} \circ f_{s_1}$. The relationship between the beginning and end of the block is

$$OUT[B] = f_B(IN[B]).$$
