# 2.2. PROGRAM SLICING

```
main() {
  a=3;
  b=4;
  v=add(a,b);
  w=add(v,b);
}
add(x,y) {
  return x+y;
}
```

![](bbox=[0.386, 0.126, 0.758, 0.365])

Figure 2.5: Interprocedural example with system program graph

the context, if PDG represents only a procedure or a whole program. At each call site, the PDG contains an actual-node per parameter of invoked procedure, modeling the assignments of the parameters to temporary variables (this assignment is supposed to take place before the actual call). The called procedure's PDG holds, in analogy, a formal-node for each formal parameter, representing the assignment of the temporary variable to the formal parameter. The edge of the procedure operates this schema is applied: the return parameters are copied to temporary variables in formal-out nodes, and after returning to the caller, those are copied back to the variables receiving the values in actual-out nodes. Globally visible variables (e.g. static variables in Java) receive special treatment: they are handled like additional read-write parameters of that procedure [HRB90] and are ignored in the subsequent discussions.

The SDG consists of all the PDGs involved in the program connected by interprocedural edges, which are inserted in accordance to the invocation edges of the call graph. An actual parameter node is connected to its corresponding formal-node with an parameter-in edge (pi), formal-out nodes to their actual-out nodes with an parameter-out edge (po). Finally, the node representing a call-site is connected to the entry node of the callee with a call edge (cl).

As an example, consider Figure 2.5, which shows an example program and the corresponding SDG. The straight edges in blue represent dependence, the curved edges in green data dependence. Interprocedural edges are shown as dashed edges. The call edges from nodes 4 and 5 to the entry of procedure add, parameter-in edges from variables a and v to x, parameter-out edges from the return statement in node 8 to the variables v and w.

While this representation does allow program slicing, the slice according to equation 2.1 is correct but not context-sensitive due to the calling-context