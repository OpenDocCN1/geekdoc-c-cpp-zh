# 3.6. FINITE AUTOMATA

```
```text
s = s0;
c = nextChar();
while ( c != eof ) {
    s = move(s, c);
    c = nextChar();
}
if ( s is in F ) return "yes";
else return "no";
```
```

Figure 3.27: Simulating a DFA

![](bbox=[0.332, 0.355, 0.681, 0.438])

Figure 3.28: DFA accepting (a|b)*abb

# 3.6.5  Exercises for Section 3.6

**Exercise 3.6.1:** Figure 3.19 in the exercises of Section 3.4 computes the failure function for the KMP algorithm. Show how, given that failure function, we can construct, from a keyword $b_1b_2\cdots b_n$, an $n+1$-state DFA that recognizes $\Sigma^*b_1b_2\cdots b_n$, where the dot stands for “any character.” Moreover, this DFA can be constructed in $O(n)$ time.

**Exercise 3.6.2:** Design finite automata (deterministic or nondeterministic) for each of the languages of Exercise 3.3.5.

**Exercise 3.6.3:** For the NFA of Fig. 3.29, indicate all the paths labeled $aabb$. Does the NFA accept $aabb$?

![](bbox=[0.332, 0.728, 0.681, 0.819])

Figure 3.29: NFA for Exercise 3.6.3