260 Knowledge Representation for Legal Applications

# 12.9. POSSIBLE FUTURE WORK

The Toolkit developed in the DHSS Demonstrator project supported many of the features that we identified as being desirable for a legal application. It was not a radical departure from existing knowledge representation paradigms, but rather represented the imposition of a discipline to the use of existing paradigms as to enforce the declarative reading and avoid some of the problems that would occur when declarativeness was violated.

It was not, however, the initial decision to implement only facilities we were clear about inevitably meant that limits of expressiveness were encountered. This section describes additional lines of work that could be pursued to remedy some of the shortcomings.

# 12.9.1. Backward chaining

Despite an intention to combine forward and backward chaining, difficulties in combining backward-chaining and hypothetical reasoning resulted in only the former being implemented, since an ATMS sits far more naturally with this style of inference, Backward chaining is useful for restricting the input data to those required to determine a given conclusion, but if hypothetical input data may be entered, and inference is restricted to paths leading to the goal (as is usual in backward chaining systems), inconsistencies in the input data (which are by definition hypothetical) may go unnoticed. One remedy, which takes particular account of the focusing nature of backward reasoning, would be to use a backward search from the goal to select the relevant input data, and to allow forward inference to occur when the data is input. The advice application implemented this strategy outside the Toolkit, and it would seem a useful extension for a variety of applications.

# 12.9.2. Rules, constraints and definitions

The limitations on the syntax of rules, though reasonable at first sight, led to unanticipated problems in their interpretation and use. While constraints did not suffer from these problems, when used for definitions they could not show the distinction between the term being defined and the terms being used in the definition. This distinction is not important to the inference mechanism, but it could be important to the user interface, and is important to the builders, validators and maintainers of the knowledge base. The ability to annotate clauses to show these distinctions would be valuable.