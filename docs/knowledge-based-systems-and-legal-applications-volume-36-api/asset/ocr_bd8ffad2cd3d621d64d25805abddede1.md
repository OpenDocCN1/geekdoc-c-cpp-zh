# Legal Applications of KBS

This point is well discussed in [Routen 1989] and [Routen and Bench-Capon 1990]. Subsection 2 of section 79 of the United Kingdom Housing Act 1985 provides a representative example:

+   79 (2) Subsection (1) has effect subject to:-
(a) the exceptions in schedule 1 ...
(b) sections 89(3) and 90(3) ... and
(c) sections 91(2) and 93(2).

This can be catered for in substituting an explicit representation of the material contained in each of the sections referred to in the representation of section 79(2), producing a flat formalisation, that is one without any cross-reference. An approach taken in [Sergot et al 1986b], and [Bench-Capon et al. 1987]. This lessens the correspondence to the source form, and introduces inescapable redundancy. The pitfalls of this with regard to construction, validation, maintenance and use of the system are addressed at length in [Routen and Bench-Capon 1990].

An alternative approach, again compatible with existing formalisms, is to introduce predicates predicating the truth values of the cross-referenced sections. While introducing less redundancy, this again causes deviation from the structure of the source form, and has the undesirable effect of creating this deviation at the "far end" of the reference so amendments introducing new cross-references will cause nonlocal changes. What is needed is a mechanism within the knowledge representation formalism to allow such cross-references to be made explicit.

# 12.4. ADEQUACY OF EXISTING PARADIGMS

So far we have considered ways in which existing paradigms might be used to build a legal KBS. There are, however, those who would argue that there are features of the legal domain which require a representation that is specific to the legal domain: for example [Greenleaf et al. 1987], and [McCarty 1989]. Greenleaf et al. base their argument on the need for the representation to be well adapted to lawyers, who see them as the natural builders of such applications, and this means that the "form of representation must be expression in that form comes naturally to lawyers’. McCarthy’s motive is different: his belief that if legal knowledge based systems to progress beyond the limited success produced by current systems, a deep conceptual model is required. Because there are common sense categories, such as time, action, belief and permission, underlying the representation of a legal problem domain, a knowledge representation language that faithfully mirrors the structure of these categories is required. In [McCarty 1989] he proposes the basic features of such a language, which he calls Language for Legal Discourse.