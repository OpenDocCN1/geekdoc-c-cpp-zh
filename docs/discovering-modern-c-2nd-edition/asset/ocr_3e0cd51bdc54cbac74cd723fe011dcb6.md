> "Gray, dear friend, is all theory and green the life's golden tree."¹⁷
> 
> —Johann Wolfgang von Goethe

17. Author's translation. “Grau, teurer Freund, ist alle Theorie und grün des Lebens goldner Baum.”

In the previous sections, you might have gotten the impression that template parameters can be substituted by any type. This is in fact not entirely true. The programmer of template classes and functions makes assumptions about the operations that can be performed on the template arguments.

Thus, it is very important to know which argument types are acceptable. We have seen, for instance, that accumulate in Listing 3-4 can be used with vectors or lists of int or double. However, value types without addition like file streams cannot be used with accumulate. What should be accumulated from a set of files?

Therefore, we have to find the set of requirements for potential argument types. Such sets are called Concepts. A concept CR that contains all requirements of concept c and possibly additional requirements is called a Refinement of c. In the standard this is called Subsumption: CR subsumes c. The definition of subsumption is however more general: a concept c2 subsuming c1 does not necessarily mean that the definition of c2 contains c1 plus potentially more requirements. It rather means that the set of requirements in c2 are a superset of c1’s requirements (after according renaming and other equivalences). The formal specification of concept subsumption is found in the standard [39, §13.5.4] and in online references. A type t that holds all requirements of concept c is called a Model of c. Regarding subsumption: if c2 subsumes c1 the models of c2 are a subset of those from c1.

A concept can contain purely syntactic requirements such as a certain type parameter must have a copy constructor or an operator+. A semantic requirement specifies a mandatory property like commutativity of the addition: x + y = y + x ∀ x, y.

Before C++20, concepts existed only in the documentation (if at all) and the users of generic functions and classes were responsible to fulfill all requirements on template parameters. If a syntactic requirement was violated, the user would see it for instance by the compiler’s complaint