
## 5.3. STATIC PATH CONDITIONS FOR JAVA

analysis for irreducible graphs may be exploited to obtain a hierarchy of nested sub-PDGs; BDDs are needed to minimize the size of path conditions. Today, the implementation ValSoft can handle C programs to approx. 10000 LOC and generate path conditions in a few seconds or minutes.

## 5.3 Static Path Conditions for Java

In this section, we present the first path condition generator for Java which relies solely on static analysis. Naturally, the main problem in generalizing path conditions from procedural languages like C was the merging of object-oriented features such as dynamic dispatch and type checks.

### 5.3.1 Overview

Path conditions are generated according to all possible dependence paths from the source to the target point and a constraint solver reduces these conditions to input values that trigger information flow between these two points. Such input values have been named 'witnesses' in [SRK06], and may be quite helpful e.g. in law suits concerning security violations. However, [SRK06] only defines path conditions for procedural languages. A naive integration of object-oriented constructs in path conditions suffers from these conditions containing dynamic type checks, which constraint solvers cannot simplify statically. This witnesses cannot be generated, rendering these path conditions only a first step towards realistic applications.

This section presents a detailed study of object-oriented language constructs based on Java's language specification, as well as solutions for integration into a path condition that contains only program variables and values. We start discussing dynamic type checks a instanceof and extend the solutions based on dynamic dispatch and exception handling. These checks can be approximated conservatively, or by using program slicing — transformed into a subcondition that no longer involves the program's but generate realistic path conditions for Java. These conditions give more practical information than the conditions for dynamic dispatch presented in [JSB06], and allow constraint solvers to find input values that satisfy these conditions.

### 5.3.2 Dynamic Type Tests

In this section, we explore the semantics of the instanceof operator in order to utilize it in path conditions. Formally, the result of the expression instanceof T is true if the expression e is not null and e has a runtime type that is below the type T in the type hierarchy [JSB06]. A compile time error occurs, when no path exists in the type hierarchy from T to the static type of e. The language thus allows e to have a static type which is equal to or below T in the hierarchy, even though in that case, unless e

null, the expression will always evaluate to true. All this is well known, path conditions require a precise formalization of the instanceof semantics.

## CHAPTER 5. PATH CONDITIONS

### Precise semantics for instanceof

Java's reference types are identical to the defined classes (interfaces) in a program, so the terms type and class (interface) are used interchangeably. We write A < B if A is a subclass of B. A type hierarchy is the transitive closure of the subclass (<) relation. Let C be the set of all types, J the set of primitive types, and A the set of array types. Further let Σ = {java.io.Serializable, Cloneable, Object}. The notation e : τ denotes that e has dynamic/runtime type τ, and e : τ denotes static typing, respectively.

The type hierarchy induces concrete sets of types that satisfy the instanceof operator. Let Γ denote the set of types in the hierarchy that evaluate to true in the instanceof τ expression, is

```
e instanceof τ ≡ ρ ∧ ρ ∈ Γτ
```

For brevity, we assume a special null-type with Γnull = ∅. Then the definition of instanceof in the JLS [JSB05] requires:

If τ ∈ A then

if e ∈ τ then

```
ρ ∈ Γτ iff (ρ ∧ C ≤ τ) ∨ (ρ ∧ τ ∈ Σ) ∧ ρ ∈ Γτ,
```

else if e ∈ τ then

```
ρ ∈ Γτ iff ρ = [ρ[]] ∧ τ = τ[] ∧ ρ ∈ Γτ’
```

```
ρ ∈ Γτ iff ρ = τ
```

The last term of equation (5.5) corresponds to Java’s covariant array analysis, which may result in type safety problems when storing arrays. When the complete type hierarchy is given at analysis time, Γτ can be easily computed from the type hierarchy with e.g. class hierarchy analysis (CHA) [DGC95] or more refined analyses like rapid type analysis (RTA) [BS96] and the XTA algorithm [TP00]. A few cases of τ are of high importance:

```
Object = C ∪ A, which is infinite in primitive² do
```

```
ΓCloneable = {X | X < Cloneable} ∪ C[[]
```

