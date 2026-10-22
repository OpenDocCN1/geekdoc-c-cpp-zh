[1] Syntactically, only type names are permitted within these contexts, so a qualified name is always assumed to name a type.

[2] Adapted from [VandevoordeSolutions], proving once and for all that C++ promotes code reuse.

[3] The terms *type-dependent expression* and *value-dependent expression* are used in the C++ standard to describe the semantics of templates, and they have an effect on several aspects of template instantiation (Chapter 14). On the other hand, the term *instantiation-dependent expression* is mainly only used by the authors of C++ compilers. Our definition of a instantiation-dependent expression comes from the Itanium C++ ABI [*ItaniumABI*], which provides the basis for binary interoperability among a number of different C++ compilers.

[4] This is part of the *two-phase lookup* rules that distinguish between a first phase when template definitions are first seen and a second phase when templates are instantiated (see Section 14.3.1 on page 249).

[5] However, the lookup is nonetheless repeated when the template is instantiated, and if a different result is produced in that context, the program is ill-formed.

[6] Braces are not entirely without problems either. Specifically, the syntax to specialize class templates would require nontrivial adaptation.

[7] Fortunately, they found out before they released the new functionality.

[8] Ironically, the first of these implementations had been developed by HP as well.