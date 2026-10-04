# CHAPTER 2 DEPENDENCE GRAPHS AND SLICING
OBJECT-ORIENTED LANGUAGES

+   - control flow can reach $n_2$ after $n_1$ via a path in the CFG along which is
o intervening definition of $f$

With this definition, we get the precise slice in Figure 2.10 without expensive replacement strategies just by inspecting the reaching definitions of the last line, which contains both assignments to the $y$ field. With the
flow-sensitivity in pointer analysis gained by SSA form, the criterion will be determined data dependence only on the definition in line 6. While this last definition of dependence is always field-sensitive, its precision relies heavily on the precision of the underlying alias analysis.

# 2.5 Interprocedural Dataflow-Analysis

For interprocedural analysis, a conservative approximation is required for how a program manipulates its data at the call-graph level. For program slicing, this mainly covers what side-effects a method$^5$ may impose on its parameters$^6$. Side-effects of called methods produce new definitions that may reach a use and thus require data dependencies. Algorithms to compute such side-effects are known in the literature [Ban79, Muc97], but they are presented for procedural languages only, without covering extensive use of objects and their fields. Side-effect analysis for multi-level pointers [LLS01] is, however, too infiltrate for representing objects slicing [L496, L498]; their approaches either have flaws or do not handle nested objects conservatively. [TAFM97] already noted that points-to-information is a prerequisite for precise side-effect analysis of oriented languages. The following section will present a new approach for putting a conservative approximation of the side-effects of methods and their invoked methods that allow context-sensitive slicing of objects. It allows field-sensitive slicing and takes placing aliasing into account.

To field-sensitive analysis also in the interprocedural case, we need to explicitly represent all the fields of parameter objects and accessed values at the method entry nodes and call sites [FS91]. This corresponds to the non-virtual scalar replacement strategy in the intra-procedural case (see section 2.4.3)

In analogy to previous work [Ban79, Muc97] we characterize side-effects as two to the set of locations they may access. A memory location is an abstract of a cell in the heap and is represented as a sequence of fields$^7$ rooted at a pointer of the given method, such that dereferencing the fields in the lists yields a pointer to the abstract location. For example, if an object may be accessed with the expression $a.f$ from the parameter $a$, then $a.f$ is an abstract location for the memory storing that object. While this representation is not necessarily unique, it is sufficient for our algorithm. We

> $5$The object-oriented term method be used instead of procedure in the sequel
$^6$As static variables are modeled as extra parameters in SDGs the parameter will cover both normal parameters and synthetic ones for static variables in the sequel
$^7$To achieve disambiguation, the fully qualified field name must be used.

50