```
Γτ[] = ∪ {τ ∈ Γτ}
```

The last equation describes how to resolve an array type τ[] based on the Γτ of its base type.

> ²In Java, the number of array dimensions is bounded by 255 [LY99].

132

## 5.3. STATIC PATH CONDITIONS FOR JAVA

```
// pre: B extends InstanceOfExample
public class InstanceOfExample {
    static boolean pred = true;
    public static void main(String[] args) {
        A a = pred ? new A() : new B();
        System.out.println(instanceOf(a));
    }
    public static int instanceOf(A sel) {
        int result = 0;
        if (sel instanceof B) {
            result = 42;
        }
        return result;
    }
}
```

Figure 5.4: An example for the instanceof operator

The Γτ constructed in the previous section are necessary to describe the generation of path conditions for instanceof. Note that these path conditions still contain dynamic type tests of the form expr : ρ; these will be removed by transformation in the next section.

> Algorithm 10 Path conditions for instanceof
**Input:** an expr instanceof τ
**Output:** representing path condition with dynamic type tests.
1: if τ = Object V (τ ∈ Γ expr : ρ) ∨ (τ = τ'[i] ∧ τ' ∈ ) then
2:     return expr ≠ null
3: else
4:     return expr ≠ null ∧ (Vⱼ ∈ Γr, expr : γⱼ)
5: end if

Algorithm 10 presents how path conditions for instanceof are computed; the algorithm is based on the precise instanceof semantics. The differences between equations (5.4)-(5.6) and the algorithm stem from optimizations which are at compile time, the JLS [GJS05]. For example, Γint = (int); the type test is at compile time and no further runtime constraint is required for the test null.

Obviously, the more refined Γτ is determined, the more precise the condition for the instanceof expression becomes. As points-to analysis is usually a prerequisite for precise slicing, points-to analysis can be leveraged to increase precision of Γτ. The number of possible runtime types reduces to less than or equal to 1, the path condition can be immediately reduced to true if the remaining type is an instance of τ, provided that the expression can never be null or false. As usual, determining Γτ requires whole-program analysis either without reflection, or using conservative approximations (e.g. [LWL05].

## CHAPTER 5. PATH CONDITIONS

For the example program in Figure 5.4, the initial path condition between the parameter in line 8 and the return value in line 12 is

```
PC(sel_s, result_{i2}) = sel instanceof B
```

as no other path between these program points exists in the PDG. Since B is no special type, Algorithm 10 replaces this condition by

```
PC(sel_s, result_{i2}) = sel != null && sel : B
```

### Exploiting backward slices in type tests

Path conditions for instanceof, described so far, are of limited practical, as they may contain types with no link to variable values (e.g. sel : B), and cannot serve as a witness. This section presents a new technique to transform such conditions into a form containing only program variables and values, which can be used to generate witnesses. The fundamental idea is to replace variables in runtime checks by their backward slice.

The conditions in the last section contained of the form M_{CF}(e : γ) for some type γ, that are naturally type checks. Program slicing offers a means to replace these conditions with terms that only reference program variables. The term e : γ depends on the last definition of e and evaluate to true only if e has been assigned an instance of γ. The program dependence graph allows to resolve paths from which γ-allocations reach a data slice [BGS97], or more precisely, the statements in a thin slice [SFB07]. In a backward slice, only data dependencies and parameter edges are traversed, but control dependencies are not. This variant yields only those statements whose value may have an influence on the slicing criterion. The thin slice is even more restrictive, that it only computes value flow, i.e. those statements that define a value that is used at the criterion node, which is exactly what we are interested in.

The following steps are to be taken to generate this refined path condition:

- 1. Determine the basic path condition p according to Algorithm 10 in section 5.3.2
- 2. Compute the backward data slice or thin slice for the parameter e of the instanceof γ operator
- 3. For each type in p extract the allocation sites of that type from the slice
- 4. Concatenate the path conditions from the program's start node to end of these allocation sites and from the instanceof expression with logical or
- 5. Replace the dynamic type checks in the basic path condition with the term generated in the last step.
