+   3. If INFO[PTR] = ITEM, then:
+      Set LOC := PTR and LOCP := SAVE.
+      Else:
+      Set LOC := NULL and LOCP := SAVE.
+      [End of If structure.]
+   4. Exit.

Observe the simplicity of this procedure compared with Procedure 5.9. Here we did not have to consider the special case when ITEM appears in the first node, and here we can perform at the same time the two tests which control the loop.

+   (c) Algorithm 5.10 deletes the first node N which contains ITEM when LIST is an ordinary linked list. The following is such an algorithm when LIST is a circular header list.

```
Algorithm 5.14: DELLOCHL(INFO, LINK, START, AVAIL, ITEM)
1. [Use Procedure 5.15 to find the location of N and its preceding node.]
   Call FINDBHL(INFO, LINK, START, ITEM, LOC, LOCP).
2. If LOC = NULL, then: Write: ITEM not in list, and Exit.
3. Set LINK[LOCP] := LINK[LOC]. [Deletes node.]
4. [Return deleted node to the AVAIL list.]
   Set LINK[LOC]:= AVAIL and AVAIL:= LOC.
5. Exit.
```

Again we did not have to consider the special case when ITEM appears in the first node, as we did in Algorithm 5.10.

Remark: There are two other variations of linked lists which sometimes appear in the literature:

+   1. A linked list whose last node points back to the first node instead of containing the null pointer, called a circular list
+   2. A linked list which contains both a special header node at the beginning of the list and a special trailer node at the end of the list

Figure 5.32 contains schematic diagrams of these lists.

![](bbox=[0.16, 0.65, 0.8, 0.75])

![](bbox=[0.16, 0.78, 0.78, 0.87])

Fig. 5.32