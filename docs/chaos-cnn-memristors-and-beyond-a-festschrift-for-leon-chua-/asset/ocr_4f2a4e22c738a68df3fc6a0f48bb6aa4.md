some to declare it “a paradigm for chaos”, and few months after the experimental demonstration of secure communication using the properties of this chaotic generator, Professor L. O. Chua was visiting us for one month, in May 1993, at the University of Nice.

In both implementations — electronic circuit realization (Fig. 3) or computer simulation (Fig. 2) — of the circuit used by Kocarev et al. [15] there is an inevitable error introduced by the signal s(t). Then the claim was to enhance the performance of the chaotic masking technique by improving the convergence of the recovered signal s2(t) towards the information-bearing signal s(t). Having in mind the knowledge of relaxation methods used in numerical analysis (in numerical mathematics, relaxation methods are iterative methods for solving systems of equations, including nonlinear systems), we proposed to iterate the process of recovering the signal, cascading a second identical receiver to the first one, i.e. introducing a second system of equations comparable to Eqs. (4)–(5) driven by x2(t) instead of r(t), as displayed in Fig. 5. The second receiver also consists of two subsystems. The first one is driven by the signal x2(t) which is assumed to be more synchronized to x(t) than the transmitted

![](bbox=[0.13, 0.57, 0.44, 0.9])

Fig. 2. Experimental set up. Block diagram of the system. It contains one Chua’s circuit and two partial Chua’s circuits, that is, subsystems #1 and #2 of Fig. 3, from [15].

![](bbox=[0.5, 0.08, 0.88, 0.28])

Fig. 3. Practical realization of the receiver. The first subsystem is a partial Chua’s circuit consisting of the (vC2, iL)-subsystem driven by the transmitted signal r(t). The second subsystem is a partial Chua’s circuit consisting of the (vC1)-subsystem driven by the transmitted signal vC2(1). The triangular symbols are OpAmps which decoupled the systems, acting as the signal drive elements, from [15].

signal r(t):

```
⎧ ẏ₃ = x₂(t) − y₃ + z₃
⎨
⎩ ż₃ = −β y₃
(8)
```

The second subsystem of the second receiver is then driven by the signal y₃(t) from Eq. (8):

```
ẋ₄ = α(y₃(t) − x₄ − f(x₄))    (9)
```

Then s(t) is recovered as

```
s₄(t) = r(t) − x₄(t) ≈ s(t)    (10)
```

In practice we simply make two copies of the receiver as shown in Fig. 4. By identifying the symbols (VC1, VC2, IL) in Chua’s circuit (see Figs. 2 and 3) with (x, y, z), the electronic circuit implementation in Fig. 4 can be translated into the block diagram shown in Fig. 5. Although no two electronic circuits can be made perfectly identical in practice, this ideal situation can be approached with the help of the integrated circuit technology demonstrated in Delgado-Restituto & Rodriguez-Vasquez [6]. By fabricating several identical Chua’s circuits on the same silicon chip, the resulting circuits are almost “clones” of each other. This technique has the additional security advantage in that even if someone else has discovered the parameters (α, β) used in the system, integrating it into another silicon chip invariably introduces