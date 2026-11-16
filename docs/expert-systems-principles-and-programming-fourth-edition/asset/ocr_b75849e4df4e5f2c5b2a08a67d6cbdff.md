ones such as P(E1 ∩ E2 | H'). There are problems with this assumption of conditional independence that will be discussed later.

While (2) is a simplification, it still does require knowledge of the prior probabilities P(Ei) and P(Ei). It's actually difficult for experts to state prior probabilities because they don't reason that way. For example, if a person goes to see a doctor, the doctor does not assume that the person has a cold a priori, because that is the most common disease and so its probability is highest.

The major problem in assigning prior probabilities is the difficulty of determining them for likelihoods. For probabilities involving reproducible events such as throwing dice, it's easy to acquire the probabilities by empirical or theoretical studies. However, when dealing with events such as finding a major mineral deposit, it's impossible to determine the prior likelihoods exactly. For example, what's the prior likelihood that your house sits on land with a major gold deposit under it? Is it 1.0, 0.01, 0.0000001, or some other number? These are unique situations in which the prior probabilities cannot be determined.

Situation 3: N pieces of uncertain evidence conclude H.

This is the general case of uncertainty in the evidence and in the rule, which depends on the evidence. As the number of pieces of evidence increases, it becomes impossible to determine all the joint and prior probabilities or likelihoods. Different approximations have been used to account for the general case of N pieces of evidence.

# Combining Evidence by Fuzzy Logic

# Conjunction of Evidence

Suppose a rule:

```
IF E THEN H
```

has E as the conjunction of evidence, as in:

```
IF E1 AND E2 AND ... En THEN H
```

All the E must be true with some probability for the antecedent to be true. In the general case, each piece of evidence is based on partial evidence e. The probability of the evidence is:

```
P(E | e) = P(E1 ∩ E2 ∩ ... ∩ En | e)
```

```
= P(E1 ∩ E2 ∩ ... ∩ En ∩ e) / P(e)
```