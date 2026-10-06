
# Legal Applications of KBS

represented. Whereas LOD analysts made KANT nodes for each proposition and logical connector, as a rule would be represented by a number of nodes, the AS knowledge base had whole rules represented in a single node. All nodes had a title field.

In nodes that contained rules, our analysis and formalisation of knowledge typically generated three other fields. The field containing the least formalized entry might contain text from the source, citation of the reference (title and page number), comments explaining these peculiarities of the knowledge, and reminders to the analysts about changes which had been made or needed to be made to the node. There was usually a field containing an English-like, semi-formal rule which was written to represent the knowledge in the original field faithfully. The third field contained the rule in the toolkit language.

The point of having the three fields juxtaposed and in the same node was to facilitate the inspection of the transformations through the three stages.

Towards the end of the project, when the facilities of KANT and KBB had been combined, an ICL colleague wrote a special 'patch' to make it also possible for our structures to have a fourth field in these nodes, one containing the compiled version of the rule. This meant we were able to inspect the rule we actually contained and compare it to the one we sent to the compiler. This enabled us to identify where, for mistakes in placing parentheses propositions had been disregarded by the compiler. It was far easier to detect these truncated rules through inspection than through the creation and running of test examples.

A complex system of KANT structures was developed. It was able to serve as a 'progress chasing'/version control tool. It was able to show increasingly fine granularity of rules, i.e. where propositions in one rule were elaborated by other rules representing the original rule and all which refined their proposition. Other structures were designed so that refining rules were 'children' of the top-level rule. Links were made between nodes where terms with crucial technical/legal meanings were used and nodes containing definitions for these terms. An effective glossary was theirs. It served not only to explain the meaning of terms but also as a check that the same meaning permeated throughout.

In some cases it was possible to make links between the original source material and nodes which made use of that material. We had not been given permission to make an on-line version of the CPAG handbook, so a reference to the books was given when material from that source was first introduced.

It's fair to say that KANT and KBB provided extremely useful flexible tools which allowed analysts with different working styles and personal preferences to co-operate effectively in the analysis and construction of our knowledge base. We did have an on-line 'KANTified' version of How to Claim State Benefits and so were able to make links between material in that source and versions of it used for the system.

# 11.6. CONCLUSIONS

A variety of analyses were undertaken. A variety of strategies for developing knowledge bases were adopted. The domain knowledge-bases which came into being each had its own character although the language for their formal expression was the same. This breadth of experience has been a strength of the project, allowing a number of lessons to be learned.

# CHAPTER 12

# KNOWLEDGE REPRESENTATION
 FOR LEGAL APPLICATIONS

Trevor Bench-Capon and Justin Forder

# 12.1. INTRODUCTION

The choice of knowledge representation is a crucial decision that must be taken when designing knowledge based systems, including those in the legal area. Over the years a number of paradigms for knowledge representation have become well established, and have been used to get good effect across a range of different application domains. In fact, all these major paradigms have been used for legal applications: an examination of the literature will disclose KBS based on production rules, various kinds of structured objects as frames and semantic networks, and first-order predicate calculus, as well as mixtures. In all such systems, techniques developed for general use were straightforwardly applied to the legal domain, and many of these applications can be seen as successful to a degree. Experience has shown, however, the paradigms have practical differences that make them particularly suited to some areas and styles of applications. In this chapter we shall consider the demands placed upon knowledge representation by legal applications, and discuss how this should affect the way in which the knowledge representation task is tackled. First we shall consider how the application area impinges on a KBS through the life cycle of the KBS. Next we shall consider whether there are particular features of the domain which render the existing paradigms inadequate, and whether the claims made by [Greenleaf et al. 1987] and McCarty [1989] to the effect that special purpose knowledge representation techniques are required for the

# Knowledge Representation for Legal Applications

legal domain is justified. We shall then present the knowledge representation formalism developed for use within the three of the applications of the DHSS Demonstrator project, so as to illustrate our earlier conclusions, and indicate some of the problems encountered and areas where we consider further work necessary.

# 12.2. PHASES IN A LEGAL KBS AND CONSEQUENCES FOR
# KNOWLEDGE REPRESENTATION

Like any software application a KBS has a life cycle which includes the construction of the system, the testing of the system and the period of use, maintenance and enhancement. In each of these phases the fact that an application is in the domain of law will have considerable influence. It is that influence will be considered in this section.

When constructing a KBS, it is necessary to consider the sources of knowledge available about the domain, and the nature of the knowledge to be represented. In the legal area a distinctive feature is the amount of knowledge that exists in written form. Not only may there be legislation itself, setting out the letter of the law, but there may also be reports of decisions made by adjudicators, perhaps transcripts giving the arguments presented by counsel, and commentaries and textbooks designed to instruct people in the law for a particular area. In many other fields, we cannot find texts corresponding to all of these categories. In the area of medical diagnosis systems, for example, we will find textbooks describing the symptoms and treatment of various diseases, and perhaps case histories as well, but there will be nothing corresponding to the legislation. For while the medical diagnosis system is ultimately about a real system, the human body, the legal KBS is ultimately about a conceptual system enshrined in legislation. The result of this is that the texts themselves need not to be taken seriously in a legal application in a way in which they do not in a medical diagnosis application. It actually matters whether a legal case is real or hypothetical, and whether case acts as a basis for a partial view of what the law is. Similarly it matters what the legislation says because the relationships and concepts underide their existence to this legislation. Any formalism for legal knowledge representation needs to be well adapted to the representation of these texts.

Of course, there exist examples of legal KBS which do not represent legal at all, or only to a rudimentary extent: McCarty's TAXMAN, described in [McCarty 1977], and Rissland and Ashley's HYPO, described in [Rissland and Ashley 1987], would provide notable examples. The explanation for this is that this kind of system is motivated by a consideration rather different than present in the majority of legal KBS. These systems set out to model the reasoning of lawyers, focusing on the way in which a single point of law may be
