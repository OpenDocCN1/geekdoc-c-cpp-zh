number of kinds of resources in the machine, and its length is the duration over which resources are used by the operation. Entry $RT[i,j]$ is the number of units of the $j$th resource used by an operation of type $i$, it clocks after it is issued. For notational simplicity, we assume $RT[i,j] = 0$ if it refers to a nonexistent entry in the table (i.e., $i$ is greater than the number of clocks it takes to execute the operation). Of course, for any $t$, $i$, and $j$, $RT[t,i,j]$ must be less than or equal to $R[j]$, the number of resources of type $j$ that the machine has.

Typical machine operations occupy only one unit of resource at the time an operation is issued. Some operations may use more than one functional unit. For example, a multiply-and-add operation may use a multiplier in the first clock and an adder in the second. Some operations, such as a divide, may need to occupy a resource for several clocks. *Fully pipelined* operations are those that can be issued every clock, even though their results are not available until some number of clocks later. We need not model the resources of every stage of a pipeline explicitly; one single unit to represent the first stage will do. Any operation occupying the first stage of a pipeline is guaranteed the right to proceed to subsequent stages in subsequent clocks.

+   1) $a = b$  
+   2) $c = d$  
+   3) $b = c$  
+   4) $d = a$  
+   5) $c = d$  
+   6) $a = b$

Figure 10.5: A sequence of assignments exhibiting data dependences

# 10.2.8  Exercises for Section 10.2

**Exercise 10.2.1:** The assignments in Fig. 10.5 have certain dependences. For each of the following pairs of statements, classify the dependence as (i) true dependence, (ii) antidependence, (iii) output dependence, or (iv) no dependence (i.e., the instructions can appear in either order):

+   a) Statements (1) and (4).  
+   b) Statements (3) and (5).  
+   c) Statements (1) and (6).  
+   d) Statements (3) and (6).  
+   e) Statements (4) and (6).

**Exercise 10.2.2:** Evaluate the expression $((u+v)+(w+x))+(y+z)$ exactly as parenthesized (i.e., do not use the commutative or associative laws to reorder the