2. In text classification, while a large corpus or a document collection contains many different words, a particular document will usually only contain quite limited words. To save space for representation, a document is represented as a *single attribute* $a$, with its *value* as the set of words that appear in the document or a word list of the document, i.e., $a = \{w_1, w_2, \ldots, w_n\}$. The primitive tests (conditions) on a set-valued attribute $a$ are in the form of $w_i \in a$.

For a rule construction, RIPPER will repeatedly add conditions to rule $r_0$, which is initialized as an empty antecedent. Specifically, at each iteration $i$, a single condition is added to the rule $r_i$, producing an expanded rule $r_{i+1}$. The condition added to $r_{i+1}$ is the one that maximizes information gain with regards to $r_i$. Given the set-valued attributes, RIPPER will carry out the following two steps to find a best condition to add:

+   1. For the current rule $r_i$, RIPPER will iterate over the set of examples/documents $S$ that are covered by $r_i$ and record a word list $W$ where each word $w_i \in W$ appears as an element/value of attribute $a$ in $S$. For each $w_i \in W$, RIPPER also computes two statistics, namely $p_i$ and $n_i$, which represent the number of positive and negative examples in $S$ that contain $w_i$, respectively.
+   
+   2. RIPPER will go over all the words $w_i \in W$, and use $p_i$ and $n_i$ to calculate the information gain for its condition $w_i \in a$. We can then choose the condition that yields the largest information gain and add it to rule $r_i$ to form rule $r_{i+1}$.

The above process of adding new literals/conditions continues until the rule does not cover negative examples or until no condition has a positive information gain. Note the process only requires time linear in the size of $S$, facilitating its applications to handle large text corpora.

RIPPER has been used to classify or filter personal emails [69] based on a relatively small sets of labeled messages.

# Sleeping-experts for phrases for text categorization

Sleeping-experts [56] is an ensemble framework that builds a *master algorithm* to integrate the “advice” of different “experts” or classifiers [51, 76]. Given a test example, the master algorithm uses a weighted combination of the predictions of the experts. One efficient weighted assignment algorithm is the *multiplicative* update method where weights for each individual experts are updated by multiplying them by a constant. Particularly, those “correct” experts that make right classification will be able to keep their weights unchanged (i.e., multiplying 1) while those “bad” experts that make wrong classification have to multiply a constant (less than 1) so that their weights will become smaller.

In the context of text classification, the experts correspond to all length-$k$ phrases that occur in a corpus. Given a document that needs to be classified, those experts are “awake” and make predictions if they appear in the document; the remaining experts are said to be “sleeping” on the document. Different from the context information used in the RIPPER, the context information in sleeping-experts (or sleeping-experts for phrases), is defined in the following phrase form:

$$w_{i_1}, w_{i_2} \cdots w_{i_j}$$

where $i_1 < i_2 < \cdots < i_{j-1} < i_j$ and $i_j - i_1 < n$.

Note that there could be some “holes” or “gaps” between any two words in the context/phrase. The detailed sleeping-experts for phrases algorithm is as follows.

# The sleeping-experts algorithm for phrases

**Input Parameters:** $\beta \in (0,1)$, $\theta_C \in (0,1)$, number of labeled documents $T$  **Initialize:** $Pool \leftarrow 0$

**Do** for $t=1, 2, \ldots, T$