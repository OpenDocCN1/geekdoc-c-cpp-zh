
### Theorem 12.8

```
|- ∀ X p a b.
prob_space p /\ (events p = POW (p_space p)) /\
(∃ y x. X y ≠ NegInf /\ X y ≠ PosInf) /\
a <= b ==> survival_function p X b <= survival_function p X a
```

The proof of Theorem 9.7 is also based on the properties of CDF of a random variable.

In a similar way other lifetime distributions like hazard function, cumulative hazard function and the p^th fractile of a random variable can also be formalized in HOL. The work presented in this chapter makes it possible to perform accurate lifetime reliability modeling and analysis for the very first time in the sound environment of a theorem prover. This approach, though interactive, is very flexible and allows modeling of lifetime behavior using single and multiple parameter, bounded and unbounded continuous random variables. This allows us to model increasing, constant and decreasing failure rates together with both short and long term lifetime behaviors. In fact, at this time any random variable with a closed form CDF expression is supported and can be formally reasoned about. This ability makes it suitable for a large set of reliability analysis problems in safety-critical engineering systems.

## 12.4 RELIABILITY BLOCK DIAGRAMS

A reliability block diagram (RBD) (Abd-Allah, 1997) is used to assess various failure related characteristics, such as reliability, availability, dependability and maintainability, of a wide range of engineering systems (Sahinoglu, 2007; Huffman & Antelme, 2009; Kolowrocki, 2009; Lin et al., 2010). The main idea is to represent the behavior of the given system in terms of a RBD, i.e., a graphical structure consisting of blocks and connectors (lines). For example, while assessing the reliability of computational software, the blocks may represent the computational elements, with some given failure rate, and the connectors between them may be used to describe various alternative paths required for a successful computation using the given software. Now, based on this RBD, the failure characteristics of the overall system can be judged based on the failure rates of individual components, whereas the overall system failure happens if all the paths for successful execution fail. The RBD-based analysis enables us to evaluate the impact of component failures on the overall system safety and reliability and thus is widely used for assessing the tradeoffs of various possible system configurations, such as series, parallel or a combination of both, at the system design stage.

Traditionally, the RBD-based analysis has been done using paper-and-pencil proof methods and computer simulations (Sahinoglu & Ramamoorthy, 2005). The first step in the paper-and-pencil based proof methods is to express the reliability of a sub-module in terms of its failure rate \(\lambda\) and a random variable, like exponential or Weibull random variable, which models the failure time. This information, along with the RBD of the system, is then used to analytically derive mathematical expressions for the system-level failure characteristics. Due to the involvement of manual manipulation and simplification, this kind of analysis is error-prone and the problem gets more severe while analyzing large systems. Moreover, it is possible, in fact, common occurrences, that many key assumptions required for the analytical proofs are in the mind of the mathematician and are not documented. These missing assumptions are thus not communicated to the design engineers and are ignored in the system implementations, which may also lead to erroneous designs. The RBD-based computer simulators, such as ReliaSoft (2015) and ASENT Reliability analysis tool (2014) generate samples from the exponential and Weibull random variables to model the reliabilities of the sub-modules of the system. This data is then manipulated using computer arithmetic and numerical techniques to compute the reliability of the complete system. These software are more scalable than the paper-and-pencil proof methods. However, they cannot ensure absolute correctness as well due to the involvement of pseudo-random numbers and numerical methods.

To overcome the above-mentioned inaccuracy problems, formal methods have been proposed for the RBD-based analysis as well. For example, colored Petri nets (CPN) (Rodious, Xu, Xing & Zhou, 2010) have been used to model dynamic RBDs (DRBDs), which are used to describe dynamic reliability behavior of systems. The CPN verification tools, based on model checking principles, are then used to verify behavioral properties of the DRBDs models to identify design flaws. However, due to the state-based model, only state-related property verification, like deadlock checks, is supported by this approach, i.e., we cannot verify generic reliability relationships for the given systems using the approach. On the other hand, the higher-order-logic theorem prover HOL4 can be used for RBD analysis using the probability theory available in the HOL4 theorem prover, to formalize reliability block diagrams and the exponential random variable. In the current chapter, we formalize the service, parallel, parallel-series and series-parallel RBD configurations. The parallel configuration allows us to model redundancy in the successful paths of the system and the overall system fails only if all the redundant paths fail. Thus, most of the RBDs for the real-world systems involve a combination of series and parallel configurations and the results of the current chapter allow us to formally assess the reliability of a wider range of systems. To illustrate the practical effectiveness of our work, we utilize our foundational formalization to conduct the formal reliability analysis of a cyber network and a simple oil and gas pipeline structure. In fact, given the generic nature of the proposed method, we were able to formally verify generic reliability relationships for arbitrary-node cyber network and an arbitrary-component pipeline structure and our results can be specialized to obtain the reliability of any specific network and pipeline as well.

