
Once we select from the collection of possible rules, for each antecedent the consequent corresponding to the fuzzy rule with the great weight w_ij, we need to generate finally fuzzy sets in each of the domains of the input variables. These fuzzy sets will be obtained by means of projecting the fuzzy clusters of the input space in each domain of the variables, then making the extensional hull of the fuzzy sets obtained, and finally we approximate them by trapezoidal fuzzy sets. As a consequence of this method we have a collection of k1 * k2 fuzzy rules:
R_h : If x1 is A1h and ... and xp is Aph then y is Bh, h = 1, ..., k1 * k2.

So, basically, each method has to:

- 1. Define the number of rules to be created.
- 2. Set the centers of the A_jh fuzzy numbers that constitute the antecedent of the rules.
- 3. Define the membership degree μ_Ajh(x_j) to be used.
- 4. Set the output value (v_j).

## 3.4.4 A Genetic Algorithm Based Method to Generate and/or Tune Fuzzy Rules

The fuzzy modeling normally is accomplished by a two step procedure. The first step is generation of a first approximation to the fuzzy model that describes the system. Implicit in this step is the determination of the necessary number of rules. The output of this step is a collection of rules which can be seen as rough estimates of the final rule base. The second step consists of a tuning of the initial rough rules to give us our final rule base.

Genetic Algorithms (GAs) have shown good results in obtaining fuzzy rule bases, although normally using different GAs in the generation and in the tuning process, or just using GAs only in one of these steps [33] [37]. We have defined an agent that implements a nonstandard GA to achieve either of the following tasks:

- 1. Only tuning: GA is used to tune a rule base with k rules (previously obtained by means of an expert or using the fuzzy clustering agent for rule generation). The final rule base will contain exactly k rules.
- 2. Generating and tuning: GA is used in this case to generate and to tune a rule base directly from data. It is also possible to incorporate an initial rule base with k rules as in the previous method, that “help” the search process. Final rule base will contain any number N of rules, with 1 ≤ N ≤ MAX, where MAX is given by user.

Genetic Algorithms (GAs) [27] [44] are adaptive procedures of optimization and search that find solutions to problems by an evolutionary process inspired in the mechanisms of natural selection and genetics. Currently, these algorithms are being highly considered above all in those problems with complex solution spaces for those which we do not have good algorithms to solve them.
Next, we describe the main characteristics of the GA:

## Representation

The number of rules is known and constant if the proposal is to tune a previous rule base with a fixed number k of rules, but it is unknown and variable (N ∈ [1..MAX]) if we want to achieve processing completely, i.e., “generating and tuning” task. Firstly, we show a possible representation of the solutions to generate and tune a rule base, and we will see how this representation can be used to tune a rule base introduced previously (“only tuning” task).

Populations in this GA are composed of individuals H_i, i = 1, …, popsize, represented as follows:

## Individual H_i :

R_1^i R_2^i … R_MAX^i  d_1^i d_2^i … d_MAX^i
Rule set          Control set

where the rule R_h^i = {Ã_h^{i1} Ã_h^{i2} … Ã_h^{ip} B̃_h^i} (1 ≤ h ≤ MAX, 1 ≤ i ≤ popsize) consists of fuzzy values for the p input variables and output variable, which are represented as:

Ã_h^{ij} = (a_{h1}^{ij}, a_{h2}^{ij}, a_{h3}^{ij}, a_{h4}^{ij}),  (1 ≤ h ≤ MAX, 1 ≤ i ≤ popsize, 1 ≤ j ≤ p)
B̃_h^i = (b_{h1}^i, b_{h2}^i, b_{h3}^i, b_{h4}^i),      (1 ≤ h ≤ MAX, 1 ≤ i ≤ popsize)

i.e., trapezoidal fuzzy numbers with a_{hl}^{ij}, b_{hl}^i ∈ R, (1 ≤ h ≤ MAX, 1 ≤ l ≤ 4, 1 ≤ i ≤ popsize, 1 ≤ j ≤ p). Values d_h^i ∈ {0,1} (1 ≤ h ≤ MAX, 1 ≤ i ≤ popsize) indicate if rule h of the individual i is active in the solution (1 = active, 0 = inactive). Thus, the number N of rules in the individual i is given by the number of values d_h^i = 1, 1 ≤ h ≤ MAX.

