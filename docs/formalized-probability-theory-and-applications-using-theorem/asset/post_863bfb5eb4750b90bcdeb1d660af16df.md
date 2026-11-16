
### Definition 13.10

```
|- forall n k. binomial n k =
(binomial n 0 = (1:num)) /\
(binomial 0 (SUC k) = (0:num)) /\
(binomial (SUC n) (SUC k) = binomial n (SUC k) + binomial n k).
```

The coverage intensity of the whole WSN with n nodes has been formally specified by the function cvrge_intsty_network, shown in Definition 13.11. The latter takes as parameters: p: the probability space, X: a random variable that returns an extended real number, k: the number of sub-networks, s: the summation set used in Definition 13.8, C: the random variable describing the number of covering nodes, n: the total number of nodes, and q: the probability that each sensor covers a given point.

### Definition 13.11

```
|- forall p x k s c n q. cvrge_intsty_network p x k s c n q =
expectation p (x. cvrge_intsty p p x k s (num (C x))).
```

where the function expectation, used in the above definition, designates the higher-order-logic formalization of the expectation of a random variable that returns an extended real, the function num converts an extended real; (&m), to its corresponding natural value m, using the real function floor.

The final network coverage intensity cvrge_intsty_network has been formally verified:

### Theorem 13.4

```
|- forall p C q k s. (prob_space p) /\ (FINITE (p_space p)) /\
(0 < q < 1) /\ (events p = POW (p_space p)) /\ (1 <= n) /\ (1 < k)
/\ FINITE s /\ (CARD s = k) /\ (sn_covers p C p q n) /\
(expectation p # PosInf) /\ (expectation p # NegInf) /\
(forall i x. (i ∈ s) /\ (x ∈ p_space p) /\
sbst_non_empty rv (X i) p k (num(C x))))
==> cvrge_intsty_network p x k s c n q = Normal (1 - (1 - q/(s*k))^n)).
```

where

- The assumption (events p = POW (p_space p)) means that the set of events is the power set of the sample space.
- The assumptions (1 <= n) ensures that the WSN include at least one node, while (0 < q < 1) ensures that the probability q lies in [0..1].
- sn_covers p is the Binomial random variable (Definition 13.9) with a finite expectation, i.e., (expectation p C ≠ PosInf) ∧ (expectation p C ≠ NegInf).
- The function (sbst_non_empty_rv (X i) p k (num(C x))) is the same as specified in Definition 13.7, except that it takes the last input parameter (num(C x)) as the output values of the random variable C.

The proof of the above theorem is primarily based on some operations on the Lebesgue integral, and the linearity of expectation which further requires Theorem 13.5 giving the expectation of a function of a random variable. Indeed, as we can notice from Definition 13.11, the network coverage intensity Cn is the expectation of a function of the random variable C. In addition, the proof of Theorem 13.5 includes the proof of injectivity of some functions and some properties related to the random variables functions. Finally, a considerable amount of real analysis related to Theorem 13.6, which formalizes the Binomial theorem for reals, and to the summation function has been necessary to achieve this proof.

### Theorem 13.5

```
⊢ ∀ C p q n k. (prob_space p) ∧ (events p = POW (p_space p)) ∧ (FINITE (p_space p)) ∧ (1 < k) ∧ (0 < q < 1) ∧ (1 ≤ n) ∧ (sn_covers p C p q n)) ⇒ (expectation p (x. f_fct (num (C x)) k) = Normal (1 - q/(&k))^x
```

where the function f_fct is defined as follows

```
f_fct x k=Normal (1-1/k)^x (13.5)
```

### Theorem 13.6

```
⊢ ∀ (a:real) (b:real) n. (a + b) pow n = sum (0, SUC n) (i. &(binomial n i) * a pow i * b pow i)
```

In this section, we presented our new higher-order-logic formalizations of the k-set randomized scheduling for wireless sensor networks, using our probability theory available in the HOL theorem prover. These formalizations have been then utilized to formally reason about the coverage performance properties. In the next section, we will demonstrate how the developed generic theorems greatly facilitate the formal analysis of real-world WSN applications.

## 13.3 FORMAL ANALYSIS OF WSN FOR FOREST FIRE DETECTION

