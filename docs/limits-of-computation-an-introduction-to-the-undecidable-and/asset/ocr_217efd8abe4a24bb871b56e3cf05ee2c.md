# Undecidability ■ 123

```
1 ↔ no-move-TM
10 ↔ no-move-TM
11 ↔ no-move-TM
100 ↔ no-move-TM
...
some integer ↔ TM that accepts strings beginning with '00'
...
some other integer ↔ TM that accepts strings of odd length
...
another integer ↔ TM that accepts strings {n:n is prime in binary}
...
```

FIGURE 6.12 Enumeration of the Turing machines.

Not positive natural numbers correspond to encodings of Turing machines. For example, the substring 11111 never appears in any encoding using the scheme from Chapter 1, so numbers as 11111, 11111011, and 11111011111 do not correspond to any Turing machine. This is not really a problem—it would only mean that there are more positive integers than there are Turing machines. Another simple solution is to say that each number does correspond to some Turing machine, but if it cannot be decoded into a Turing machine then we say that it corresponds to a Turing machine with no moves at all (Turing machine that rejects all inputs). Thus, 11111, 11111011, and 11111011111—and all the other Turing machine strings—correspond to this no-move TM.

We enumerate the Turing machines—take each encoding, and put them in order. See Figure 6.12.

This means that there are �₀ Turing machines. There are, however, ��₁ languages. This means that there are countably many Turing machines—including all the deciding and accepting Turing machines—and uncountably many languages.

In short, there are far more languages than Turing machines—in fact, not just more, but uncountably more. By this argument, there are languages—infinitely of them—that are not decided, or even accepted, by a Turing machine.

This is what we wanted to prove, but it is an existence proof only. In the next section, we will actually construct an example of a language not decided by any Turing machine, and another language not accepted by any Turing machine.

We restate this as a theorem, to stress its importance: