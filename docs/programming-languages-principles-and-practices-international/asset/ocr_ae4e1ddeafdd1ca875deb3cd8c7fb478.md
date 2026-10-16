First, however, we want to describe a general form of conditional statement that encompasses all the various conditional constructs. This general form, known as the guarded if statement, was introduced by E. W. Dijkstra, and looks like this:

```
if B1 -> S1
| B2 -> S2
| B3 -> S3
...
| Bn -> Sn
fi
```

The semantics of this statement are as follows: each Bi is a Boolean expression, called a guard, and each Si is a statement sequence. If one Bi evaluates to true, then the corresponding statement sequence Si is executed. If more than one Bi is true, then the one and only corresponding Si is selected for execution. If no Bi is true, then an error occurs.

There are several interesting features in this description. First, it does not say that the first Bi that evaluates to true is the one chosen. Thus, the guarded if introduces nondeterminism into programming, a feature that becomes very useful in concurrent programming (Chapter 13). Second, it leaves unspecified whether all the guards are evaluated. Thus, if the evaluation of a Bi has a side effect, the result of the execution of the guarded if may be unknown. Of course, the usual deterministic implementation of such a statement would sequentially evaluate the Bi s until a true one is found, whence the corresponding Si is executed and control is transferred to the point following the guarded statement.

The two major ways that programming languages implement conditional statements like the guarded if are as if-statements and case-statements.

# 9.2.1 If-Statements

The basic form of the if-statement is as given in the extended Backus-Naur form (EBNF) rule for the if statement in C, with an optional “else” part:

```
if-statement → if ( expression ) statement [else statement]
```

where statement can be either a single statement or a sequence of statements surrounded by braces:

```
if (x > 0) y = 1/x;
else{
    x = 2;
    y = 1/z;
}
```

This form of the if (which also exists in Java and Pascal) is problematic, however, because it is ambiguous in the syntactic sense described in Chapter 6. Indeed, the statement

```
if (e1) if (e2) S1 else S2
```

has two different parse trees according to the BNF. These parse trees are shown in Figure 9.4.