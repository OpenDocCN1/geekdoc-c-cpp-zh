# ### 6.3. TYPES AND DECLARATIONS

```
    T → B        { t = B.type; w = B.width; }
        C        { T.type = C.type; T.width = C.width; }
    B → int      { B.type = integer; B.width = 4; }
    B → float    { B.type = float; B.width = 8; }
    C → ε        { C.type = t; C.width = w; }
    C → [ num ] C_1  { C.type = array(num.value, C_1.type);
                       C.width = num.value × C_1.width; }
```

Figure 6.15: Computing types and their widths

The width of an array is obtained by multiplying the width of an element by the number of elements in the array. If addresses of consecutive integers differ by 4, then address calculations for an array of integers will include multiplications by 4. Such multiplications provide opportunities for optimization, so it is helpful for the front end to make them explicit. In this chapter, we ignore other machine dependencies such as the alignment of data objects on word boundaries.

**Example 6.9:** The parse tree for the type int[2][3] is shown by dotted lines in Fig. 6.16. The solid lines show how the type and width are passed from B, down the chain of C's through variables t and w, and then back up the chain as synthesized attributes type and width. The variables t and w are assigned the values of B.type and B.width, respectively, before the subtree with the C nodes is examined. The values of t and w are used at the node for C → ε to start the evaluation of the synthesized attributes up the chain of C nodes. □

![](bbox=[0.25, 0.61, 0.77, 0.79])

Figure 6.16: Syntax-directed translation of array types