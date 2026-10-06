
# Chapter 5 The gap

# 183

7 A protein family may be considered to be a group of sequences that:

- + A share more than 50 per cent similarity.
- B share the same function.
- C have the same fold.
- D less than 30 per cent identity.

8 Homology is the acquisition of common features as a result of:

- + A gene transfer between two organisms.
- C the evolutionary process of convergence from unrelated ancestors.
- D None of the above.

9 Anfinsen's dogma states that:

- + A the native structure of membrane proteins is determined by the amino acid sequence.
- B genetic information is transferred unidirectionally in biological systems.
- C the native structure of small globular proteins is determined by the amino acid sequence.
- D genetic information is transferred bidirectionally in biological systems.

10 The three ontologies within GO define:

- + A biological pathway, cellular structure, molecular function.
- B biological process, cellular component, molecular function.
- C biological function, cellular component, molecular structure.
- D None of the above.

# 5.16 Problems

1 How many descriptive titles have carbonic anhydrase 2 (CAH2-HUMAN, P00918⁵⁵) having its 35-year journey from PIR, Swiss-Prot to UniProtKB?

2 5.11 depicts an alignment of two proteins, Q9C29_ARATH (Q9C29⁵⁶) and Q48670_9LACT (Q48670⁷⁷), published in The Plant Journal in 2007. The alignment, using Clustal⁸⁸ contains errors that result in misalignment of three key features. What are those features?

What does the alignment of these sequences like when generated using MUSCLE⁵⁹, T-Coffee⁶⁰ and Multalin⁶¹? How well do the different algorithms perform, and which gives the 'best' result justify your answer.

> ⁵⁵ http://www.uniprot.org/uniprot/P00918.txt?version=202
> ⁵⁶ http://www.uniprot.org/uniprot/Q9C29
> ⁷⁷ http://www.uniprot.org/uniprot/Q48670
> ⁸⁸ http://www.ebi.ac.uk/embblast/software/ClustalWhtml
> ⁸⁹ http://www.ebi.ac.uk/Tools/msa/muscle
> ⁶⁰ http://www.ebi.ac.uk/Tools/coffee
> ⁶¹ http://www.toulouse.in.fr/multalin/multalin.html

UniProtKB/TreMBL sequence Q23293_CAEEL (Q232936²) is described as 'Dro-Myosuppression Receptor related'; when it first entered TreMBL, however, the descriptive title of version⁶³ of the sequence was 'SIMILARITY TO MAMAMALIAN MU- AND KAPPA-TYPE OPIOID RECEPTORS'. Why do you think the title of the protein changed? Where does the DMSR annotation come from? What insights does this offer into how database annotations are derived?

Considering the same sequence (Q232936⁴) as in problem 3, use the BLAST facility in the UniProtKB entry to run a similarity search (accepting the default parameters). Select from the output (which may run over several pages) up to half-dozen sequences that have annotations other than 'putative' or 'hypothetical' (e.g., see if you can find examples of types of receptor). Then use an alignment tool to align your chosen sequences.

Now return to the UniProtKB BLAST facility and change the search database to UniProtKB/Swiss-Prot. Accepting default parameters, re-run the search, and select the top half-dozen sequences for alignment.

Are the alignments the same? What might account for any differences you observe? Does either set of results help shed light on the function of the Q23293? If so, what do you think it might be, and why?

> ⁶² http://www.uniprot.org/uniprot/Q23293.txt?version=107
> ⁶³ http://www.uniprot.org/uniprot/Q23293.txt?version=1
> ⁶⁴ http://www.uniprot.org/uniprot/Q23299

# PART 2

# Chapter 6

## Algorithms and complexity

### 6.1 Overview

In this chapter, we begin to consider how computers have been brought to bear on some of the issues we've been discussing so far. We look at how to go about trying to solve problems algorithmically (from a more conceptual perspective of what computation is capable of and), and learn that computation has some surprising limits. From there, we consider how the reality of modern computer technology affects our ability to solve problems, and, conversely, how the problems faced by bioinformaticians may not be as amenable to solution.

In this chapter, we begin to consider how computers have been brought to bear on some of the issues we've been discussing so far. We look at how to go about trying to solve problems algorithmically (from a more conceptual perspective of what computation is capable of and), and learn that computation has some surprising limits. From there, we consider how the reality of modern computer technology affects our ability to solve problems, and, conversely, how the problems faced by bioinformaticians may not be as amenable to solution.

In this chapter, we begin to consider how computers have been brought to bear on some of the issues we've been discussing so far. We look at how to go about trying to solve problems algorithmically (from a more conceptual perspective of what computation is capable of and), and learn that computation has some surprising limits. From there, we consider how the reality of modern computer technology affects our ability to solve problems, and, conversely, how the problems faced by bioinformaticians may not be as amenable to solution.

