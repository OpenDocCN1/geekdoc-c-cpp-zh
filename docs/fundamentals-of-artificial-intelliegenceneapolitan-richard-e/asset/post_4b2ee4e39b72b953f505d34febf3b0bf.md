
independently from the mechanism that inhibits tuberculosis from resulting in fatigue. Mathematically, this assumption is as follows:

\( P(F = no|B = yes, T = yes, L = no) = (1 - p_B)(1 - p_T) \\
= (1 - .6)(1 - .7) = .12. \)

Note that in the previous equality we are conditioning on bronchitis and tuberculosis both being present and lung cancer being absent. In this case, fatigue should occur unless the causal effects of bronchitis and tuberculosis are both inhibited. Because we have assumed these inhibitions act independently, the probability that both effects are inhibited is the product of the probabilities that each is inhibited, which is \( (1 - p_B)(1 - p_T) \).

In this same way, if all three causes are present, we have

\( P(F = no|B = yes, T = yes, L = yes) = (1 - p_B)(1 - p_T)(1 - p_L) \\
= (1 - .6)(1 - .7)(1 - .8) = .024. \)

Notice that when more causes are present, it is less probable that fatigue will be absent. This is what we would expect. It is left as an exercise to compute the remaining six conditional probabilities needed for node \( F \) in Figure 6.25. The reason that we only need to compute eight conditional probabilities is because the variables are binary, and therefore we need only compute the probabilities that \( F = no \). The probabilities that \( F = yes \) are uniquely determined by these. For example,

\( P(F = yes|B = yes, T = yes, L = yes) = 1 - .024 = .976. \)

Although we illustrated the model for three causes, it clearly extends to an arbitrary number of causes. We showed the assumptions in the model in italics when we introduced them. Next, we summarize them and show the general formula.

The noisy OR-gate model makes the following three assumptions:

- 1. **Causal inhibition:** This assumption entails that there is some mechanism which inhibits a cause from bringing about its effect, and the presence of the cause results in the presence of the effect if and only if this mechanism is disabled (turned off).
- 2. **Exception independence:** This assumption entails that the mechanism which inhibits one cause is independent of the mechanism that inhibits other causes.
- 3. **Accountability:** This assumption entails that an effect can happen only if at least one of its causes is present and is not being inhibited.

The general formula for the noisy OR-gate model is as follows: Suppose \( Y \) has \( n \) causes \( X_1, X_2, ..., X_n \), all variables are binary, and we assume the noisy OR-gate model. Let \( p_i \) be the causal strength of \( X_i \) for \( Y \). That is,

\( p_i = P(Y = yes|X_1 = no, X_2 = no, ... X_i = yes, ... X_n = no). \)

![](img/67fa924962ee21b3590be9f3b10d9fe7_182_0.png)

Figure 6.26 The probabilities in (a) are the causal strengths in the noisy OR-gate model. The probabilities in (b) are the ones we ascertain.

```
P(Y = no|X) = \prod_{i \text{ such that } X_i \in X} (1 - p_i).
```

## 6.6.3 Leaky Noisy OR-Gate Model

Of the three assumptions in the noisy OR-gate model, the assumption of accountability seems to be justified least often. For example, in the case of fatigue, there are certainly other causes of fatigue such as listening to a lecture by Professor Neapolitan. So the model in Figure 6.25 does not contain all causes of fatigue, and the assumption of accountability is not justified. It seems in many, if not most, situations we would not be certain that we have elaborated all known causes of an effect. Next, we show a version of the model that does not assume accountability. The derivation of the formula for this model is not simple and intuitive like the one for the basic noisy OR-gate model. So here we simply present the model without deriving it. The formula is derived in [Neapolitan and Jiang, 2007].

### 6.6.3.1 Leaky Noisy OR-Gate Formula

The leaky noisy OR-gate model assumes that all causes that have not been articulated can be grouped into one other cause H and that the articulated causes, along with H, satisfy the three assumptions in the noisy OR-gate model. This is illustrated for the fatigue example in Figure 6.26 (a). The probabilities in that figure are the causal strengths in the noisy OR-gate model. For example,

```
p'_B = P(F = yes|B = yes, T = no, L = no, H = no).
```

We could not ascertain the values because we do not know whether or not H is present. The probabilities in Figure 6.26 (b) are the ones we could ascertain. For each of the three articulated causes, the probability shown is the probability the effect is present given that the remaining two articulated causes are not present. For example,

```
p_B = P(F = yes|B = yes, T = no, L = no).
```

