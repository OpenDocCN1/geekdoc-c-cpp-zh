
# 4.9. RELATED WORK

but are more efficient. JIF supports generic classes and the decentralized label model [ML00]; labels and principals are first class objects. Note that our PD-based approach can be generalized to utilize decentralized labels.

Bartex Rezk [BR05] present a system type for strict noninterference without classification, handling classes and objects. NullPointer-Exception is the only exception type allowed. Only values annotated with Low may throw exceptions. Constructors are ignored, instead, objects are initialized with default values. A proof showing the noninterference property of the type system is given.

Strecker [Str03] formulated a non-deterministic system type including the noninterference proof in Isabelle [NPW02]. It handles major concepts of Micro-Java such as classes, and method calls, but arrays and exceptions. Mantel and Reinhardt [MR07] defined the first type system for a multi-threaded language that controls the *what* and the *where* dimension of declassification simultaneity. The type system is based on a definition for the *where* dimension that supersedes their previous definition of intransitive noninterference [MS04], and two variants of a definition for the *what* dimension similar to secrecy [Coh78]. However, they do not show their approach is practically viable.

## 4.9.3 Verification and IFC

Amtoft et al. [ABB06] present an interprocedural flow-sensitive Hoare-like logic for information control in a rudimentary object-oriented language. Casts, type tests, visibility modifiers other than public, and exception handling are not considered. Only structured control flow is allowed.

The Pacap case study [BCM07] verifies secure interaction of multiple Java-lets on one screen. They employ method checking to ensure a sufficient condition for their security policy, which is based on a lattice similar to noninterference without declassification. Implicit exceptions are modeled, but such unstructured control flow may lead to label creep (cf [SM03, Sect. 1 E]).

Genais [GS05] defines an abstract interpretation of the CFG looking for information leaks. It can handle all bytecode instructions of single-threaded Java and conservatively handle implicit exceptions of bytecode instructions. The analysis is flow- and context-sensitive object but does not differentiate fields of different objects. They propose an object-insensitive solution for all fields of a given class. In our experience [IS04] object-insensitivity yields too many spurious dependencies. The same is true for the approximation of the call graph by CHA. In this setting, too will result in many false alarms.

An area uncovered by our system is security policies, defining under which circumstances declassification is allowed. Li and Zdancevic [LZ05] define a framework for downgrading a core language with conditionals and fixed-points, yielding a formalized security guarantee with a program equivalence.

# CHAPTER 4. INFORMATION FLOW CONTROL

## 4.9.4 Static analysis for security

Static analysis is often used for source code security analysis [CM04]. For example, information flow control is closely related to tainted variable analysis. There are even approaches like the one from Pistoa et al. [PFKS05] for slicing analysis and the one from Livshits and Lam [LL03, LL05] use IPSSA, a representation very similar to dependency graphs. However, these analyse only a trivial security level (tainted/untainted) with a trivial declassification (untaint) and could greatly benefit from our approach. Scholtz et al. [SZC08] present a static analysis that tracks user input on a data structure similar to a dependency graph. Like our analysis, it is defined as a dataflow analysis framework and reduce the constraint system using properties of SSA form. Again, this is targeted to bug tracking and taint analysis.

Pistoia et al. [PCFY07] survey recent methods for static analysis of security problems. They focus on stack and role-based access control, information flow and API control. A unified access-control and integrity checker for information-based access control, an extension of Java's stack-based access control mechanism has been proposed in [PS07]. They show that an implicit policy can be extracted from the access control policy, and that the access control enforces integrity policy.

Another approach is to use path conditions (as sketched in section 4.8.3) in order to obtain more semantically convincing characterizations and context constraints for sound declassification. Our approach to declassification currently not offer per-checks of semantic properties as stipulated by SS05], but will rely on path conditions to provide necessary conditions for a declassification to take place. This approach falls into the category “how” declassification may occur, which has not yet been extensively researched.

For multithreaded programs, PDGs need not only check for classic noninterference, but eventually for possible or probabilistic noninterference. Details of this novel technique will be presented by Giffhorn and Lochbihler [GL].

# Chapter 5

# Path Conditions

## 5.1 Introduction

The previous chapter presented our precise approach for information flow control. But no matter how precise the information flow analysis is, it will always answer a binary question only — whether illegal flow between two program points is possible, or whether this is definitely not the case. It may even be able to track down the source point making trouble, but still lack to provide insight into the specific conditions of the security violation. In particular, information flow control mechanisms do not provide "counter examples", e.g. in the form of input values that make the security violation visible.

This chapter will present two approaches to exactly that, based on the concept of a static path condition [Sn96, RS02, SRK06], which is a precise condition that needs to be satisfiable for information flow between two program points to be possible. Such a condition can be unsatisfiable, which means that the constraint solver finds the given information flow impossible and was a false positive in the original analysis, or simplifies the condition to input variable bindings that trigger that flow. This chapter extends this notion in two dimensions: First, the concept of a static path condition is extended to the object-oriented features of Java, which impose additional difficulties due to the dynamic nature of types through instanceof, dynamic dispatch and exceptions. However, our approach relies solely on static program analysis and thus allows generating precise conditions for illicit information flow, that say why this flow takes place, together with a set of input values that allow reproduction of that illicit flow.

Second, a dynamic variant of path conditions is presented that combines traditional static path conditions with dynamic analyses like dynamic slicing and information collected by program instrumentation. Dynamic slicing yields significantly smaller sets of conditions than static slicing, therefore the dynamic path conditions allow a precise post-mortem analysis of a failed program run and might even be leveraged for analyzing how illicit information flow occurred, after prevention by a dynamic flow control mechanism.

# CHAPTER 5. PATH CONDITIONS

```
1 a = u();
2 while (n>0) {
3 x = v();
4 if (x>0) {
5 b = a;
6 else
7 c = b;
8 }
9 z = c;
```

![](img/27c6595637bae6b27613772d7079f8a2_135_0.png)

Figure 5.1: A small program and its dependence graph

Both extensions have been implemented in a prototype tool based on the Valsoft architecture [HOb05]. Previous results from this effort have been described in [HGK06, HS08].

## 5.2 Foundations of Path Conditions

Program dependence graphs (PDG) as presented in chapter 2 are a standard tool to model information flow through a program. Program statements or conditions are represented by nodes, the edges represent data and control dependences between statements or conditions. A path x→y means that information can flow from x to y; if there is no path, it is guaranteed that there is no information flow. In particular, all statements (possibly) influencing (the so-called backward slice) are easily computed as BS(y) = {x | x→y}.

For the small program and its dependence graph in Figure 5.1, there is a path from statement 1 to statement 9, indicating that input variable a may influence output variable z. Since there is no path 1→4, there is definitely no influence from a to x.

- A chop for a chopping criterion (x,y) is the set of nodes that are part of the influence of the (source) node x on the (target) node y. The nodes that lie on a path from x to y in the PDG: CH(x,y) = {z | x→z→y}. For convenience, we use CH(x,y) for the set of paths between x and y.

### 5.2.1 Intraprocedural Path Conditions

In order to make program slicing more precise, Seltening path conditions [Sne96], which are necessary conditions for information flow between two nodes. The formula for the generation of path conditions are complex formulae (for details, see [SRK06]), and only the most fundamental formulae will be given here:

```
PC(x,y) = ∧_{Path=x→y z∈P} E(z) where E(z) = ∧_{Control Path Start→cd*z ν∈P} c(ν→μ) (5.1)
```
