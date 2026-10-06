# The Representation of Law in Computer Programs

classical logic P to avoid the paradoxes of classical (material) implication and to provide a formal system that captures our intuitive understanding of 'if' (and 'not'). In this case, McCarthy also finds the model for intuitionistic logic particularly convenient for integrating the semantics of other components of his language into a single framework. The semantics and proof procedure for McCarthy's intuitionistic logic programming are presented in [McCarthy 1988a, 1988b]. [McCarthy 1988c] discusses the treatment of defaults in this system.

Syntactically, McCarthy's intuitionistic logic programs are also sets of extended define clauses A < P W. When W is a conjunction of atomic clauses (or empty) McCarthy's intuitionistic logic programming and classical logic coincide. The difference lies in the treatment of implications and negations occurring inside the conditions W.

There is much more to the Language for Legal Discourse than its intuitionistic logic core. A range of additional language features will support the representation of various basic, common sense concepts. A brief description of these other components appears in section 1.16.3.

The LEX project (next section) can be regarded as another variation on the general approach of section 1.10.1.

# 1.10. The LEX project

The LEX project is a collaborative research project between the University of Tingen and the IBM Scientific Centre in Heidelberg [Jones 1986; Haft et al. 1987]. The project develops two kinds of application: a consultation system, which gives legal advice to lawyers and helps them to prepare a case (what I have been calling a legal analysis program); and an intelligent tutor, a computer-assisted instruction system based on a representation of legal knowledge. The project is taking traffic law regulations in the German penal code as its main experimental domain.

The LEX project has emphasized the declarative nature of its representations, and the use of automated theorem-proving techniques to execute these representations in practical applications. In this respect, the project shares the motivation and nature of the presuppitions of the approach described in section 1.10.1. The LEX project, developed from research into natural language interfaces to relational databases. It differs from the approach described in the previous section in its continuing concern with natural language issues. It differs in too its specific choice of representational formalism and theorem-proving technique.

The representational formalism adopted in the LEX project is a language based on first-order predicate logic with some additional syntactic features, whose formulas are discourse representation structures [Gunther et al. 1986]. This in turn is based on the Discourse Representation Theory of Kamp [1981]. LEX provides a general-purpose parser