The RBD-based analysis is based on the assumption that the reliability events, associated with the systems’ subcomponents, are mutually independent from one another. This section provides a generic formalization of ensuring mutual independence of n events and we will use it for the formalization of all the RBD configurations later.

Any two events, A and B, are termed as mutually independent iff Pr (A ∩ B) = Pr (A) Pr (B). Generally, reliability assessment of systems involves more than two random variables, i.e., Pr (∩_{i=0}^{n} L_i) = ∏_{i=0}^{n} Pr (L_i). Thus, we formalize the mutual independence of a list of random variables as (Ahmad, Hasan, Tahar & Hamdi, 2014):

### Definition 12.3

```
|- ∀ p L. mutual_indep p L = ∀ L1 n. PERM L L1 /\
2 <= n /\ n <= LENGTH L ==>
prob p (inter_set p (TAKE n L1)) =
list_prod (list_prob p (TAKE n L1))
```

### Table 1. HOL4 functions used in Definition 12.3

| Function | HOL Definition |
|---|---|
| PERM | |- ∀ L1 L2. PERM L1 L2 = ∀ x. FILTER(=x) L1 = FILTER(=x) L2 |
| LENGTH | - (LENGTH [] = 0) /\ ∀ h. LENGTH (h::x) = SUC (LENGTH x) |
| TAKE | - (∀ n. TAKE n ([]:α) = []) /\ ∀ n x xs. TAKE n (x::xs) = if n = 0 then [] else x:TAKE (n - 1) xs |
| inter_list | - (∀ p. inter_list p [] = p_space p) /\ ∀ p b t. inter_list p (b::t) = b ∩ inter_list p t |
| list_prod | - (list_prod [] = 1) /\ ∀ h t. list_prod (h::t) = h * list_prod t |
| list_prob | - (∀ p. list_prob p [] = []) /\ ∀ p h t. list_prob p (h::t) = prob p (h) * list_prob p t |
| compl_list | - (∀ p L. compl_list p L = MAP (λa. p_space p DIFF a) L) |
| min | - ∀ x y. min x y = if x ≤ y then x else y |
| min_rel | - (∀ f t. min_rel f ([]:α) = 1) /\ ∀ f b t. min_rel f (b::t) = min (f b) (min_rel f t) |

The function mutual_indep accepts a list of events L along with probability space p and returns True if the events in the given list are mutually independent in the probability space p. The formal definitions for the HOL4 functions used in the above definition are given in Table 1. The function PERM takes two lists as its arguments and makes sure that these lists form a permutation of one another. The function LENGTH returns the length of the given list. The function TAKE returns the first n elements of its argument list as a list. The function inter_set performs the intersection of all the sets in its argument list of sets and returns the probability space if the given list of sets is empty. The function list_prob takes a list of events and returns a list of probabilities associated with the events in the given list of events in the given probability space. Finally, the function list_prod recursively multiplies all the elements in the given list of real numbers. Using these functions, the function mutual_indep, given in Definition 12.3, models the mutual independence condition such that for any 2 or more events n taken from any permutation of the given list L, the property Pr (∩_{i=0}^{n} L_i) = ∏_{i=0}^{n} Pr (L_i) holds.

Next, we define a list of events constructed from a given list of random variables, such that each event models the proper functioning of a component or system at a given time based on the corresponding random variable.

### Definition 12.4

```
|- ∀ p. rel_event_list p [] x = [] ∧
|- ∀ p x h t. rel_event_list p (h::t) x =
PREIMAGE h {y | Normal x < y} ∩
p_space p :: rel_event_list p t x
```

The function rel_event_list accepts a probability space p, a list of random variables, representing the failure time of individual components, and a real number x, which represents the time index at which the reliability is desired. It returns a list of events, representing the proper functioning of all the individual components at time x.

Similarly, we can model the individual reliabilities of every random variable in a list as follows:

### Definition 12.5

```
|- ∀ p. rel_list p [] x = [] ∧
|- ∀ p h t x. rel_list p (h::t) x =
Reliability p h x :: rel_list p t x
```
