
measures how fast mail travels from one point to another by using an in-plant process monitoring of the tag serial number and recording the time when a message from the tag is received. This kind of quality measurement of solutions is based on Radio-frequency identification (RFID), which is a technology that identifies and tracks objects, such as a product, an animal or a person by using radio waves to transfer data from an electronic tag, called the RFID tag. In the last decade, a large volume of research was conducted on complying RFID systems with the international standard ISO/IEC 18000-7. The AMQM system exhibits some features of the ISO/IEC 18000-7 standard and hence its formal analysis is quite important.

In an AMQM system, tags are intended for identifying the objects that are to be managed. The interrogator communicates with the tag in its RF (Radio Frequency) communication range and controls the protocol, reads information from the tag, directs the tag to store data in some cases, and makes sure that messages are delivered and are also valid. An interrogator controls the messages that are transmitted during their allotted time periods called slots and an acknowledge received when each message has been received successfully. Based on the AMQM communication protocol, the timing diagram of a tag collection process is depicted in Figure 2.

![](img/0e284aa46fa831bc38a68343fef110e3_93_0.png)

The communication sequence starts with a Wakeup Period (WP), within which wake up signals are sent to bring all tags in the ready state. The WP is followed by a collection round named Command Period (CP), which in turn consists of a collection command period, a Listen Period (LP) and an Acknowledgment Period (AP). The interrogator then waits for the responses from the tags that are sent randomly. The tag collection is done based on a predetermined algorithm that complies with the ISO/IEC 18000-7 standard. Thus, this system has two properties:

- 1. The probability that a message can be delivered successfully within i slots is 1 - (n - 1) / n
- 2. If the collection process is long enough, eventually any message can be delivered successfully.

This communication protocol can be modeled as a DTMC with 4 states: s0 (start), s1 (try), s2 (lost) and s3 (delivered), as shown in Figure 3.

In the start state, the message is generated. The next state is always the state try and thus the probability from the start state to try state is 1. The probability of losing a message is $\alpha$. Thus in the case of losing a message, the system will move to the lost state with probability $\alpha$. Whereas, it moves to the delivered state with probability $\beta = 1 - \alpha$ in case of a successful transmission. Hence, the probability that a message can be delivered successfully is $\beta$, which equals to $1 - \alpha$. Once a message is delivered successfully, the system moves to the start state for getting ready to identify the other tags in the next time slot. When the collection process ends, the system goes to sleep mode in order to minimize power consumption. The state transition probability matrix, corresponding to the Markov chain, given in Figure 3, is as follows:

\( P = \begin{pmatrix} 0 & 1 & 0 & 0 \\ 0 & 0 & 1 - \frac{1}{n} & \frac{1}{n} \\ 0 & 1 & 0 & 0 \\ 1 & 0 & 0 & 0 \end{pmatrix}; I = \begin{pmatrix} 1 \\ 0 \\ 0 \\ 0 \end{pmatrix} \)

**Figure 3. DTMC model of the AMQM protocol**

![](img/0e284aa46fa831bc38a68343fef110e3_94_0.png)

The initial distribution and transition probability can be expressed as two functions in higher-order logic as follows:

### Definition 6.13

```
|- Li i = if (i = 0) then 1 else 0
|- Lt n t i j = case (i,j) of
(0, 1) -> 1 | (0, _) -> 0 | (1, 2) -> 1 - 1/n | (1, 3) -> 1/n |
(1, _) -> 0 | (2, 1) -> 1 | (2, _) -> 0 | (3, 0) -> 1 | (3, _) -> 0
```

Now, the tag collection process involved in the AMQM protocol can be formalized as a time-homogeneous DTMC, based on the state diagram and the initial distribution and transition probability matrix.

### Definition 6.14

```
|- forall X p a b c d. AMQM_MODEL X p n =
th_dtmc X p [(0, 3)], POW [(0, 3)] Li (Itr n) \land (1 \leq n)
```

