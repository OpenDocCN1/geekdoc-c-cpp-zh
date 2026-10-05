# 4 Pattern Matching

*Pattern matching* is a technology that supports the creation of domain-specific languages and other systems that should have an additive character.

Pattern matching is a generalization of equality testing. In equality testing we compare two objects to determine that they have the same structure and contents. In pattern matching, we generalize equality testing to allow some parts of the structure and contents to be unspecified. A *pattern* specifies certain parts of the data exactly, but it has "holes" (*pattern variables*) that match the unspecified parts of the data. We may impose constraints on what a pattern variable can match, and we may require that multiple instances of the same pattern variable match the same thing.

A pattern can be matched to a part of a larger datum; the context of the match is unspecified. The ability to work with partial information means that only the specified parts of the pattern are assumptions about the data matched; there are few or no assumptions about the unspecified parts.

This property of pattern matching enables the construction of very flexible rule-based systems. In a rule-based system one can add new rules to add new capabilities, though there are difficulties associated with how rules are defined and how they interact with one another. For example, if more than one rule is applicable, the results may depend on the ordering of application. We already encountered problems with the interaction of rules, in the boardgame rule interpreter. (See the critique on page 63.)

Besides the use of patterns to match data that meets a partial specification, patterns can themselves represent partially known