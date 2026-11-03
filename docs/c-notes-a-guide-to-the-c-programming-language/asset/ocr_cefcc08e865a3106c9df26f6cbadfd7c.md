# 2. INITIALIZERS 39

Here cmat has been declared as a variable of type structure with parts matrix and tag. Hence, its initializer has the general form

```
```
{ initializer-for-matrix , char-constant }
```
```

Since matrix is of type array of COMPLEX, its initializer has the form

```
```
{ initializer-for-row-0 ,
 initializer-for-row-1
}
```
```

and so on. Finally, each initializer for a COMPLEX structure has the form

```
```
{ initializer-for-real-part , initializer-for-imag-part }
```
```

and so on the complete initializer for cmat emerges from a sequence of stepwise refinements. Note that the first element of the first row of cmat.matrix has not been explicitly initialized. In the case of external declarations, it would be {0.0, 0.0} by default.

If an initializer is specified for a union, it must correspond to the first of the declared parts. Neither unions nor structures may be initialized in automatic declarations.

# 2.6 Function definitions

A function definition looks somewhat like a data declaration that is initialized — therefore, its discussion in this section. Indeed, the arguments and function body constitute the value associated with a function name, so they do play a role similar to initializer, except that function names represent constant (unchangeable) values, not variables. Variables of type pointer to function may change their allegiance but functions may not!