Here, the state space is represented as a pair, in which the set {0, 3} contains all the states and POW [0,3] is the sigma-algebra of the states set {0, 3}, to ensure this state space is measurable. Li and Lt n represent the initial distribution and the transition probability matrix, respectively. Variable n denotes the number of tags that are sent randomly. The first condition ensures the model to be a time-homogeneous DTMC. The second condition refers that more than one node are considered in this collection process. Generally, the possible path of delivering a message successfully can be expressed as \pi = (start, try, (lost, try)*, delivered).

Here, k represents the number of iterations required for a successful message transmission. Let Pr (<> delivered i) be the probability of delivering a message within \( i \) trials, where \(\Diamond\) is a logic represents the temporal operator “eventually”. Then the probability of reaching state s3 is given by the following equation where \( n \) represents the number of tags.

\(\text{Pr } (\Diamond \text{ delivered })_i = \sum_{k=0}^{i-1} \alpha^k \beta = 1 - \left( \frac{n-1}{n} \right)^i \quad (6.10)\)

If the collection process is long enough, that is \( i \) tends to \(+\infty\), then finally the message always can be delivered successfully. So the probability of delivering a message successfully in the future is

\(\text{Pr } (\Diamond \text{ delivered }) = \sum_{k=0}^{\infty} \alpha^k \beta = \frac{\beta}{1-\alpha} = \frac{\frac{1}{n}}{1 - \frac{n-1}{n}} = 1 \quad (6.11)\)

Now, the two properties presented in Equations (6.10) and (6.11) can be expressed in higher-order logic as Theorem 6.12 and Theorem 6.13.

### Theorem 6.12

```
⊢ ∀ X p n i.
AMQM_MODEL X p n ⇒
sum (0, i) (λk.
P (( X2 + k * 2 = 3 ) ∩
⋂_{m=0}^{k-1} ( ( X3 + m * 2 = 1 ) ∩
{ X2 + m * 2 = 2 } ) ∩
{ X1 = 1 } ∩ ( X0 = 0 )))
= 1 - \left( \frac{n-1}{n} \right)^i
```

### Theorem 6.13

```
|- ∀ X p n .
AMQM_MODEL X p n =>
lim (\X i_sum (0, 1) (\k.
prob p ({X2 + k * 2 = 3 } n \cap
\bigcap_{m=0}^{k-1} ({X3 + m * 2 = 1 } \cap
{X2 + m * 2 = 2 } ) n {X1 = 0 } n {X0 = 0 }))) = 1
```

The proofs of both Theorem 6.12 and Theorem 6.13 are mainly based on Theorem 6.1 along with some arithmetic reasoning.

In Theorem 6.12, which corresponds to Equation (6.10), the variable i refers to the number of trials required for successfully delivering n tags. The performance of a tag collection algorithm can be evaluated by this probability. Theorem 6.13 verifies that the probability of reaching the delivered state in infinite trials is 1. That is to say, if the tag collection process is long enough, at last the reader will receive all the tags generated at the start state successfully.

## 6.7 CONCLUSION

In this chapter, we presented a higher-order-logic formalization of the DTMC with a finite state space. This formalization allows the modeling of both time-homogeneous and time-inhomogeneous DTMCs. When the transition probabilities are time dependent, then the parameter p_g contains the dependence on time t. Furthermore, the general state space s in Definition 6.3 covers two cases: infinite or finite state spaces. Since time-homogeneous DTMCs are the most frequently used in many applications, the chapter provided a formal definition of time-homogeneous DTMC. Building upon the formalization of DTMC, the most commonly used theorems, such as joint probability theorem, Chapman-Kolmogorov Equation and Absolute probability, were formally verified in HOL. These theorems are foundational for analyzing all kinds of DTMC models. Moreover, the reversible stochastic process and detailed balance equations, which facilitate the verification of the reversibility property of a DTMC, have also been verified. Also, we described the formalizations of stationary distribution and stationary process, which are the basic concepts of the performance analysis. Using these notions, the formal verification of two interesting properties of the DTMC that satisfy the detailed balance equations has also been presented. Finally, for illustration purposes, the chapter presented the formal verification of two interesting applications of DTMC.
