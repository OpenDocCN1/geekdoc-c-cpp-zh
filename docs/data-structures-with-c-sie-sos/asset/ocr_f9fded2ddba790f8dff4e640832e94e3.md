# Little Oh Notation (o)

# Definition

f(n) = o(g(n))(read as f of n is little oh of g of n) iff f(n) = O(g(n)) and f(n) ≠ Ω(g(n)).

For f(n) = 18n + 9, we have f(n) = O(n²) but f(n) ≠ Ω(n²). Hence f(n) = o(n²). However, f(n) ≠ o(n).

# 2.7 SUBALGORITHMS

A subalgorithm is a complete and independently defined algorithmic module which is used (or invoked or called) by some main algorithm or by some other subalgorithm. A subalgorithm receives values, called arguments, from an originating (calling) algorithm; performs computations; and then sends back the result to the calling algorithm. The subalgorithm is defined independently so that it may be called by many different algorithms or called at different times in the same algorithm. The relationship between an algorithm and a subalgorithm is similar to the relationship between a main program and a subprogram in a programming language.

The main difference between the format of a subalgorithm and that of an algorithm is that the subalgorithm will usually have a heading of the form

```
NAME(PAR₁, PAR₂, ..., PARₖ)
```

Here NAME refers to the name of the subalgorithm which is used when the subalgorithm is called, and PAR₁, PAR₂, ..., PARₖ refer to parameters which are used to transmit data between the sub algorithm and the calling algorithm.

Another difference is that the subalgorithm will have a Return statement rather than an Exit statement; this emphasizes that control is transferred back to the calling program when the execution of the subalgorithm is completed.

Subalgorithms fall into two basic categories: function subalgorithms and procedure subalgorithms. The similarities and differences between these two types of subalgorithms will be examined below by means of examples. One major difference between the subalgorithms is that the function subalgorithm returns only a single value to the calling algorithm, whereas the procedure subalgorithm may send back more than one value.

# Example 2.9

The following function subalgorithm MEAN finds the average AVE of three numbers A, B and C.

```
Function 2.5: MEAN(A, B, C)
1. Set AVE := (A + B + C)/3.
2. Return(AVE).
```

Note that MEAN is the name of the subalgorithm and A, B and C are the parameters. The Return statement includes, in parentheses, the variable AVE, whose value is returned to the calling program.

The subalgorithm MEAN is invoked by an algorithm in the same way as a function subprogram is invoked by a calling program. For example, suppose an algorithm contains the statement

```
Set TEST := MEAN(T₁, T₂, T₃)
```

where T₁, T₂ and T₃ are test scores. The argument values T₁, T₂ and T₃ are transferred to the parameters A, B, C in the subalgorithm, the subalgorithm MEAN is executed, and then the value of AVE is returned to the program and replaces MEAN(T₁, T₂, T₃) in the statement. Hence the average of T₁, T₂ and T₃ is assigned to TEST.