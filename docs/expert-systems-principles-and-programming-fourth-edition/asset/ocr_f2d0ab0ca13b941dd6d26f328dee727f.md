If not, the Markov algorithm tries lower-priority ones. Although the Markov algorithm can be used as the basis of an expert system, it is very inefficient for systems with many rules. The problem of efficiency becomes of major importance if we want to create expert systems for real problems containing hundreds or thousands of rules. No matter how good everything else is about a system, if a user has to wait a long time for a response, the system will not be used. What we really need is an algorithm that knows about all the rules and can apply any rule without having to try each rule sequentially.

A solution to this problem is the Rete Algorithm developed by Charles L. Forgy at Carnegie-Mellon University in 1979 for his Ph.D. dissertation on the OPS (Official Production System) expert system shell. The term Rete comes from the Latin word rete, which means net. The Rete Algorithm functions like a net in holding a lot of information so that much faster response times and rule firings can occur compared to a large group of IF-THEN rules which must be checked one by one in a conventional program. The Rete Algorithm is a dynamic data structure like a standard B+ tree which reorganizes itself to optimize search.

The Rete Algorithm is a very fast pattern-matcher that obtains its speed by storing information about the rules in a network in memory. The Rete Algorithm is intended to improve the speed of forward-chained rule systems by limiting the effort required to recompute the conflict set after a rule is fired. Its drawback is that it has high memory space requirements, but this is not a problem these days in which memory is so cheap. The Rete takes advantage of two empirical observations that were used to come up with its data structure:

Temporal Redundancy—The firing of a rule usually changes only a few facts, and only a few rules are affected by each of those changes.

Structural Similarity—The same pattern often appears in the left-hand side of more than one rule.

If you have hundreds or thousands of rules, it would be very inefficient for the computer to specifically check whether each rule is likely to fire. The Rete Algorithm made expert system tools practical on the slow computers of the 1970s. Today the Rete network is still important for fast execution when many rules are involved in an expert system.

Instead of having to match facts against every rule on every recognize-act cycle, the Rete algorithm looks only for changes to matches on every cycle. This greatly speeds up the matching of facts to antecedents since the static data that doesn't change from cycle to cycle can be ignored. This topic will be discussed further in the chapters on CLIPS. Fast pattern matching algorithms such as the Rete completed the foundation for the practical application of expert systems. Figure 1.7 summarizes the foundations of modern rule-based expert system technologies.

# 1.11 PROCEDURAL PARADIGMS

Programming paradigms can be classified as procedural and nonprocedural. Figure 1.8 shows a taxonomy or classification of the procedural paradigms in terms of languages. Figure 1.9 shows a taxonomy for nonprocedural paradigms.