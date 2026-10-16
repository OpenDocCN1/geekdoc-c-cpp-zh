Name change is another available conversion process in lambda calculus, called **alpha-conversion**: $(\lambda x.E)$ is equivalent to $(\lambda y.E[y/x])$, where as before, $E[y/x]$ stands for the expression $E$ with all free occurrences of $x$ replaced by $y$. (Note that if $y$ is a variable that already occurs in $E$ there can be trouble similar to the substitution problem just discussed.)

Finally, there is a conversion that allows for the elimination of “redundant” lambda abstractions. This conversion is called **eta-conversion**. A simple example is the expression $(\lambda x. (+ 1 x))$. Since 1 is curried, the expression $(+ 1)$ is a function of one argument, and the expression $(+ 1 x)$ can be viewed as the application of the function $+ 1$ to $x$. Thus, $(\lambda x. (+ 1 x))$ is equivalent to the function $(+ 1)$ without the lambda abstraction. In general, $(\lambda x. (E x))$ is equivalent to $E$ by eta-conversion, as long as $E$ contains no free occurrences of $x$. A further example of eta-conversion is:

$(\lambda x. (\lambda y. (+ x y))) \Rightarrow (\lambda x. (+ x)) \Rightarrow 1$

which is to say that the first expression is just another notation for the 1 function.

It is worth noting that eta-reduction is helpful in simplifying curried definitions in functional languages. For example, the ML definition

```
fun square_list lis = map (fn x => x * x) lis ;
```

can be simplified by eta-reduction to

```
val square_list = map (fn x => x * x) ;
```

The order in which beta-reductions are applied to a lambda expression can have an effect on the final result obtained, just as different evaluation orders can make a difference in programming languages. In particular, it is possible to distinguish applicative order evaluation (or pass by value) from normal order evaluation (or pass by name). For example, in the following expression:

($(\lambda x. * x x) (+ 2 3))$

we could either use applicative order, replacing $(1 2 3)$ by its value and then applying beta-reduction, as in

($(\lambda x. * x x) (+ 2 3)) \Rightarrow ((\lambda x. * x x) 5) \Rightarrow (* 5 5) \Rightarrow 25$

or we could apply beta-reduction first and then evaluate, giving normal order evaluation:

($(\lambda x. * x x) (+ 2 3)) \Rightarrow (* (+ 2 3) (+ 2 3)) \Rightarrow (* 5 5) \Rightarrow 25$

Normal order evaluation is, as we have noted several times, a kind of **delayed** evaluation, since the evaluation of expressions is done only after substitution.

Normal order evaluation can have a different result than applicative order, as we have also previously noted. A striking example is when parameter evaluation gives an undefined result. If the value of an expression does not depend on the value of the parameter, then normal order will still compute the correct value, while applicative order will also give an undefined result.