# 4.9. RELATED WORK

but are more efficient. JIF supports generic classes and the decentralized la-bel model [ML00]; labels and principals are first class objects. Note that our PD-based approach can be generalized to utilize decentralized labels.

Bartex Rezk [BR05] present a system type for strict noninterference without classification, handling classes and objects. NullPointer-Exception is the only exception type allowed. Only values annotated with Low may throw exceptions. Constructors are ignored, instead, objects are initialized with default values. A proof showing the noninterference property of the type system is given.

Strecker [Str03] formulated a non-deterministic system type including the noninterference proof in Isabelle [NPW02]. It handles major concepts of Micro-Java such as classes, and method calls, but arrays and exceptions. Mantel and Reinhardt [MR07] defined the first type system for a multi-threaded language that controls the *what* and the *where* dimension of declassificationsimultaneity. The type system is based on a definition for the *where* dimension that supersedes their previous definition of intransitive noninterference [MS04], and two variants of a definition for the *what* dimension similar to secrecy [Coh78]. However, they do not show their approach is practically viable.

# 4.9.3 Verification and IFC

Amtof et al. [ABB06] present an intercultural flow-sensitive Hoare-like logic for information control in a rudimentary object-oriented language. Casts, type tests, visibility modifiers other than public, and exception handling are not considered. Only structured control flow is allowed.

The Pacap case study [BCM07] verifies secure interaction of multiple Java-lets on one screen. They employ method checking to ensure a sufficient condition for their security policy, which is based on a lattice similar to noninterference without declassification. Implicit exceptions are modeled, but such unstructured control flow may lead to label creep (cef [SM03, Sect. 1 E]).

Genain [GS05] defines an abstract interpretation of the CFG looking for information leaks. It can handle all bytecode instructions of single-threaded Java and conservatively handle implicit exceptions of bytecode instructions. The analysis is flow- and context-sensitive object but does not differentiate fields of different objects. They propose an object-insensitive solution for all fields of a given class. In our experience [IS04] object-insensitivity yields too many spurious dependencies. The same is true for the approximation of the call graph by CHA. In this setting, too will result in many false alarms.

An area uncovered by our system is security policies, defining under which circumstances declassification is allowed. Li and Zdancevic [LZ05] define a framework for downgrading a core language with conditionals and fixed-points, yielding a formalized security guarantee with a program equivalence.