
![](img/67fa924962ee21b3590be9f3b10d9fe7_162_0.png)

Figure 6.10 A causal DAG representing a manipulation experiment.

other causal relationships. The causal DAG representing the manipulation just discussed appears in Figure 6.10.

## 6.3.2 Causality and the Markov Condition

First, we more rigorously define a causal DAG. After that, we state the causal Markov assumption and argue why it should be satisfied.

### 6.3.2.1 Causal DAGs

We say X is a cause of Y if a manipulation of X results in a change in the probability distribution of Y. A causal graph is a directed graph containing a set of causally related random variables V such that for every X, Y ∈ V there is an edge from X to Y if and only if X is a cause of Y, and there is no subset of variables W_XY of V such that if we knew the values of the variables in W_XY, a manipulation of X would no longer change the probability distribution of Y. If there is an edge from X to Y, we call X a direct cause of Y. Note that whether or not X is a direct cause of Y depends on the variables included in V. A causal graph is a causal DAG if the causal graph is acyclic (i.e., there are no causal feedback loops).

Example 6.4 Testosterone (T) is known to convert to dihydro-testosterone (D), and dihydro-testosterone is believed to be the hormone necessary for erectile function (E). A study in [Lugg et al., 1995] tested the causal relationship among these variables in rats. They manipulated testosterone to low levels and found that both dihydro-testosterone and erectile function declined. They then held dihydro-testosterone fixed at low levels and found that erectile function was low regardless of the manipulated value of testosterone. Finally, they held dihydro-testosterone fixed at high levels and found that erectile function was high regardless of the manipulated value of testosterone. So they learned that, in a causal graph containing only the variables T, D, and E, T is a direct cause of D, and D is a direct cause of E; but, although T is a cause of E, it is not a direct cause. So the causal graph (DAG) is the one in Figure 6.11.

![](img/67fa924962ee21b3590be9f3b10d9fe7_163_0.png)

Figure 6.11 A causal DAG.

Notice that if the variable D were not in the DAG in Figure 6.11, T would be called a direct cause of E, and there would be an edge from T directly into E instead of the directed path through D. In general, our edges always represent only the relationships among the identified variables. It seems we can usually conceive of intermediate, unidentified variables along each edge. Consider the following example taken from [Spirtes et al., 1993; 2000], p. 42:

> If C is the event of striking a match, and A is the event of the match catching on fire, and no other events are considered, then C is a direct cause of A. If, however, we added B, the sulfur on the match tip achieved sufficient heat to combine with the oxygen, then we could no longer say that C directly caused A, but rather C directly caused B and B directly caused A. Accordingly, we say that B is a causal mediary between C and A if C causes B and B causes A.

Note that, in this intuitive explanation, a variable name is used to also stand for a value of the variable. For example, A is a variable whose value is on-fire or not-on-fire, and A is also used to represent that the match is on fire. Clearly, we can add more causal mediaries. For example, we could add the variable D, representing whether the match tip is abraded by a rough surface. C would then cause D, which would cause B, and so on. We could go much further and describe the chemical reaction that occurs when sulfur combines with oxygen.

Indeed, it seems we can conceive of a continuum of events in any causal description of a process. We see then that the set of observable variables is observer dependent. Apparently an individual, given myriad sensory input, selectively records discernible events and develops cause/effect relationships among them. Therefore, rather than assuming that there is a set of causally related variables out there, it seems more appropriate to only assume that, in a given context or application, we identify certain variables and develop a set of causal relationships among them.

### 6.3.2.2 Causal Markov Assumption

If we assume that the observed probability distribution P of a set of random variables V satisfies the Markov condition with the causal DAG G containing the variables, we say we are making the causal Markov assumption, and we call (G, P) a causal network. Why should we make the causal Markov assumption? To answer this question, we show several examples.

**Example 6.5** Consider again the situation involving testosterone (T), dihydrotestosterone (D), and erectile function (E). Recall the manipulation study in [Lugg et al., 1995], which we discussed in Example 6.4. This study showed that if we instantiate D, the value of E is independent of the value of T. So there is experimental evidence that the Markov condition is satisfied for a three-variable causal chain.

**Example 6.6** A history of smoking (H) is known to cause both bronchitis (B) and lung cancer (L). Lung cancer and bronchitis both cause fatigue (F), but only lung cancer can cause a chest X-ray (X) to be positive. There are no other causal relationships among the variables. Figure 6.12 shows a causal DAG containing these variables. The causal Markov assumption for that DAG entails the following conditional independencies.

| Node | Parents | Nondescendents | Conditional Independence |
|---|---|---|---|
| H | \(\emptyset\) | \(\emptyset\) | None |
| B | H | L, X | \(I_P(B, \{L, X\} | H)\) |
| L | H | B | \(I_P(L, B | H)\) |
| F | B, L | H, X | \(I_P(F, \{H, X\} | \{B, L\})\) |
| X | L | H, B, F | \(I_P(X, \{H, B, F\} | L)\) |

Given the causal relationship in Figure 6.12, we would not expect bronchitis and lung cancer to be independent, because if someone had lung cancer it would make it more probable that the individual smoked (as smoking can cause lung cancer), which would make it more probable that another effect of smoking, namely bronchitis, was present. However, if we knew someone smoked, it would already be more probable that the person had bronchitis. Learning that the individual had lung cancer could no longer increase the probability of smoking (which is now 1), which means it cannot change the probability of bronchitis. That is, the variable H shields B from the influence of L, which is what the causal Markov condition says. Similarly, a positive chest X-ray increases the probability of lung cancer, which in turn increases the probability of smoking, which in turn increases the probability of bronchitis. So, a chest X-ray and bronchitis are not independent. However, if we knew the person had lung cancer, the chest X-ray could not change the probability of lung cancer and thereby change the probability of bronchitis. So B is independent of X conditional on L, which is what the causal Markov condition says.

There are three situations in which a causal graph should not satisfy the Markov condition. The first one is when there is a causal feedback loop. For example, perhaps studying causes good grades, and good grades cause a student to study harder. When there is a causal feedback loop, our graph is not even a DAG.

The second situation is when a hidden common cause is present. The following example illustrates the problem with hidden common causes.

**Example 6.7** Suppose we wanted to create a causal DAG containing the variables cold (C), sneezing (S), and runny nose (R). Because a cold can cause both sneezing and a runny nose and neither of these conditions can cause each other, we would create the DAG in Figure 6.13 (a). The causal Markov condition for that DAG would entail $I_P(S, R|C)$. However, if there were a hidden common cause of S and R as depicted in Figure 6.13 (b), this conditional independency would not hold because even if the value of C were known, S would change the probability of H, which in turn would change the probability of R. Indeed, there is at least one other cause of sneezing and runny nose, namely hay fever. So when making the causal Markov assumption, we must be certain that we have identified all common causes.

The final situation is more subtle. It concerns the presence of *selection bias*. The following example illustrates this situation.

**Example 6.8** The pharmaceutical company Merck had been marketing its drug finasteride as medication for men with benign prostatic hyperplasia (BPH). Based on anecdotal evidence, it seemed that there was a correlation between use of the drug and regrowth of scalp hair. Let’s assume that Merck took a random sample from the population of interest and, based on that sample, determined that there is a correlation between finasteride use and hair regrowth. Assume further that there could be no hidden common causes of finasteride use and hair regrowth. Should Merck conclude that finasteride causes hair regrowth and therefore market it as a cure for baldness? Not necessarily. There is yet another possible causal explanation for this correlation. Suppose that our
