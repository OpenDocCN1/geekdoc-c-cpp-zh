# Undecidability and Reducibility ■ 133

yes and—but there may be many instances of $P_2$ that are not related to anything in $P_1$.

Note on the name for: Despite the best efforts of Donald Knuth, who did succeed in standardizing the terms NP-hard and NP-complete (see the next chapter), there are various terms used for what we have defined as reducible. Emil Post, in 1944, called this "many-one reducible" since the mapping may take many instances from $P_1$ to a single instance of $P_2$. Some authors use "mapping reducible"; others do not use a function. Instead, they speak of constructing a yes/no instance of $P_2$ from an instance of $P_1$.

There are other kinds of reducibility. If we add the requirement that the function calculated in polynomial time, we get "polynomial time mapping". We will find this definition very important in Chapters 8 through 10.

# Definition 7.2

A decision problem $P_1$ is polynomially reducible to decision problem $P_2$, written $P_1 \leq_p P_2$, if there is a mapping $f$ from possible instances (yes or no) of $P_1$ to possible instances of $P_2$, such that:

+   1. For any yes/no instance X of $P_1$, $f(X)$ can be computed by a Turing machine (transducer) in time bounded by a polynomial $p(|X|), |X|$ = length of the input.
2. If X is a yes instance of $P_1$, then $f(X)$ is a yes instance of $P_2$.
3. If X is no instance of $P_1$, then $f(X)$ is a no instance of $P_2$.

The only difference between definitions 7.1 and 7.2 is the addition of the restriction that the function can be computed in polynomial time.

Turing reducibility is a slightly different and more general concept in which the answer to the right-hand problem can be used to answer the left-hand problem. It is not used in this text. Log space reducibility is another different and more restrictive reducibility in which the function $f$ is only allowed to use a work space that is bounded by a constant times the log of the input size.

It would be tempting to think that answering $P_1$ would also answer $P_2$. That would be the case for yes or no instances that are in the range of $f$—that is, they come from something in $P_1$. Thus, in the two instances