position in the vector corresponds to a feature of the individual. However, the features are considered to be behavioral rather than structural.

Evolution Strategies (ESs) are in many ways very similar to Genetic Algorithms (GAs). As their name implies, ESs too simulate natural evolution. The differences between GAs and ESs arise primarily because the original applications for which the algorithms were developed are different. While GAs were designed to solve discrete or integer optimization problems, ESs were applied first to continuous parameter optimization problems associated with laboratory experiments. ESs differ from traditional optimization algorithms in a few aspects:

+   - ES search between populations, rather than between individuals.
+   - The objective function information is sufficient, derivatives are not required.
+   - The transition rules used by ESs are probabilistic, not deterministic.

The reproduction process in an ES is only by mutation. To apply mutation, the Gaussian mutation operator is made use of. Sometimes an intermediate recombination operator is used, in which the vectors of two parents are averaged together, element by element, to form a new offspring (see Figure 11.9).

These operators reflect the behavioral as opposed to structural interpretation of the representation since knowledge of the values of vector elements is used to derive new vector elements.

Compared to GA and GP, the selection of parents to form offspring is less constrained, since the string representation is simple. Due to this nature of the representation, it is easy to average vectors from many

| Parent 1 | 0.2 | 0.6 | 0.9 | 1.5 |
|---|---:|---:|---:|---:|
| Parent 2 | 1.0 | 0.8 | 0.7 | 0.5 |

![](bbox=[0.458, 0.773, 0.488, 0.819])

| Offspring | 0.6 | 0.7 | 0.8 | 1.0 |

**FIGURE 11.9:** Intermediate Recombination of Parents