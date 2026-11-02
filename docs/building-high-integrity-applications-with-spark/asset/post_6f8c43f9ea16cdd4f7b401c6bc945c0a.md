
attempt to discharge them regardless of the assertion policy setting. Thus, static verification is unaffected by the `Assertion_Policy` pragma.

## Summary

- A logical error is an error in the program’s logic as a result of programmer oversight. A runtime error is a special kind of logical error that is detected by Ada-mandated runtime checks.
- An assertion is a programmer-defined check. All assertions are executable under the control of the assertion policy in force when a unit is compiled. A policy of Check enables assertions. A policy of Ignore disables them. If an assertion fails during execution, `Assertion_Error` is raised.
- The SPARK tools attempt to prove that a program is free of runtime errors and, in addition, all programmer supplied assertions will always be satisfied.
- SPARK eliminates `Program_Error` and `Tasking_Error` by prohibiting the features that might raise them.
- SPARK does not eliminate the possibility of `Storage_Error`, but it simplifies the analysis required to eliminate it.
- SPARK eliminates `Constraint_Error` as part of proving freedom of runtime errors.
- At each point where a check is required, either as mandated by the Ada standard or as added by the programmer in the form of an assertion, the SPARK tools generate a verification condition that, if proved, shows the check will never fail.
- A precondition is an assertion attached to a subprogram that must hold whenever the subprogram is called. It can be used to constrain the inputs to a subprogram beyond the constraints imposed by the type system. In particular, preconditions can describe required relationships between inputs.
- A postcondition is an assertion attached to a subprogram that must hold whenever the subprogram returns. It describes the effect of the subprogram and is part of the subprogram’s functional specification.
- In a postcondition, you can use the `'Old` attribute to reference the value of an input when the subprogram is first entered. You can use the `'Result` attribute to reference the return value of a function.
- The `Initial_Condition` aspect can be used on a package to specify the state the package has after elaboration. It serves as a kind of package-wide postcondition and is most useful for packages that have internal state.
- Assertions in the visible part of a package cannot directly reference information in the private section of a package. It is thus sometimes necessary to define and use public functions in such assertions.
- The Refined_Post aspect can be used in the body of a package to describe a subprogram’s postcondition in internal terms. SPARK attempts to prove that the public postcondition, if any, follows from the subprogram’s precondition and refined postcondition.
- Expression functions are automatically given a refined postcondition that asserts they return the value of the expression used to define them. As a result, expression functions can be thought of as pure specification.
- It is common to define functions in public assertions as inline expression functions in the private section of a package specification.
- A type invariant is an assertion attached to private type that must hold whenever a subprogram manipulating an object of that type returns. They can be approximately thought of as postconditions that are automatically applied to all subprograms manipulating the type.
- Type invariants are currently not supported by SPARK. However, they are part of Ada and can still be used. The SPARK tools will simply not (yet) attempt to prove they never fail.
- Subtype predicates allow you to specify complex constraints on subtypes. They can be used to specify types more precisely. SPARK currently does not support dynamic predicates but does support static predicates.
- Contract_Cases gives you a way of specifying a collection of pre- and postconditions in a convenient, easy-to-maintain way. It is most applicable when the input domain of a subprogram can be partitioned into disjoint subdomains. SPARK proves that all the cases are mutually exclusive and that they cover the entire input domain.
- Because assertions are executable, there is a possibility they might cause a runtime error when evaluated. The SPARK tools also generate verification conditions to show this will not happen.
- Runtime errors in the assertions can be avoided by adjusting the overflow mode of the GNAT compiler.
- The Assert pragma allows you to inject arbitrary checks into the body of a subprogram. The SPARK tools attempt to prove every Assert is always true, and it uses the asserted information to help with following proofs. The Assert pragma lets you give “hints” to the tools to simplify later proofs.
- The Assert_And_Cut pragma is like the Assert pragma except that it also introduces a cut point. All paths that reach the Assert_And_Cut are terminated. Only a single path leaves the Assert_And_Cut. This is useful for reducing the total number of paths in a subprogram to simplify verification conditions and speed up processing.
- The Assume pragma introduces information for the SPARK tools to use but does not carry any proof obligations itself. It can be used to encode information external to the program that the tools nevertheless need to complete reasonable proofs.
- The Assume pragma should be used carefully. If the assumption is false, the SPARK tools may end up proving false things. However, Assume is executed as usual so testing may uncover false assumptions.
- A loop invariant is an assertion added to the body of the loop that asserts a condition that is true for every loop iteration. It serves as a cut point and thus prevents the loop from creating a potentially infinite number of paths.
- Despite being a cut point, the SPARK tools give special handling to values that are not changed inside the loop. Information about those values do not need to be reasserted by the loop invariant.
- Choosing loop invariants can be tricky. You need to find a condition that is readily proved on loop entry and for each iteration of the loop and that also provides enough information to prove other verification conditions inside and beyond the loop.
- If the SPARK tools successfully prove a subprogram’s postcondition, it only means the postcondition is honored if the subprogram actually returns.
- The Loop_Variant pragma allows you to specify one or more expressions that always increase or always decrease as a loop executes. The expressions must have a discrete type so if the loop variant is true it implies the loop must terminate eventually.
- It is appropriate to use Loop_Variant in while loops or in loops constructed with a bare loop reserved word.
- SPARK handles discriminated types similarly to the way it handles unconstrained array types. The tools generate verification conditions related to the discriminants as appropriate, and the discriminants can be used in assertions in a natural way.
- The SPARK tools do not analyze generic code directly but instead analyze each instantiation of a generic separately. Some instantiations might prove fully, whereas others might not even be legal SPARK.
- When the SPARK tools analyze a generic instantiation, they use information about the actual generic parameters involved. Some instantiations might be difficult to prove because of the limited information available about the types and operations used.
- In fully proved code, it may be desirable to suppress runtime checks and assertion checks to improve the efficiency of the program. Assertion checks, especially, may warrant suppression because assertions have the potential of slowing down execution asymptotically.

## Exercises

6.1 Alice is interested in using a package Bob created. Which of them wants the public subprograms in that package to have strong preconditions? Which of them wants strong postconditions?

6.2 Suppose there is a function File_Exists that takes a string and returns True if a file of the given name is available to your program. Now consider a procedure that reads a configuration file declared as follows:

```
procedure Read_Configuration (File_Name : in String)
  with Pre => File_Exists (File_Name);
```

This is a suspicious use of contracts. Why?

6.3 What is a *cut point* and under what circumstances would it be appropriate to consider introducing one into your code? How would you add a cut point to your code?

6.4 Suppose you wanted to create a subprogram that accepted only even nonnegative integers. You could either use a precondition as follows,

```
procedure Example (X : Natural)
  with Pre => (X mod 2 = 0);
```

or you could use a subtype predicate as follows,

```
subtype Even is Natural
  with Dynamic_Predicate => Even mod 2 = 0;

procedure Example (X : Even);
```

Discuss the relative merits of these two approaches with respect to SPARK programming. Is your answer different if the subtype could be defined using a static predicate instead?

6.5 Type invariants are not supported by SPARK at the time of this writing. However, to a large degree this can be worked around. How?

6.6 Explain how contract cases can be considered a combination of preconditions and postconditions. Is the Contract_Cases aspect strictly necessary, or is it always possible to express contract cases using pre- and postconditions?

6.7 Write a procedure that increments every counter in an array of counters. Prove your procedure free of runtime errors. You will need a precondition to assert that all the counters are not yet at their maximal values. You may also need a suitable loop invariant.
