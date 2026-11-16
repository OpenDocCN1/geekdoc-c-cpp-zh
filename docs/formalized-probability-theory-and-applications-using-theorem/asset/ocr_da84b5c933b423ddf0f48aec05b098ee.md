node connecting m senders (s1, ..., sm) to n receivers (r1, ..., rn). The single MIX is determined by its inputs (senders), outputs (receivers) and the transition probabilities. We can also add clauses in the specification to capture additional information about the MIX like structural symmetry. The following is the formalization of the single MIX given in Figure 3.

```
|- MIX_channel s m X Y =
X (s) = { 0; 1 } /\ Y (s) = { 0; 1; 2; 3 } /\
(p Y | X { 0 } { 0 } = 1/2 /\ (p Y | X { 1 } { 0 } = 1/2 /\ (p Y | X
{ 2 } { 1 } = 1)
```

Zhu & Bettati (2009) used the single MIX to model an anonymity-based covert-channel where a sender is trying to covertly send messages through the MIX. They used the channel capacity as a measure of the maximum information that can be leaked through the MIX and can be used as a measure of the quality of anonymity of the network. A communication between a sender si and a receiver rj is denoted by [ si, rj ]. The term p ( su, rv ] s | si, rj ]a) represents the probability that the communication [ su, rv ] is suspected given that [ si, rj ] is actually taking place. This model describes attacks on sender-receiver anonymity. The input symbols of the covert-channel are the actual sender-receiver pairs [ s, r ]a and the output symbols are the suspected pairs [ s, r ]s. In this case, p ( s, r j s | s, r j a ) represents

# Figure 3. Single MIX example

![](bbox=[0.35, 0.6, 0.65, 0.88])