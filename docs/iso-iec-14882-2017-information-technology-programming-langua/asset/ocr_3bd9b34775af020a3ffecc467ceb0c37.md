# ISO/IEC 14882:2017(E)

[Example: If an object of type std::vector<int> is in a valid but unspecified state, x.empty() can be called unconditionally, and x.front() can be called only if x.empty() returns false.— end example]

# 20.4 Method of description (Informative) [description]

1 This clause describes the conventions used to specify the C++ standard library. 20.4.1 describes the structure of the normative Clauses 21 through 33 and Annex D. 20.4.2 describes other editorial conventions.

# 20.4.1 Structure of each clause [structure]

# 20.4.1.1 Elements [structure.elements]

1 Each library clause contains the following elements, as applicable:155

+   - (1.1) Summary
- (1.2) Requirements
- (1.3) Detailed specifications
- (1.4) References to the C standard library

# 20.4.1.2 Summary [structure.summary]

1 The Summary provides a synopsis of the clause, and introduces the first-level subclauses. Each clause also provides a summary, listing the headers specified in the subclause and the library entities provided in each header.

2 Paragraphs labeled "Note(s):" or "Example(s):" are informative, and other paragraphs are normative.

3 The contents of the summary and the detailed specifications include:

+   - (3.1) macros
- (3.2) values
- (3.3) types
- (3.4) classes and class templates
- (3.5) functions and function templates
- (3.6) objects

# 20.4.1.3 Requirements [structure.requirements]

1 Requirements describe constraints that shall be met by a C++ program that extends the standard library. Such extensions are generally one of the following:

+   - (1.1) Template arguments
- (1.2) Derived classes
- (1.3) Containers, iterators, and algorithms that meet an interface convention

2 The string andostream use an explicit representation of operations required of template arguments. If you use a template class_traits to define these constraints.

3 Interface conventions are stated as generally as possible. Instead of stating class X has to define a member function operator=(), the interface requires "for any object of class X, ++x is defined". That is, whether the operator is unspecified.

4 Requirements are stated in terms of well-defined expressions that define a table of types that satisfy the requirements. For every set of well-defined requirements there is a table that specifies an initial

155 To save space, items that do not apply to a Clause are omitted. For example, if a Clause does not specify any requirements, there will be no "Requirements" subclause.