Wireless sensor networks have been extensively explored for forest fire detection (Liu, Wu, Xiao, & Sun, 2011). Indeed, forest fires are considered to be one of the worst natural disasters throughout the world. They threaten forests, animals, and people, and cause a lot of environmental degradations. Indeed, more than 100,000 wild fires occur annually. For example, in Tunisia, 103 fires destroyed 287 hectares of forests just between May 1, 2012 and July 25, 2012. In such context, the main job of the sensors is to sense and communicate temperature, humidity and barometric pressure values to a base station. Moreover, the harsh nature of the field of interest makes a random deployment by air-dropping sensors much easier. In this section, we are interested in formally analyzing the coverage performances of a wireless sensor network deployed for a forest fire application. Due to the safety-critical feature of the target application, the deployed WSN has to remain alive as long as possible while ensuring an efficient coverage of any fire breakthrough. Nevertheless, most of the existing WSNs for forest fire detection suffer from lifetime limitations. In order to extend the whole network lifetime, the k-set randomized scheduling algorithm has been proposed for a given forest fire detection application using wireless sensor networks. In the specified application, the nodes have a sensing area r = 30, and are deployed into a forest region of size a = 100m x 100m, whereas the success probability q of a sensor covering a point, is q = r / a = 0.003.

Based on our theoretical development done in the previous section, we now conduct a formal asymptotic analysis of the probabilistic coverage based on the parameters n and k (Elleuch, Hasan, Tahar & Abid, 2012). For that, we are going to tackle the generic case and then instantiate it for the given forest fire application. Hence, we simply denote (cvrge_intsty_network p X k s C n q) by (Cn_wsn p X k s C n q). In the context of our application, we can formally specify the given forest fire detection application by specializing Definition 13.11 since it describes the generic coverage intensity of a WSN using a k-set randomized scheduling algorithm.

### Definition 13.12

```
⊢ ∀ p X k s C n.
cn_wsn_first p X k s C n = cvrge_intsty_network p X k s C n
(0.003).
```

Then, we easily check in HOL that (cn_wsn_first p X k s C n) equals

Normal (1 - (1 - (0.003/k)^n)) (13.6)

It is important to note that, for space constraints, we only mention the main mathematical assumptions related to the used variables in the network coverage intensity.

The number of deployed nodes n is a common critical attribute, which has a significant impact on both energy and coverage. Intuitively, deploying too few nodes may not guarantee a good coverage, however deploying too many nodes can lead to a waste of energy. In the next analysis, we formally confirm this intuition through verifying the minimum number of nodes n min that are required to deploy in order to ensure a network coverage intensity Cn of at least t, for a given number k. This lower bound can be formally verified based on Theorem 13.4, which gives a clear relationship between the network coverage intensity Cn_wsn, the number of nodes n and the number of disjoint sub-networks k.

### Lemma 13.1

```
⊢ ∀ p X k s C n q t. (1 ≤ n) ∧ (1 < k) ∧ (0 < q < 1) ∧ (0 < t < 1) ∧ (Normal t ≤ Cn_wsn p X k s C n q) ⇒ ln(1-t) / (ln(1-q/k)) ≤ &n.
```

The proof of the above lemma is based on some properties of transcendental functions and arithmetic reasoning.

Next, we formally verify, in Lemma 13.2, that the network coverage intensity Cn_wsn is an increasing function of n, i.e., a larger n value leads to a better coverage intensity. In this case, an occurring event at any point of the monitored area is expected to be covered more quickly, since it is likely that many more covering nodes are deployed in the surrounding area.

### Lemma 13.2

```
⊢ ∀ p X k s C q. (1 < k) ∧ (0 < q < 1) ⇒ (mono_incr (λn. real (Cn_wsn p X k s C (SUC n) q)))
```

where the function real is used to convert the network coverage intensity of type extended real to its corresponding real value, and mono_incr is the HOL definition of an increasing sequence, which we define as follows:

### Definition 13.13

```
⊢ ∀ f. mono_incr f = ∀n, f n ≤ f (SUC n).
```

We can deduce hence that under the randomized scheduling, which divides the network into a given number k of sub-networks, any network coverage intensity Cn_wsn can be achieved by increasing the number of deployed nodes n.

Besides, we formally verify in Lemma 13.3 that when n is very large, Cn_wsn approaches its ideal value 1.
