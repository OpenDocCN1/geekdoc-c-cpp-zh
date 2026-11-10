Thus, an operation *n* in the *i*th iteration, counting from 0, is executed at clock *i* × *T* + *S*(*n*). Like all the other scheduling problems, software pipelining has two kinds of constraints: resources and data dependences. We discuss each kind in detail below.

# **Modular Resource Reservation**

Let a machine's resources be represented by R = [r₁, r₂, …], where rᵢ is the number of units of the *i*th kind of resource available. If an iteration of a loop requires nᵢ units of resource *i*, then the average initiation interval of a pipelined loop is at least maxᵢ(nᵢ/rᵢ) clock cycles. Software pipelining requires that the initiation intervals between any pair of iterations have a constant value. Thus, the initiation interval must have at least maxᵢ[nᵢ/rᵢ] clocks. If maxᵢ(nᵢ/rᵢ) is less than 1, it is useful to unroll the source code a small number of times.

**Example 10.17:** Let us return to our software-pipelined loop shown in Fig. 10.20. Recall that the target machine can issue one load, one arithmetic operation, one store, and one loop-back branch per clock. Since the loop has two loads, two arithmetic operations, and one store operation, the minimum initiation interval based on resource constraints is 2 clocks.

![](bbox=[0.235, 0.49, 0.776, 0.755])

Figure 10.24: Resource requirements of four consecutive iterations from the code in Example 10.13

Figure 10.24 shows the resource requirements of four consecutive iterations across time. More resources are used as more iterations get initiated, culmi-