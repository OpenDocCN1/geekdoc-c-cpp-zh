```
@defun "counter"
def client(server) do
  x = send(server, {stop})
  receive do
    {value, num} -> num
  end
end
end
```

# Listing 4: Counter client obeying the protocol counter.

described by the initial session type. Since public functions are always typed with a residual session type end, certain executions could reach the case where the outstanding session is updated to end as well, i.e. `after(S_p, alpha) = end`. In such a case, we are guaranteed that the term will not produce further side-effects, as in the case of Fig. 10 where the term is reduced all the way down to some value, v.

Example 5.1. We consider a concrete example to show the importance of session fidelity. The function called client/1 sends a `stop` label and awaits a reply with the total value.
This function adheres to the following protocol (from eq. (2)):

```
counter = + { [incr...
[stop]?value(number),end
end }
```

A process evaluating the function client executes by first sending a message containing a stop label to the interacting processes' pid (t_server), as shown below.

![](bbox=[0.1, 0.425, 0.7, 0.505])

As the process evaluates, the initial term t transitions to t', where it sends a message as a side-effect. This side-effect is denoted as an action alpha, where alpha = t_server!{stop}. By the After Function Definition, counter evolves to a new session type X:

```
X = after(counter, alpha) = ?value(number).end
```

For t' to remain well-typed, it must now match with the evolved session type X, where it has to be able to receive a message labelled value, before terminating. As a result, by the session fidelity property, we know that each step of execution will be in line with the original protocol.

We will also show that ElixirST observes a conditional form of the progress property, which describes how well-typed terms transition within the aforementioned analysis context. However, we consider the most problematic scenario first, where a process depends on external factors to progress. When a process executes a term that is following the branching session type, the process has to be able to handle (and pattern match) any valid incoming message. Concretely, a term t following the session type &[...] has to be able to accept incoming messages, by (successfully) pattern matching them to one of the branches. This holds due to the [TBRANCH] rule (from Section 3.4) where we restrict all branching patterns to simple ones. In Proposition 3 we show that valid messages can always be matched to one of the branches.

# Proposition 3. Any well-typed term (Delta |- Gamma |-^w_p S > t : T < S') following the branching session type is able to process any any valid incoming message, i.e.,

```
t = receive do ({l_i; p_i^1, ... p_i^n} -> t_i)_i in end
S = &[2l_i(T_1^i, ... T_n^i), S_i]_i in i
=> match(p_j^k, v^j)_{i=1..n} is defined
after(S, ?[l_k, v^1, ... v^n]) = S_k for some k in I
```

Proof. Note that Delta |- Gamma |-^w_p S > t : T < S' and t = receive do ({l_i; p_i^1, ... p_i^n} -> t_i)_i in end imply simplepat(p_i^j, T_i^j)_{i in I, j in 1..n}. Refer to Appendix B.3.