In this chapter, we begin to consider how computers have been brought to bear on some of the issues we've been discussing so far. We look at how to go about trying to solve problems algorithmically (from a more conceptual perspective of what computation is capable of and), and learn that computation has some surprising limits. From there, we consider how the reality of modern computer technology affects our ability to solve problems, and, conversely, how the problems faced by bioinformaticians may not be as amenable to solution.

In this chapter, we begin to consider how computers have been brought to bear on some of the issues we've been discussing so far. We look at how to go about trying to solve problems algorithmically (from a more conceptual perspective of what computation is capable of and), and learn that computation has some surprising limits. From there, we consider how the reality of modern computer technology affects our ability to solve problems, and, conversely, how the problems faced by bioinformaticians may not be as amenable to solution.

In this chapter, we begin to consider how computers have been brought to bear on some of the issues we've been discussing so far. We look at how to go about trying to solve problems algorithmically (from a more conceptual perspective of what computation is capable of and), and learn that computation has some surprising limits. From there, we consider how the reality of modern computer technology affects our ability to solve problems, and, conversely, how the problems faced by bioinformaticians may not be as amenable to solution.

In this chapter, we begin to consider how computers have been brought to bear on some of the issues we've been discussing so far. We look at how to go about trying to solve problems algorithmically (from a more conceptual perspective of what computation is capable of and), and learn that computation has some surprising limits. From there, we consider how the reality of modern computer technology affects our ability to solve problems, and, conversely, how the problems faced by bioinformaticians may not be as amenable to solution.

In this chapter, we begin to consider how computers have been brought to bear on some of the issues we've been discussing so far. We look at how to go about trying to solve problems algorithmically (from a more conceptual perspective of what computation is capable of and), and learn that computation has some surprising limits. From there, we consider how the reality of modern computer technology affects our ability to solve problems, and, conversely, how the problems faced by bioinformaticians may not be as amenable to solution.

In this chapter, we begin to consider how computers have been brought to bear on some of the issues we've been discussing so far. We look at how to go about trying to solve problems algorithmically (from a more conceptual perspective of what computation is capable of and), and learn that computation has some surprising limits. From there, we consider how the reality of modern computer technology affects our ability to solve problems, and, conversely, how the problems faced by bioinformaticians may not be as amenable to solution.

### 6.2 Introduction to algorithms

Most algorithms are finite sequences of well-defined instructions that transform an input to produce an output. We look at how to go about trying to solve problems algorithmically (from a more conceptual perspective of what computation is capable of and), and learn that computation has some surprising limits. From there, we consider how the reality of modern computer technology affects our ability to solve problems, and, conversely, how the problems faced by bioinformaticians may not be as amenable to solution.

Most algorithms are finite sequences of well-defined instructions that transform an input to produce an output. We look at how to go about trying to solve problems algorithmically (from a more conceptual perspective of what computation is capable of and), and learn that computation has some surprising limits. From there, we consider how the reality of modern computer technology affects our ability to solve problems, and, conversely, how the problems faced by bioinformaticians may not be as amenable to solution.

Most algorithms are finite sequences of well-defined instructions that transform an input to produce an output. We look at how to go about trying to solve problems algorithmically (from a more conceptual perspective of what computation is capable of and), and learn that computation has some surprising limits. From there, we consider how the reality of modern computer technology affects our ability to solve problems, and, conversely, how the problems faced by bioinformaticians may not be as amenable to solution.

Most algorithms are finite sequences of well-defined instructions that transform an input to produce an output. We look at how to go about trying to solve problems algorithmically (from a more conceptual perspective of what computation is capable of and), and learn that computation has some surprising limits. From there, we consider how the reality of modern computer technology affects our ability to solve problems, and, conversely, how the problems faced by bioinformaticians may not be as amenable to solution.

### 6.2.1 Mathematical computability

Stepping back from the question of how to go about computing solutions to problems, and looking at the theory of computation, various interests emerge. Without exception, the maths underpinning the observations are beyond the scope of this book. We touch on the maths simplest aspects of complexity theory (a subfield of the theory of computation) in a more practical setting in Section 6.4, but the conclusions derived from the theory are important enough to state them without the working-out.

# Not all problems are computable

Some problems simply cannot be solved, although it're rare to come across in practice. One example of a non-computable problem is described by the halting problem, which states that it's impossible to decide whether algorithms will actually complete in a finite time, or will continue running forever; for non-halting algorithms, the only way to know they won't halt is to run them and wait and see, which will obviously take forever as well. Frankly, this class of problem doesnt often make an appearance in practical terms, but it's a good starting point for the following observations.
