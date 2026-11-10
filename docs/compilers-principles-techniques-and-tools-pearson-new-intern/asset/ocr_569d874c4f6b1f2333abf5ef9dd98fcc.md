```
return new Access(y, rvalue(z));
```

is reached with y being the node for a and z being the node for expression 2*k. The call rvalue(z) generates code for the expression 2*k (i.e., the three-address statement t = 2 * k) and returns the new node z′ representing the temporary name t. That node z′ becomes the value of the second field in the new Access node x′ that is created.

```
Expr rvalue(x : Expr) {
    if (x is an Id or a Constant node) return x;
    else if (x is an Op(op, y, z) or a Rel(op, y, z) node) {
        t = new temporary;
        emit string for t = rvalue(y) op rvalue(z);
        return a new node for t;
    }
    else if (x is an Access(y, z) node) {
        t = new temporary;
        call lvalue(x), which returns Access(y, z′);
        emit string for t = Access(y, z′);
        return a new node for t;
    }
    else if (x is an Assign(y, z) node) {
        z′ = rvalue(z);
        emit string for lvalue(y) = z′;
        return z′;
    }
}
```

Figure 2.45: Pseudocode for function rvalue

Function rvalue in Fig. 2.45 generates instructions and returns a possibly new node. When x represents an identifier or a constant, rvalue returns x itself. In all other cases, it returns an Id node for a new temporary t. The cases are as follows:

+   - When x represents y op z, the code first computes y′ = rvalue(y) and z′ = rvalue(z). It creates a new temporary t and generates an instruction t = y′ op z′ (more precisely, an instruction formed from the string representations of t, y′, op, and z′). It returns a node for identifier t.
+   - When x represents an array access y[z], we can reuse function lvalue. The call lvalue(x) returns an access y[z′], where z′ represents an identifier holding the offset for the array access. The code creates a new temporary t, generates an instruction based on t = y[z′], and returns a node for t.