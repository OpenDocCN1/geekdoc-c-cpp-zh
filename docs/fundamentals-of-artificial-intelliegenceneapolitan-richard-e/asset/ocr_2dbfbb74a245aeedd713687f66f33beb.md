The meaning of an event is that one of the elements of the subset is the outcome of the experiment. In the preceding example, the meaning of the event E is that the card drawn is one of the four jacks, and the meaning of the elementary event F is that the card is the jack of hearts.

We articulate our certainty that an event contains the outcome of the experiment with a real number between 0 and 1. This number is called the **probability** of the event. When the sample space is finite, a probability of 0 means we are certain the event does not contain the outcome, whereas a probability of 1 means we are certain it does. Values in between represent varying degrees of belief. The following definition formally defines probability for a finite sample space.

**Definition 5.1** Suppose we have a sample space \(\Omega\) containing \(n\) distinct elements; that is, \(\Omega = \{e_1, e_2, \dots, e_n\}\).

A function that assigns a real number \(P(E)\) to each event \(E \subseteq \Omega\) is called a **probability function** on the set of subsets of \(\Omega\) if it satisfies the following conditions:

+   1. \(0 \le P(e_i) \le 1\) for \(1 \le i \le n\)
+   2. \(P(e_1) + P(e_2) + \dots + P(e_n) = 1\)
+   3. For each event that is not an elementary event, \(P(E)\) is the sum of the probabilities of the elementary events whose outcomes are in E. For example, if \(E = \{e_3, e_6, e_8\}\), then \(P(E) = P(e_3) + P(e_6) + P(e_8)\)

The pair \((\Omega, P)\) is called a **probability space.**\(\blacklozenge\)

Because probability is defined as a function whose domain is a set of sets, we should write \(P(\{e_i\})\) instead of \(P(e_i)\) when denoting the probability of an elementary event. However, for the sake of simplicity, we do not do this. In the same way, we write \(P(e_3, e_6, e_8)\) instead of \(P(\{e_3, e_6, e_8\})\).

The most straightforward way to assign probabilities is to use the **Principle of Indifference**, which says that outcomes are to be considered equiprobable if we have no reason to expect one over the other. According to this principle, when there are \(n\) elementary events, each has probability equal to \(1/n\).

**Example 5.2** Let the experiment be tossing a coin. Then the sample space is \(\Omega = \{heads, tails\}\),

and, according to the Principle of Indifference, we assign \(P(heads) = P(tails) = .5\).