# The Representation of Law in Computer Programs

reasoning is relatively well understood While applying the provisions of a statute can often be seen as deduction, to a first approximation at least, reasoning with cases is harder. Reasoning with cases resembles inductive or logical inference more than it does deduction (though this does not imply that such reasoning is non-logical). Reasoning with cases (or statutes which are open to many different interpretations) cannot be approximated realistically by identifying all relevant legal sources and deciding in advance how they should be interpreted and applied. Identifying previous cases and interpreting the significance of their decisions according the context of a new case is where the essential problem lies, and a system which eliminates this path altogether is of little or no value.

It should be noted that no project to my knowledge has attempted to reason directly with the sources of law. Reasoning directly with the sources of law would require a computer program that could understand natural language at a level of sophistication that is well beyond the capabilities of any system that could be constructed in the foreseeable future (or ever). Those projects which attempt to reason with case law must devise some suitable abstraction and representation of the original sources, one which is flexible enough to allow some of the interpretation to be delayed and only undertaken by the system as the context of a new requires. What characterizes case-based reasoning is the need to leave part of the interpretation of sources to the system itself, but successful techniques for this could be applied to statute law as well.

# 1.5. MODELS OF LEGAL EXPERTISE

This section describes two systems developed by Don Waterman and Mark Peterson (LDS and SAL), Robert Michaels's TAXADVISOR system, and Philip Capper and Richard Suskind's Latent Damage System. All of them are examples of legal expert systems, in the strictest meaning of that term. Waterman and Peterson's approach will be examined in most detail. Their systems are unusual in that they attempt to address all aspects of the legal decision-making process.

# 1.5.1. Waterman and Peterson

The Legal Decision making System (LDS) is a system developed by Don Waterman and Mark Peterson which addresses the problem of settling product liability cases [Waterman and Peterson 1980, 1981, 1984; Peterson and Waterman 1985; see also Cook et al. 1981]. Given such a case, the system determines the defendant's liability, and then calculates the value of the case, which is the amount that would be acceptable to all parties as a fair settlement of the case.

The knowledge represented in LDS is both of a formal kind based