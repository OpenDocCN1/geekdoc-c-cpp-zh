# 3: EXPRESSIONS

> > The result we proceed to divide, as you see,
> > By Nine Hundred and Ninety and Two:
> > Then subtract Seventeen, and the answer must be
> > Exactly and perfectly true.
> >
> > — Lewis Carroll, Hunting of the Snark

# 3.0 Introduction

The expressions of C actually carry out the work (change of state of variables) of the program. In particular, a simple assignment replaces the current value of some variable by a newly calculated value and has the syntax

```
variable-name-expr = expr
```

The variable-name-exprs range in degree of complexity from simple identifiers of integer variables to complicated name expressions like

```
pcm -> matrix[1][k].imag
```

which identifies the imag part of the complex member at row 1 and column k of the matrix part of the structure pointed at by pointer variable pcm. The remainder of this chapter will explain such expressions.

The expressions themselves are a wider class allowing many different operators to be combined with variable-name-exprs and constants and so provide the computational power of the