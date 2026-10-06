
# The Representation of Law in Computer Programs

## 1.4.4. Open texture

At this point I introduce the notion of open texture, for this is a term which is frequently encountered in the literature, and is the main concern of many of the projects to be discussed.

In any new case we cannot say with certainty what its outcome will be. Statutes and case law may provide good guidelines, but it is always possible that a court will decide otherwise. We know whether a legal concept applies to cases which have been decided by a court. But we have no way of determining with certainty whether a legal concept holds in a new case, except by taking the case before a court. Until the case has been decided in court, there is no fact of the matter. Legal concepts are therefore 'pointwise defined' and are said to exhibit open texture: a legal concept has a precise definition only for those cases which have been decided by a court at the appropriate level of authority; there is no precise definition of the concept for cases which have still to come to court.

Vague and discretionary concepts in law are most obviously open textured. But even legal concepts which appear to be precisely defined in a statute or code exhibit open texture. However however precise definition might seem, it is always possible that a court will decide to take a different interpretation of the statute, or decide there some good reason why the statute should not be applied in a new case.

The notion of open texture has its origins in the philosophy of language, but it is in jurisprudence that this notion has become most useful. The legal philosopher Hart, who argues that legal concepts are incurably open textured [Hart 1961]. Hart's views, however persuasive and very influential, have not been universally accepted. Dworkin [1967], for example, argues that there is no open texture in law, because any case, no matter how abstuse, is decided by the proper process of legal reasoning and argumentation. These are philosophically interesting positions, but the debate seems to have no practical significance. There is no dispute about what processes a court should use in coming to its decision. In practice, the concepts of law are incurably open textured (if you follow Hart) or behave as if they were incurably open textured (if you follow Dworkin, say). Open texture in law, which is fairly standard way of characterizing the fundamental uncertainty in law, is eliminated only when a case comes to court and a definition is given.

## 1.4.5. Fixed interpretations of the law

A classification of projects which distinguishes between statutes and case law is not ideal, partly because it can suggest that one is fundamentally more certain in its outcome than the other, and partly because some projects attempt to reason with both sources of law. I think that a better classification would distinguish systems that represent a single, fixed interpretation of the legal sources constructed in advance, and systems that attempt to be more flexible in their interpretation of the original sources.

The distinction can be made clearer if we take the following, simplified model of what is involved in determining whether a legal concept applies in a given case:

- 1. Identify relevant facts.
- 2. Construct legal rule from relevant legal sources.
- 3. Apply legal rule to relevant facts.

The stages are not distinct, of course, but are bound together inextricricably. In order to determine what the relevant facts are, we must first have some idea of what legal rules are relevant and where we can find them. Further, we would normally be interested in identifying those legal rules which apply to the facts in a particular way, for example in a way that is most favourable to the interests of a client; and once a suitable rule is identified and ready to be applied, this will turn determine what facts in a case are relevant.

I am making no claim, therefore for the accuracy of the simplified model. Its purpose is merely to provide a basis for classifying projects into various categories. Further, 'rule of law' in any strict sense de, but is intended to encompass all that might be deemed relevant. I include in this even the judge's personality or what he ate for breakfast or the opinion of his six-year-old daughter if these are considered to have a bearing on the outcome of a given case.

Examined in terms of this simple model, most of the projects to be considered simplify matters still further. They assume, or rather pretend, that 'relevant sources of law' have been identified and that legal rules have been constructed from them. That is, they incorporate a single, fixed representation of the law constructed in advance, and they concentrate on applying this fixed representation to a variety of fact situations.

It is true that most of these systems consider only statutes and explicitly written rules and regulations. If a fixed representation is of much practical value, there must be some reasonable consensus that the representation is an accurate model of the law. There is less doubt about the accuracy of a model based on certain kinds of statute than based on sources of law which are more open to alternative interpretation, or where there is some doubt about which legal sources are relevant.

Further, the majority of projects to be considered implement a form of deductive reasoning with rules, and these rules are usually derived from statutes. Computational techniques for mechan reasoning is relatively well understood While applying the provisions of a statute can often be seen as deduction, to a first approximation at least, reasoning with cases is harder. Reasoning with cases resembles inductive or logical inference more than it does deduction (though this does not imply that such reasoning is non-logical). Reasoning with cases (or statutes which are open to many different interpretations) cannot be approximated realistically by identifying all relevant legal sources and deciding in advance how they should be interpreted and applied. Identifying previous cases and interpreting the significance of their decisions according the context of a new case is where the essential problem lies, and a system which eliminates this path altogether is of little or no value.

It should be noted that no project to my knowledge has attempted to reason directly with the sources of law. Reasoning directly with the sources of law would require a computer program that could understand natural language at a level of sophistication that is well beyond the capabilities of any system that could be constructed in the foreseeable future (or ever). Those projects which attempt to reason with case law must devise some suitable abstraction and representation of the original sources, one which is flexible enough to allow some of the interpretation to be delayed and only undertaken by the system as the context of a new requires. What characterizes case-based reasoning is the need to leave part of the interpretation of sources to the system itself, but successful techniques for this could be applied to statute law as well.

## 1.5. MODELS OF LEGAL EXPERTISE

This section describes two systems developed by Don Waterman and Mark Peterson (LDS and SAL), Robert Michaels's TAXADVISOR system, and Philip Capper and Richard Suskind's Latent Damage System. All of them are examples of legal expert systems, in the strictest meaning of that term. Waterman and Peterson's approach will be examined in most detail. Their systems are unusual in that they attempt to address all aspects of the legal decision-making process.

## 1.5.1. Waterman and Peterson

The Legal Decision making System (LDS) is a system developed by Don Waterman and Mark Peterson which addresses the problem of settling product liability cases [Waterman and Peterson 1980, 1981, 1984; Peterson and Waterman 1985; see also Cook et al. 1981]. Given such a case, the system determines the defendant's liability, and then calculates the value of the case, which is the amount that would be acceptable to all parties as a fair settlement of the case.

The knowledge represented in LDS is both of a formal kind based
