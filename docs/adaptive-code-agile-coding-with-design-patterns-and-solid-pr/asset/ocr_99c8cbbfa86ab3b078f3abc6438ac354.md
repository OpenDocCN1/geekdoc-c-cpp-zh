There are three code ingredients relating to the LSP:

+   - **Base type** The type (T) that clients have reference to. Clients call various methods, any of which can be overridden—or partially specialized—by the subtype.
+   - **Subtype** Any one of a possible family of classes (S) that inherit from the base type (T). Clients should not know which specific subtype they are calling, nor should they need to. The client should behave the same regardless of the subtype instance that it is given.
+   - **Context** The way in which the client interacts with the subtype. If the client doesn’t interact with a subtype, the LSP can neither be honored nor contravened.

# LSP rules

There are several “rules” that must be followed for LSP compliance. These rules can be split into two categories: contract rules (relating to the expectations of classes) and variance rules (relating to the types that can be substituted in code).

# Contract rules

These rules relate to the contract of the supertype and the restrictions placed on the contracts that can be added to the subtype.

+   - Preconditions cannot be strengthened in a subtype.
+   - Postconditions cannot be weakened in a subtype.
+   - Invariants of the supertype—conditions that must remain true—must be preserved in a subtype.

To understand the contract rules, you should first understand the concept of contracts and then explore what you can do to ensure that you follow these rules when creating subtypes. The “Contracts” section later in this chapter covers both in depth.

# Variance rules

These rules relate to the variance of arguments and return types.

+   - There must be contravariance of the method arguments in the subtype.
+   - There must be covariance of the return types in the subtype.
+   - No new exceptions can be thrown by the subtype unless they are part of the existing exception hierarchy.

The concept of type variance in the languages of the Common Language Runtime (CLR) of the Microsoft .NET Framework is limited to generic types and delegates. However, variance in these scenarios is well worth exploring and will equip you with the requisite knowledge to write code that is LSP compliant for variance. This will be explored in depth in the “Covariance and contravariance” section later in this chapter.