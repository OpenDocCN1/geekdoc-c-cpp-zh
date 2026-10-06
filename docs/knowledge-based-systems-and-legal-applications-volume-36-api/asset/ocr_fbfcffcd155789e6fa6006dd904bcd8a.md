# 56 The Representation of Law in Computer Programs

of a new case is identical to those in some previous one, then the corresponding ratio decidendi is applied by deduction ( 'syllogism') like any other rule. Since this is not likely to happen often, Meldman has an additional 'analogy' mechanism to deal with cases which do not match exactly.

Meldman's analogy mechanism is based on a hierarchical classification of the concepts represented in his system. When the facts of a case do not match exactly the conditions of a rule in the system (expressing an established legal doctrine or the ratio decidendi of a previous case), Meldman's system uses its classification of concepts to provide an extended notion of 'matching'. A fact in a case is considered to 'match' in a rule when both are instances of a more general concept in the hierarchy. Thus 'kick' and 'hit' would match because they are instances of the more general concept 'violent physical contact'. In this way, the facts of a new case can be subsumed by the ratio decidendi of a previous, similar case. (Note that the analogy mechanism also applies to rules representing general doctrines. Since these have conditions that are already rather abstract the analogy mechanism is seldom invoked for.)

Meldman stresses that his mechanism provides only a very simplified form of analogy. (In fact it corresponds to what is sometimes called 'first-order generalization' [Reynolds 1970]. Ashley [1985] has compiled a survey of research in artificial intelligence on reasoning by analogy and discussed the applicability of these techniques to applications in law. See also [Kedar-Cababelli 1984].

Schild [1989] describes a quite different way of using the general doctrines that appear in a text like Prosser's not as deductive rules in a legal analysis program, but as a way of organizing the storage of case reports and bringing the user's attention to possibly relevant instances. What seems to have been a small student exercise, Hustler [1982] implemented a logic program based on Meldman's extracts from Prosser; he did not attempt to reconstruct Meldman's semantic network representation and directly ignored the analogy mechanism altogether.

# 1.15.1. Commentary

Meldman's early system anticipated many of the features of current legal analysis programs. The treatment of general doctrines (where others have statutes) is fairly standard. It is the treatment of individual cases that need most comment.

Meldman's approach, to represent a case by a single rule expressing its ratio decidendi, has severe limitations. (These criticisms are intended to highlight the limitations of the approach, and not as attack on Meldman's work.)

Firstly, there is the problem of determining what should be taken as