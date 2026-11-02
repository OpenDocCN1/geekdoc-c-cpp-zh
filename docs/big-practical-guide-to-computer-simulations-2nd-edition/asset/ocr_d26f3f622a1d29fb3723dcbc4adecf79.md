# The Utility of Knowledge in Inductive Learning

# K. Branting

Department of Computer Science, University of Waterloo, Waterloo, Ontario N2L 3G1, Canada

Abstract. A primary motivation for `hybrid' learning systems is that domain knowledge can reduce the number of training instances needed for inductive learning. However, no formal account has yet been proposed of the relationship between domain knowledge and inductive bias. This paper presents a formal framework for analyzing the utility of knowledge in inductive learning that is based on the notion of inductive bias as a partial ordering over hypotheses. For concrete illustration, the framework is applied to a connectionist learning system.

1 Introduct on

The utility of domain knowledge in inductive learning is an issue of widespread interest. In many learning tasks, only a limited number of training instances are available, and some form of pre-existing knowledge may be the only means of adequately constraining the induction. For this reason, `hybrid' learning systems have been proposed that combine some form of domain knowledge with inductive learning from training instances. Many such systems have been shown experimentally to achieve higher predictive accuracy on tasks in their domains than purely inductive systems (see Section 5). However, there is as yet no formal account of why domain knowledge is useful in induction.

This paper proposes a framework for analyzing the utility of domain knowledge in inductive learning. The framework is based on a formalization of inductive bias as a partial ordering over hypotheses. The claim to be established is that the prior knowledge, or bias, of a learning system affects the number of training instances required to identify a target hypothesis. In particular, for a class of learning systems which are consistent Bayes classifiers it can be shown that a system whose bias is a stronger ordering on a class of hypotheses requires fewer instances to identify a target hypothesis than a. system that has a weaker ordering.

For concreteness, this analysis of bias is applied to the `recursive sigmoidal' network of [2], a novel connectionist architecture. The recursive sigmoidal network can be given a prior ordering on hypotheses with a direct connectionist interpretation, and, for such prior orderings, a bound on the number of instances needed for learning can be determined. This provides a theoretical basis for the experimentally-demonstrated utility of initial connectionist knowledge.

The plan of this paper is as follows. Section 2 defines the form of inductive learning and inductive bias to which this analysis applies. Section 3 describes the recursive sigmoidal network of [2]. Section 4 uses the framework of Sections 2 and 3 to derive a sample bound for recursive sigmoidal networks. Section 5 discusses related and future work, and Section 6 presents some conclusions.