# CHAPTER 4. INFORMATION FLOW CONTROL

![](bbox=[0.263, 0.116, 0.736, 0.3])

As another example consider Figure 4.11. In line 3 a declassification : confidential $ightarrow$ public is present. Here $3 \in D, R(3) = confidential$ and $P(3) = public$. It means that a *secret* value can flow from line 10 to line 3, hence in line 3 an illegal flow seems possible $(R(3) 
eq S(3))$ because we can declassify from confidential to public but not from *secret* to public. In fact the return value in line 3 is only copied to x1 at line 10, and x1 is (never used afterwards and never output). Thus intuitively, the program seems.

The SDG for this program is shown in Figure 4.12. By Algorithm 7 x1 is not in the context-sensitive backward slice for line 12, and thus the SDG-based confidentiality criterion will not generate a false alarm, but determine that confidentiality is guaranteed. This example demonstrates once more how context-sensitive backward slices improve precision.

# 4.8 Improving Intercedural Declassification

Algorithm 7 is correct, but in the presence of declassifications, its precision still needs to be improved. The reason is that Algorithm 7 essentially ignores the effect of declassifications in called procedures; summary edges represent a transitive information flow between pairs of parameters, whereas declassification is intransitive. Using them for computation of the actual security level $S(l)$ implies that every piece of information flowing into a procedure with a given security level $l$ will be treated as if flowed back out with the same level. This approach is overly conservative and leads to many false alarms.

As an example, consider Figure 4.12: The required security level for node 11 is Low as Algorithm 7 computes $S(2) = S(8) = S(10) = S(11) = Low$ due to the summary edge. This will result in a false alarm because the declassification at node 15 is ignored.

# 4.8.1 Summary Declassification Nodes

In order to respect declassifications in called procedures, and achieve maximal precision, an extension of the notion of a summary edge is needed. The funda-