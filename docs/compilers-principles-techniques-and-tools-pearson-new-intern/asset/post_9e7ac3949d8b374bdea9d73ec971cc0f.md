
## Are There Alternatives to Heuristics?

We can formulate the problem of simultaneously finding an optimal software pipeline schedule and register assignment as an integer-linear-programming problem. While many integer linear programs can be solved quickly, some of them can take an exorbitant amount of time. To use an integer-linear-programming solver in a compiler, we must be able to abort the procedure if it does not complete within some preset limit.

Such an approach has been tried on a target machine (the SGI R8000) empirically, and it was found that the solver could find the optimal solution for a large percentage of the programs in the experiment within a reasonable amount of time. It turned out that the schedules produced using a heuristic approach were also close to optimal. The results suggest that, at least for that machine, it does not make sense to use the integer-linear-programming approach, especially from a software engineering perspective. Because the integer-linear solver may not finish, it is still necessary to implement some kind of a heuristic scheduler in the compiler. Once such a heuristic scheduler is in place, there is little incentive to implement a scheduler based on integer programming techniques as well.

Different processors executing different iterations in a loop can have their own private copies and thus not interfere with one another.

*Variable expansion* refers to the transformation of converting a privatizable scalar variable into an array and having the *i*th iteration of the loop read and write the *i*th element. This transformation eliminates the antidependence constraints between reads in one iteration and writes in the subsequent iterations, as well as output dependences between writes from different iterations. If all loop-carried dependences can be eliminated, all the iterations in the loop can be executed in parallel.

Eliminating loop-carried dependences, and thus eliminating cycles in the data-dependence graph, can greatly improve the effectiveness of software pipelining. As illustrated by Example 10.15, we need not expand a privatizable variable fully by the number of iterations in the loop. Only a small number of iterations can be executing at a time, and privatizable variables may simultaneously be live in an even smaller number of iterations. The same storage can thus be reused to hold variables with nonoverlapping lifetimes. More specifically, if the lifetime of a register is *l* clocks, and the initiation interval is *T*, then only $q = \lceil l/T \rceil$ values can be live at any one point. We can allocate $q$ registers to the variable, with the variable in the *i*th iteration using the (*i* mod *q*)th register. We refer to this transformation as *modular variable expansion*.

**Algorithm 10.23:** Software pipelining with modular variable expansion.

**INPUT:** A data-dependence graph and a machine-resource description.

**OUTPUT:** Two loops, one software pipelined and one unpipelined.

**METHOD:**

