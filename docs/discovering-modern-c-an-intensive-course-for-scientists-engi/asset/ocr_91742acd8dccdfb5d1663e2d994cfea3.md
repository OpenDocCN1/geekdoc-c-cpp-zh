TPara is substituted by the unqualified argument type—here int and unique_ptr<int>—and the type of p is the corresponding rvalue reference.

When we call f4 with an lvalue like i or j, the compiler accepts these arguments as template rvalue-reference parameters. The type parameter TPara is substituted by int& and this is also the type of p. How is this possible? The explanation is found in Table 3-1, which shows how references of references are collapsed.

The résumé of Table 3-1 is that references are collapsed to an lvalue reference when at least one of them is an lvalue reference (loosely said, very loosely, we can take the minimal number of ampersands). This explains the handling of lvalues in f4. TPara is substituted by int& and an rvalue reference thereof is int&&, too.

The lack of type substitution is the reason why the non-template rvalue references do not accept lvalues. The only reason why the function parameter can be an lvalue is that an lvalue reference is introduced by the substitution. Without this substitution, no lvalue reference is involved and references are not collapsed.

A more detailed and more dramatic telling of the whole type deduction story is found in [32, pages 9-35 and 157-214].

# 3.1.2.4 Perfect Forwarding

We have already seen that lvalues can be turned into rvalues with move (§2.3.5.4). This time we want to cast them conditionally. A forward reference parameter accepts both rvalue and lvalue arguments that are held by rvalue and lvalue references respectively. When we pass such a reference parameter to another function, we want the lvalue reference to be passed as an lvalue and the rvalue reference to be passed as an lvalue and the rvalue reference as an rvalue. However, the references themselves are lvalues in both cases (since they have names). We could cast a reference to an rvalue with move but this would also apply to an lvalue reference.

Here, we need a conditional cast. This is achieved by std::forward. It casts an rvalue reference into an rvalue and leaves an lvalue as it is. forward must be instantiated with the (unqualified) type parameter, e.g.:

```
template <typename TPara>
void f5(TPara&& p)
{
    f4(forward<TPara>(p));
}
```

The argument of f5 is passed with the same value category to f4. Whatever was passed as an lvalue to f5 is passed as an lvalue to f4; likewise for every rvalue. Like move, forward is a pure cast and does not generate a single machine operation. People have phrased this as: move does not move and forward does not forward. They rather cast their arguments to be moved or forwarded.

| | & | && |
|---|---|---|
| T& | T& | T& |
| T&& | T& | T&& |