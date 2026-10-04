# CHAPTER 5. PATH CONDITIONS

```
1 a = u();
2 while (n>0) {
3 x = v();
4 if (x>0) {
5 b = a;
6 else
7 c = b;
8 }
9 z = c;
```

![](bbox=[0.403, 0.127, 0.597, 0.27])

Figure 5.1: A small program and its dependence graph

Both extensions have been implemented in a prototype tool based on the Valsoft architecture [HOb05]. Previous results from this effort have been described in [HGK06, HS08].

# 5.2 Foundations of Path Conditions

Program dependence graphs (PDG) as presented in chapter 2 are a standard tool to model information flow through a program. Program statements or conditions are represented by nodes, the edges represent data and control dependences between statements or conditions. A path x→y means that information can flow from x to y; if there is no path, it is guaranteed that there is no information flow. In particular, all statements (possibly) influencing (the so-called backward slice) are easily computed as BS(y) = {x | x→y}.

For the small program and its dependence graph in Figure 5.1, there is a path from statement 1 to statement 9, indicating that input variable a may influence output variable z. Since there is no path 1→4, there is definitely no influence from a to x.

+   A chop for a chopping criterion (x,y) is the set of nodes that are part of the influence of the (source) node x on the (target) node y. The nodes that lie on a path from x to y in the PDG: CH(x,y) = {z | x→z→y}. For convenience, we use CH(x,y) for the set of paths between x and y.

# 5.2.1 Intraproural Path Conditions

In order to make program slicing more precise, Seltening path conditions [Sne96], which are necessary conditions for information flow between two nodes. The formula for the generation of path conditions are complex formulae (for details, see [SRK06]), and only the most fundamental formulae will be given here:

```
PC(x,y) = ∧_{Path=x→y z∈P} E(z) where E(z) = ∧_{Control Path Start→cd*z ν∈P} c(ν→μ) (5.1)
```