# Chapter 7

# Evaluation

The previous chapters defined several precise analyses which can be leveraged for security purposes. This chapter now presents empirical evidence of their practicability, scalability, and precision. First, we will evaluate the precision of our new side-effect analysis for program slicing (see chapter 2). Second, we assess the effectiveness of our improved algorithm that determines interference dependence (see chapter 3), and contrast it to previous definitions, which did not take points-to information into account.

Next, we evaluate our slicing-based definition of information flow control (see chapter 4). To thoroughly analyze practicability, we present Jif, the only implementation of an information flow type system, and compare it to our system. The gain in precision is examined by a case study with an Jif program, which we converted back to standard Java. A detailed evaluation of our IFC algorithm on a set of benchmark programs illustrates its scalability.

Finally, we present path conditions (see chapter 5). Both static path conditions for Java with its object-oriented language constructs, and dynamic path conditions for C are presented. These studies illustrate that extensions provide precise results for realistic programs.

# 7.1 Slicing Java Programs

Our initial presentation of the Java slic [HS04] aimed at an evaluation of the imprecise between an approximate modeling of parameter objects and our object trees. However, we could not learn from Liang and Harro [LH98] how k-limiting works. So we fell back to comparing our sound model without k-limiting, i. we measured the effect of omitting the dependences induced by deeper levels all-together. As a matter of fact, we found that unsound k-limiting may miss up to 90% of the correct slice. While this evaluation showed that deeper levels have great impact on slicing of Java programs, this comparison was not what we originally had in mind. But after several years we could not find a sound approximation for the missed dependences of k-limiting.

However, the Indus/Kaveri slic [JRH05] propagates an alternative approach to data dependence computation. They essentially add data dependences