Note the difference in the probabilities \(p'_B\) and \(p_B\). The latter one does not condition on a value of \(H\), while the former one does. The probability \(p_0\) is different from the other probabilities. It is the probability that the effect will be present given none of the articulated causes are present. That is,

```
p_0 = P(F = yes|B = no, T = no, L = no).
```

Note again that we are not conditioning on a value of \(H\).

Our goal is to develop conditional probability distributions for a Bayesian network containing the nodes \(B\), \(T\), \(L\), and \(F\) from the probabilities ascertained in Figure 6.26 (b). We show an example that realizes this goal after presenting the formula necessary to the task.

The general formula for the leaky noisy OR-gate model is as follows (a derivation appears in the next subsection): Suppose \(Y\) has \(n\) causes \(X_1, X_2, ..., X_n\), all variables are binary, and we assume the leaky noisy OR-gate model. Let

```
p_i = P(Y = yes|X_1 = no, X_2 = no, ... X_i = yes, ... X_n = no) \quad (6.3)
```

```
p_0 = P(Y = yes|X_1 = no, X_2 = no, ... X_n = no). \quad (6.4)
```

Then if \(\mathbf{X}\) is a set of nodes that are instantiated to yes,

```
P(Y = no|\mathbf{X}) = (1 - p_0) \prod_{i \text{ such that } X_i \in \mathbf{X}} \frac{1 - p_i}{1 - p_0}.
```

### Example 6.17

Let's compute the conditional probabilities for a Bayesian network containing the nodes \(B\), \(T\), \(L\), and \(F\) from the probabilities ascertained in Figure 6.26 (b). We have

```
P(F = no|B = no, T = no, L = no) = 1 - p_0
= 1 - .1 = .9

P(F = no|B = no, T = no, L = yes) = (1 - p_0) \frac{1 - p_L}{1 - p_0}
= 1 - .8 = .2

P(F = no|B = no, T = yes, L = no) = (1 - p_0) \frac{1 - p_T}{1 - p_0}
= 1 - .7 = .3

P(F = no|B = no, T = yes, L = yes) = (1 - p_0) \frac{1 - p_T}{1 - p_0} \frac{1 - p_L}{1 - p_0}
= \frac{(1 - .7)(1 - .8)}{1 - .1} = .067
```

![](img/67fa924962ee21b3590be9f3b10d9fe7_184_0.png)

Figure 6.27 A small portion of the Bayesian network in Promedas. Courtesy of Bert Kappen, Promedas project.

It is left as an exercise to compute the remaining four conditional probabilities.

## 6.6.4 Further Models

A generalization of the noisy OR-gate model to the case of more than two values appears in [Srinivas, 1993]. Diez and Druzdzel [2002] propose a general framework for canonical models, classifying them into three categories: deterministic, noisy, and leaky. They then analyze the most common families of canonical models, namely the noisy OR/MAX, the noisy AND/MIN, and the noisy XOR. Other models for succinctly representing the conditional distributions use the sigmoid function [Neal, 1992] and the logit function [McLachlan and Krishnan, 2008]. Another approach to reducing the number of parameter estimates is the use of embedded Bayesian networks, which is discussed in [Heckerman and Meek, 1997].

## 6.7 Large-Scale Application: Promedas

Bayesian networks have been applied successfully in many domains. Section 8.8 discusses many of these applications. Here we present perhaps the largest

![](img/67fa924962ee21b3590be9f3b10d9fe7_185_0.png)

Figure 6.28 The Bayesian network in Figure 6.27 with some of the nodes instantiated. Courtesy of Bert Kappen, Promedas project.

**Promedas** (PRObabilistic MEdical Diagnostic Advisory System) is a diagnostic decision support system used in health care. This computer program was developed by research groups of SNN Adaptive Intelligence, University of Nijmegen and University Medical Center Utrecht. Promedas produces a differential diagnosis using a set of patient findings such as history data, physical findings and laboratory data. The findings can be provided by an individual user or an Electronic Patient Records. For each diagnoses Promedas suggests additional tests that can be performed to make the differential diagnosis more precise.

> — http://www.promedas.nl/

A small part of the Bayesian network in Promedas appears in Figure 6.27. This figure shows a subset of diagnoses and some of the conditions that affect their prior probability. In addition, some tests are shown, whose probability is affected by these diagnoses. Connections between these diagnoses and other tests are suppressed, as well as connections between the shown tests and other diagnoses. Figure 6.28 shows as an application of this small subnetwork to a particular patient. This patient is a sushi chef who recently visited Nigeria. Both these facts affect his prevalence for lung flukes. His white blood cell count