Note that a control set is not necessary if we want to tune a previous rule base with a fixed number k of rules.

## Initial Population

To create an initial population we take into account two criteria:

- 1. Explore available information (examples, rule bases, etc.).
- 2. Explore (randomly) solution space to obtain an appropriate diversity.

According to these criteria, we propose three different alternatives (F1, F2 and F3) to initialize the solutions, which will be applied with probabilities p1, p2 and p3 respectively. F1 and F2 forms assume the existence of an initial rule base with k rules (1 ≤ k ≤ MAX).

(F1) All k rules of the initial rule base are introduced in random positions of the solution, and corresponding values in the control set are set to 1. Remainder rules (MAX − k) are obtained randomly according to the domains of input and output variables, and corresponding values in the control set are set to 0.
Example:
Initial rule base (k = 4):
R1 R2 R3 R4
Initial solution (MAX = 7):
Rnd R3 R2 Rnd R1 R4 Rnd 0 1 1 0 1 1 0
where Rnd denote that a rule has been obtained randomly. Although other approaches can be used to obtain randomly fuzzy rules, we propose the following:
For each trapezoidal fuzzy number ũ = (u1, u2, u3, u4) do
Step 1. Δ ← (b − a)/(m − 1);
Step 2. u1 ← random real number ∈ [a − Δ, b + Δ];
u2 ← random real number ∈ [u1, b + Δ];
u3 ← random real number ∈ [u2, b + Δ];
u4 ← random real number ∈ [u3, b + Δ];
where [a,b] is the domain of the variable, and m is the number of linguistics values associated with a variable (typically seven).

(F2) Each rule of the solution, with equal probability, either is selected from the initial rule base or is obtained randomly. All values in the control set are generated randomly.
Example:
Initial rule base (k = 4):
R1 R2 R3 R4
Initial solution (MAX = 7):
R2 Rnd Rnd R4 Rnd R1 Rnd 1 0 1 0 1 1 1

(F3) All MAX rules of the solution and all values in the control set are obtained randomly.
Example:
Initial solution (MAX = 7):
Rnd Rnd Rnd Rnd Rnd Rnd Rnd 0 1 0 1 1 0 1

## Genetic Operators

Since solutions contain two different types of information (denoted as rule set and control set) it is necessary to use different genetic operators to achieve completely the recombination process. We have used the following genetic operators:

- **Rule set genetic operators**
  - *Simple crossover*
  - *Arithmetical crossover*
  - *Max-Min crossover*
  - *Simple mutation*
  - *Non-uniform mutation*

- **Control set genetic operators**
  - As control set is a bit string, simple binary crossover and mutation [27] are used in this case.

## Parameters

The most significant parameters used by GA have been maximal generation number ($T$), population size ($popsize$), probabilities F1, F2 and F3 used in obtaining initial population ($p_1$, $p_2$ and $p_3$, respectively), probability of crossover ($p_c$) and probability of mutation ($p_m$). Note that to achieve the generating and tuning task when there is no initial rule base, it is necessary to set $p_1 = 0$, $p_2 = 0$ and $p_3 = 1$ in obtaining initial population. Note also that probabilities $p_c$ and $p_m$ correspond to the sums of the probabilities of all crossover and mutation operators respectively described above.

## 3.5 Robotics Application Example

## 3.5.1 Introduction

The operation of a mobile autonomous robot in an unstructured environment, as it occurs in the real world, needs to take into account many details. Mainly, the controller has to be able to operate under conditions of imprecision and uncertainty. For instance, the a priori knowledge of the environment, in general, is incomplete, uncertain, and approximate. Typically, the perceptual information acquired is also incomplete and affected by the noise. Moreover, the execution of a control command is not completely reliable due to the complexity and unpredictability of the real world dynamics. To cope with these difficulties, the controller should respond reactively to unpredicted events as soon as they are perceived.
