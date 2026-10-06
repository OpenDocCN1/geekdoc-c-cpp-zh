
# ISO/IEC 14882:2017(E)

## 3.19 [defns.signature]

signature (function) name, parameter type list (11.3.5), and enclosing namespace (if any)
[Note 1 to entry: Signatures are used as a basis for name mangling and linking. — end note.]

## 3.20 [defns.signature.templ]

signature (function template) name, parameter type list (11.3.5), enclosing namespace (if any), return type, and template parameter list

## 3.21 [defns.signature.spec]

signature (function template specialization) signature of the template of which it is a specialization and its template arguments (whether explicitly specified or deduced)

## 3.22 [defns.signature.member.templ]

signature (class member function) name, parameter type list (11.3.5), class of which is a member, ce-qualifiers (if any), and ref-qualifier (if any)

## 3.23 [defns.signature.member.spec]

signature (class member function template) name, parameter type list (11.3.5), class of which is a member, ce-qualifiers (if any), and ref-qualifier (if any), return type (if any), and template parameter list

## 3.24 [defns.static.type]

signature (class function template specialization) signature of the member function template of which it is a specialization and its template arguments (whether explicitly specified or deduced)

## 3.25 [defns.unblock]

static type of an expression (6.9) resulting from analysis of the program without considering execution semantics
[Note 1 to entry: The static type of an expression depends only on the form of the program in which the expression appears, and does not change while the program is executing. — end note.]

## 3.26 [defns.undefined]

unblock satisfy that one or more blocked clauses are waiting for

## 3.27

undefined behavior for this document imposes no requirements
[Note 1 to entry: Undefined behavior may be expected when any explicit definition of behavior when a program uses an erroneous construct or erroneous data. Permissible behavior ranges from implementation completely to unpredictable results, both during translation or program execution in a documented characteristic of the environment (with or without the issuance of a diagnostic message), to terminating a transaction or execution (with the issuance of a diagnostic message). Many erroneous constructs do not engender undefined behavior; they are required to be diagnosed. Evaluation of a constant expression never exhibits behavior explicitly specified as undefined (8.20). — end note.]

ISO/IEC 14882:2017(E)

## 3.28 unspecified behavior

behavior, for a well-formed program construct and correct data, that depends on the implementation

[Note 1 to entry: The implementation is not required to document which behavior occurs. The range of possible behaviors is usually delineated by this document. — end note]

## 3.29 well-formed program

C++ program constructed according to the syntax rules, diagnostic semantic rules, and the one-definition rule (6.2).

## 4 General principles

## 4.1 Implementation compliance

The set of *diagnosable rules* consists of all syntactic and semantic rules in this document except for those rules containing an explicit notation that “no diagnostic is required” or which are described as resulting in “undefined behavior.”

Although this document states only requirements on C++ implementations, these requirements are often easier to understand if they are phrased as rules on programs, parts of programs, or execution of programs. Such requirements have the following:

- (2.1) If a program contains no violations of the rules in this document, a conforming implementation shall, within its resources, accept and correctly execute”
- (2.2) If a program contains any of diagnosable rule or a construct described in this document as “commonly-supported” when the implementation does not support construct, a conforming implementation shall issue at least one diagnostic.
- (2.3) If a program contains a violation of a rule in this document, this document places no requirement on implementations respect to that program.

[Note: During template instantiation and substitution, certain constructs in other contexts require a diagnostic is required: see 17.8.2, for note.]

- 3 For classes and templates, the Library Classes specify particular defaults. New members (Clause 14) are not specified, but each implementation shall supply to complete the definitions according to the description in the Library Classes
- 4 For functions, function templates, objects, and values, the Library Classes specify declarations. Implementations shall supply definitions for standard library entities, as necessary, while combining translation units to form a complete C++ program (5.2).
- 5 The names defined in the library have namespace (10.5). A C++ translation unit (5.2) accesses to these names by including the appropriate standard library header (19.2).
- 6 The templates, classes, functions, and objects in the library have external linkage (6.5). The implementation provides definitions for standard library entities, as necessary, while combining translation units to form a complete C++ program
- 7 Two kinds of implementations are defined: a hosted and freestanding implementation. A hosted implementation is one in which execution may take place without the benefit of an operating system, and an implementation-defined set of libraries that contains language-support libraries (20.5.1.3).
- A conforming implementation may have extensions (including additional library)
- A conforming implementation may have extensions (including additional library)
- A conforming implementation may have extensions (including additional library)
- A conforming implementation may have extensions (including additional library)

ISO/IEC 14882:2017(E)

## 4.3 Syntax notation

2 Names for syntactic categories are generally chosen to indicate their.
- (2.1) X—name is one of an identifier (e.g., *class-name, typedef-id*).
- (2.2) X—id is one or more X’s with context-dependent delimiter (e.g., *qualified-id*).
- (2.3) X—seq is one or more X’s with intervening delimiters (e.g., *declaration-seq*).
- (2.4) X—list is one or more X’s separated by intervening commas (e.g., *identifier-list*).

## 4.4 The C++ memory model

## [intro.memory]
