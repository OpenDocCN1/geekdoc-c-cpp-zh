
## About the Authors

![](img/67fa924962ee21b3590be9f3b10d9fe7_7_0.png)

Richard E. Neapolitan is a professor of computer science at Northeastern Illinois University. His research interests include probability and statistics, expert systems, cognitive science, and applications of probabilistic modeling to fields such as medicine, biology, and finance. Dr. Neapolitan is a prolific author and has published in the most prestigious journals in the broad area of reasoning under uncertainty. He has previously written five books, including the seminal 1990 Bayesian network text Probabilistic Reasoning in Expert Systems; Learning Bayesian Networks (2004); Foundations of Algorithms (1996, 1998, 2003, 2010), which has been translated into three languages; Probabilistic Methods for Financial and Marketing Informatics (2007); and Probabilistic Methods for Bioinformatics (2009). His approach to textbook writing is innovative; his books have the reputation for making difficult concepts easy to understand while still remaining thought-provoking.

![](img/67fa924962ee21b3590be9f3b10d9fe7_7_1.png)

Xia Jiang is an assistant professor in the Department of Biomedical Informatics at the University of Pittsburgh. She has over 13 years of teaching and research experience in Bayesian network modeling, machine learning, and algorithm design. She is the co-author of the book Probabilistic Methods for Financial and Marketing Informatics (2007). Dr. Jiang is currently focusing on developing novel algorithms/systems that improve the computational efficiency of large data analysis, and network modeling of cancer genome data.

## Contents

- Preface .................................................... xi
- About the Authors ........................................ xiii
- 1 Introduction to Artificial Intelligence .................... 1
  - 1.1 History of Artificial Intelligence ....................... 2
    - 1.1.1 What Is Artificial Intelligence? ....................... 2
    - 1.1.2 Emergence of AI ........................................ 4
    - 1.1.3 Cognitive Science and AI ............................... 4
    - 1.1.4 Logical Approach to AI ................................. 5
    - 1.1.5 Knowledge-Based Systems .............................. 6
    - 1.1.6 Probabilistic Approach to AI ........................... 7
    - 1.1.7 Evolutionary Computation and Swarm Intelligence .... 7
    - 1.1.8 A Return to HAL ........................................ 8
  - 1.2 Contemporary Artificial Intelligence ..................... 8
- I Logical Intelligence ....................................... 11
  - 2 Propositional Logic ........................................ 13
    - 2.1 Basics of Propositional Logic ............................ 14
      - 2.1.1 Syntax ................................................. 14
      - 2.1.2 Semantics .............................................. 16
      - 2.1.3 Tautologies and Logical Implication .................... 20
      - 2.1.4 Logical Arguments ...................................... 22
      - 2.1.5 Derivation Systems ................................... 25
    - 2.2 Resolution ............................................... 28
      - 2.2.1 Normal Forms ........................................... 28
      - 2.2.2 Derivations Using Resolution ........................... 31
      - 2.2.3 Resolution Algorithm ................................... 34
    - 2.3 Artificial Intelligence Applications ..................... 35
      - 2.3.1 Knowledge-Based Systems ................................ 35
      - 2.3.2 Wumpus World ......................................... 48
    - 2.4 Discussion and Further Reading ......................... 56
- 3 First-Order Logic .................................... 61
  - 3.1 Basics of First-Order Logic ........................ 62
    - 3.1.1 Syntax ............................................ 62
    - 3.1.2 Semantics ......................................... 65
    - 3.1.3 Validity and Logical Implication ............... 69
    - 3.1.4 Derivation Systems .............................. 71
    - 3.1.5 Modus Ponens for First-Order Logic ........... 75
  - 3.2 Artificial Intelligence Applications ............. 79
    - 3.2.1 Wumpus World Revisited ........................ 79
    - 3.2.2 Planning ........................................ 80
  - 3.3 Discussion and Further Reading ................... 84
- 4 Certain Knowledge Representation ................... 89
  - 4.1 Taxonomic Knowledge .............................. 90
    - 4.1.1 Semantic Nets .................................. 90
    - 4.1.2 Model of Human Organization of Knowledge .... 92
  - 4.2 Frames ........................................... 92
    - 4.2.1 Frame Data Structure ........................... 92
    - 4.2.2 Planning a Trip Using Frames ................. 93
  - 4.3 Nonmonotonic Logic ............................... 96
    - 4.3.1 Circumscription ................................ 96
    - 4.3.2 Default Logic .................................. 97
    - 4.3.3 Difficulties ................................... 99
  - 4.4 Discussion and Further Reading ................. 99