- 1. Remove the loop-carried antidependences and output dependences associated with privatizable variables from the data-dependence graph.
- 2. Software-pipeline the resulting dependence graph using Algorithm 10.21. Let $T$ be the initiation interval for which a schedule is found, and $L$ be the length of the schedule for one iteration.
- 3. From the resulting schedule, compute $q_v$, the minimum number of registers needed by each privatizable variable $v$. Let $Q = \max_v q_v$.
- 4. Generate two loops: a software-pipelined loop and an unpipelined loop. The software-pipelined loop has

  $$\left\lceil\frac{L}{T}\right\rceil + Q - 1$$

  copies of the iterations, placed $T$ clocks apart. It has a prolog with

  $$\left(\left\lceil\frac{L}{T}\right\rceil - 1\right)T$$

  instructions, a steady state with $QT$ instructions, and an epilog of $L-T$ instructions. Insert a loop-back instruction that branches from the bottom of the steady state to the top of the steady state.

  The number of registers assigned to the privatizable variable $v$ is

  $$q'_v = \begin{cases} q_v & \text{if } Q \bmod q_v = 0 \\ Q & \text{otherwise} \end{cases}$$

  The variable $v$ in iteration $i$ uses the $(i \bmod q'_v)$th register assigned.

  Let $n$ be the variable representing the number of iterations in the source loop. The software-pipelined loop is executed if

  $$n \ge \left\lceil\frac{L}{T}\right\rceil + Q - 1.$$

  The number of times the loop-back branch is taken is

  $$n_1 = \left\lfloor\frac{n - \left\lceil\frac{L}{T}\right\rceil + 1}{Q}\right\rfloor.$$

  Thus, the number of source iterations executed by the software-pipelined loop is

  $$n_2 = \begin{cases} \left\lceil\frac{L}{T}\right\rceil - 1 + Qn_1 & \text{if } n \ge \left\lceil\frac{L}{T}\right\rceil + Q - 1 \\ 0 & \text{otherwise} \end{cases}$$

  The number of iterations executed by the unpipelined loop is $n_3 = n - n_2$.

## 10.5. SOFTWARE PIPELINING

**Example 10.24:** For the software-pipelined loop in Fig. 10.22, *L* = 8, *T* = 2, and *Q* = 2. The software-pipelined loop has 5 copies of the iterations, with the prolog, steady state, and epilog having 6, 4, and 6 instructions, respectively. Let *n* be the number of iterations in the source loop. The software-pipelined loop is executed if *n* ≥ 5, in which case the loop-back branch is taken

$$\left\lfloor\frac{n-3}{2}\right\rfloor$$

times, and the software-pipelined loop is responsible for

$$3 + 2 \times \left\lfloor\frac{n-3}{2}\right\rfloor$$

of the iterations in the source loop.

Modular expansion increases the size of the steady state by a factor of *Q*. Despite this increase, the code generated by Algorithm 10.23 is still fairly compact. In the worst case, the software-pipelined loop would take three times as many instructions as that of the schedule for the original loop. Roughly, together with the extra loop generated to handle the left-over iterations, the total code size is about four times the original. This technique is usually applied to tight inner loops, so this increase is reasonable.

Algorithm 10.23 minimizes code expansion at the expense of using more registers. We can reduce register usage by generating more code. We can use the minimum $q_v$ registers for each variable $v$ if we use a steady state with

$$T \times \operatorname{LCM}_{v} q_v$$

instructions. Here, $\operatorname{LCM}_v$ represents the operation of taking the *least common multiple* of all the $q_v$'s, as $v$ ranges over all the privatizable variables (i.e., the smallest integer that is an integer multiple of all the $q_v$'s). Unfortunately, the least common multiple can be quite large even for a few small $q_v$'s.

### 10.5.11 Conditional Statements

If predicated instructions are available, we can convert control-dependent instructions into predicated ones. Predicated instructions can be software-pipelined like any other operations. However, if there is a large amount of data-dependent control flow within the loop body, scheduling techniques described in Section 10.4 may be more appropriate.

If a machine does not have predicated instructions, we can use the concept of *hierarchical reduction*, described below, to handle a small amount of data-dependent control flow. Like Algorithm 10.11, in hierarchical reduction the control constructs in the loop are scheduled inside-out, starting with the most deeply nested structures. As each construct is scheduled, the entire construct is reduced to a single node representing all the scheduling constraints of its components with respect to the other parts of the program. This node can then be scheduled as if it were a simple node within the surrounding control construct. The scheduling process is complete when the entire program is reduced to a single node.

In the case of a conditional statement with “then” and “else” branches, we schedule each of the branches independently. Then:

- 1. The constraints of the entire conditional statement are conservatively taken to be the union of the constraints from both branches.
- 2. Its resource usage is the maximum of the resources used in each branch.
- 3. Its precedence constraints are the union of those in each branch, obtained by pretending that both branches are executed.

This node can then be scheduled like any other node. Two sets of code, corresponding to the two branches, are generated. Any code scheduled in parallel with the conditional statement is duplicated in both branches. If multiple conditional statements are overlapped, separate code must be generated for each combination of branches executed in parallel.

### 10.5.12 Hardware Support for Software Pipelining

Specialized hardware support has been proposed for minimizing the size of software-pipelined code. The rotating register file in the Itanium architecture is one such example. A rotating register file has a base register, which is added to the register number specified in the code to derive the actual register accessed. We can get different iterations in a loop to use different registers simply by changing the contents of the base register at the boundary of each iteration. The Itanium architecture also has extensive predicated instruction support. Not only can predication be used to convert control dependence to data dependence but it also can be used to avoid generating the prologs and epilogs. The body of a software-pipelined loop contains a superset of the instructions issued in the prolog and epilog. We can simply generate the code for the steady state and use predication appropriately to suppress the extra operations to get the effects of having a prolog and an epilog.

While Itanium’s hardware support improves the density of software-pipelined code, we must also realize that the support is not cheap. Since software pipelining is a technique intended for tight innermost loops, pipelined loops tend to be small anyway. Specialized support for software pipelining is warranted principally for machines that are intended to execute many software-pipelined loops and in situations where it is very important to minimize code size.
