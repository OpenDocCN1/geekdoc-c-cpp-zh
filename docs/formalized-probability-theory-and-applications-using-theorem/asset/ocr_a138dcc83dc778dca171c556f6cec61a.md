The above theorem can be verified by rewriting the original goal using Theorem 6.2 and performing induction on variable n.

# Theorem 6.11

```
|- ∀ X p a b c d.
BINARY_CHANNELS_MODEL X p a b c d =>
```

```
(lim (n,probp({x | Xnx = 0} | {x | X0x = 0}) = \frac{b}{a + b}) ∧
(lim (n,probp({x | Xnx = 1} | {x | X0x = 0}) = \frac{a}{a + b}) ∧
(lim (n,probp({x | Xnx = 0} | {x | X0x = 1}) = \frac{b}{a + b}) ∧
(lim (n,probp({x | Xnx = 1} | {x | X0x = 1}) = \frac{a}{a + b})
```

The proof of Theorem 6.11 is primarily based on Theorem 6.10 along with the limit of real sequence principles. This small two-state DTMC case study clearly illustrates the main strength of the proposed theorem proving based technique against the probabilistic model checking approach (Baier & Katoen, 2008) by allowing us to verify the desired probabilistic characteristics as generic theorems that are universally quantified for all allowable values of variables a, b and n. These variables can also be specialized to specific values to obtain corresponding precise conditional probabilistic values. Moreover, we have been able to reason about the limiting behaviors, which cannot be done using probabilistic model checking.

# 6.6 AMQM PROTOCOL

As a second application, consider analyzing the probability of reaching a targeted state in an Automatic Mail Quality Measurement (AMQM) system based on the ISO/IEC 18000-7 Standard (2008) by building upon our formalized DTMC described above.

An AMQM system is used to measure the quality of postal service transport and delivery by IPC (International Post Corporation) (Nokovic & Sekerinski, 2010). It