- II Probabilistic Intelligence ........................ 101
- 5 Probability ........................................ 103
  - 5.1 Probability Basics ............................... 106
    - 5.1.1 Probability Spaces ............................. 106
    - 5.1.2 Conditional Probability and Independence ..... 109
    - 5.1.3 Bayes' Theorem ................................. 112
  - 5.2 Random Variables ................................. 113
    - 5.2.1 Probability Distributions of Random Variables ... 113
    - 5.2.2 Independence of Random Variables ............. 118
  - 5.3 Meaning of Probability ........................... 122
    - 5.3.1 Relative Frequency Approach to Probability ... 122
    - 5.3.2 Subjective Approach to Probability ........... 125
  - 5.4 Random Variables in Applications ............... 127
  - 5.5 Probability in the Wumpus World ................ 131
- 6 Uncertain Knowledge Representation ............... 137
  - 6.1 Intuitive Introduction to Bayesian Networks .... 139
  - 6.2 Properties of Bayesian Networks ................ 142
    - 6.2.1 Definition of a Bayesian Network ............. 142
    - 6.2.2 Representation of a Bayesian Network ......... 145
  - 6.3 Causal Networks as Bayesian Networks ........... 148
    - 6.3.1 Causality .................................... 148
    - 6.3.2 Causality and the Markov Condition ......... 149
    - 6.3.3 Markov Condition without Causality ......... 154
  - 6.4 Inference in Bayesian Networks ................. 154
    - 6.4.1 Examples of Inference ...................... 155
    - 6.4.2 Inference Algorithms and Packages .......... 157
    - 6.4.3 Inference Using Netica ..................... 159
  - 6.5 Networks with Continuous Variables ............. 161
    - 6.5.1 Gaussian Bayesian Networks ................. 161
    - 6.5.2 Hybrid Networks ............................ 163
  - 6.6 Obtaining the Probabilities .................... 165
    - 6.6.1 Difficulty Inherent in Multiple Parents .... 166
    - 6.6.2 Basic Noisy OR-Gate Model .................. 167
    - 6.6.3 Leaky Noisy OR-Gate Model .................. 169
    - 6.6.4 Further Models ............................. 171
  - 6.7 Large-Scale Application: Promedas .............. 171
- 7 Advanced Properties of Bayesian Network ........... 177
  - 7.1 Entailed Conditional Independencies ............. 178
    - 7.1.1 Examples of Entailed Conditional Independencies ... 178
    - 7.1.2 d-Separation ................................... 182
  - 7.2 Faithfulness ..................................... 185
    - 7.2.1 Unfaithful Probability Distributions ......... 186
    - 7.2.2 Faithfulness Condition ....................... 188
  - 7.3 Markov Equivalence ............................... 189
  - 7.4 Markov Blankets and Boundaries ................. 192
- 8 Decision Analysis .................................. 199
  - 8.1 Decision Trees ................................... 200
    - 8.1.1 Simple Examples .............................. 200
    - 8.1.2 Solving More Complex Decision Trees .......... 204
  - 8.2 Influence Diagrams ............................... 217
    - 8.2.1 Representing with Influence Diagrams ......... 217
    - 8.2.2 Solving Influence Diagrams ................... 225
    - 8.2.3 Techniques for Solving Influence Diagrams .... 225
    - 8.2.4 Solving Influence Diagrams Using Netica ...... 229
  - 8.3 Modeling Risk Preferences ...................... 234
    - 8.3.1 Exponential Utility Function ................. 234
    - 8.3.2 Assessing r .................................. 236
  - 8.4 Analyzing Risk Directly ........................ 237
    - 8.4.1 Using the Variance to Measure Risk ........... 237
    - 8.4.2 Risk Profiles ................................ 239
    - 8.4.3 Dominance .................................... 240
  - 8.5 Good Decision versus Good Outcome .............. 245
  - 8.6 Sensitivity Analysis ............................. 245
  - 8.7 Value of Information ........................... 248
