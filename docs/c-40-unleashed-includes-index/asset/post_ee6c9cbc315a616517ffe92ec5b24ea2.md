
![](img/a16f85e62ce9bdc527f4b09dbfe26092_274_0.png)

FIGURE 4.40 Nullable<T> from an abstract viewpoint.

## LIFE WITHOUT NULL?

Let’s be clear about one thing first: An orthogonal approach for nullability versus the distinction between value and reference types is absolutely a good thing. It should be every type’s right to support null as a proper value if it chooses to do so. However, the attentive reader will spot another missing piece from the puzzle. With the inception of nullable value types, null was brought to the world of value types. This aligns well with modern society: Adding capabilities is always seen as a good thing. But what about the opposite? Maybe I want to define a type for which null cannot be defined meaningfully.

So here we are with a new asymmetry. For value types, we can opt in to nullability if we want to support null values. But for reference types, we can’t opt out from nullability if we don’t want to support null values. This proves to be a common source of errors as people miss out on null checks.

A farfetched idea? Not really. Some languages (for example, Eiffel) have built-in support for non-null types (also known as nonvoid types in Eiffel). Another sample is Spec#, a research language created by Microsoft Research, based on C#. Spec#’s notation for a non-null type used the exclamation mark, as in string! for a non-null string. F# strikes a middle by embracing nullability for existing .NET types but promotes non-null types by making them the standard for newly defined types. When null is required, regardless of the underlying type representation, an option type is used.

Why are non-null types not in the mainstream languages and CLR at this point then? One answer is to be found in the complications it brings to existing languages. Where nullability extends the domain of a type, non-null types restrict it. For nullable value types, if a language doesn’t support syntax for it (like int?), the type is still usable (although its use will become a bit more cumbersome). However, when taking away values, the language needs to have rules to ensure no nullable values are assigned in non-nullable positions. In a multilanguage world, this would be a very invasive change.

All is not lost, though. With .NET 4.0 code contracts, a library approach is taken to provide non-null contracts on variables. The underlying type doesn't change, and no syntax has to be added to languages, so the impact on existing languages and tools is minimal. Because contracts get compiled into IL code, common tools can be provided to check non-null constraints regardless of the used language:

```
public void ContractSample(string input)
{
    Contract.Requires(input != null);
    // ...
}
```

Think of this as an extension to the method signature that can be used by tools to reason about the code, prove potential violations against the contract, emit rich documentation for users of the API, and so on. Contracts can either be compiled into the code, resulting in runtime checks, or compiled away when automated tools are used to prove or disprove the contract's validity by means of static code analysis. By having it as a library, all languages can benefit from it.

## Summary

By exploring the entry point of a program, we put ourselves in a position to experiment with language essentials in this and the chapters to come. In this chapter, you learned a good deal about the role types play in programs and what the built-in types are. Concepts such as types, objects, instances, variables, assignment, arrays, and nullable value types should hold no secrets for you anymore.

In the next chapter, we continue on our merry way through the C# language by starting to write code that really does something. Expressions will be used to compute values, and statements will drive the program's execution through mechanisms such as control flow.

## CHAPTER 5

## Expressions and Operators

## IN THIS CHAPTER

- What Are Expressions? 247
- The Evaluation Stack 251
- Arithmetic Operators 255
- String Concatenation 266
- Shift Operators 270
- Relational Operators 271
- Logical Operators 273
- Conditional Operators 278
- An Operator’s Result Type 281
- Null-Coalescing Operator 282
- Assignment 285

Continuing our journey through language essentials, we’ve arrived at the point where we focus on blocks of code. One thing we need is the ability to compute values based on existing ones, using expressions. Besides this, there’s a need for control flow structures, sequencing of instructions, and so on, which is provided through statements. In this chapter, we start by looking at expressions. In the next chapter we continue our journey through expressions related to working with objects. Statements are covered in the chapters following our discussion of expressions.

## What Are Expressions?

A key ingredient to every programming language’s expressiveness stems from the use of expressions. In fact, some languages are (almost) entirely based on this concept. C# isn’t that extreme though. But what are expressions? According to the language specification:

> An expression is a sequence of operators and operands.

First, it’s important to notice expressions typically denote a value by means of some computation. This is achieved by having operators operate on one or more operands, carrying out the desired computation. Because expressions represent a value, they also do have a type.

Examples of operators include arithmetic operators, comparison operators, and so on. Operands can be variables, literals, or even other expressions. This gives rise to a tree structure, as illustrated in Figure 5.1.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_277_0.png)

FIGURE 5.1 Operators and operands in an expression.

## Arity of Operators

Operators have an *arity*, indicating the number of operands on which they operate. For example, negating an integer value takes just one operand and is said to be a *unary operator*. Other operations, such as addition or Boolean conjunction, require two operands and are therefore called *binary operators*. The maximum number of operands in any operator in the C# language is three, making those operators *ternary operators*.

## Precedence and Associativity

Operators also have a precedence relative to one another. The use of parentheses can be used to circumvent those precedence rules. It’s often clearer to add some gratuitous pairs of parentheses than to assume every reader of the code is intimately familiar with the precedence of operators used in an expression.

Everyone knows examples from high school mathematics:

```
```text
a + b * c
```
```

The preceding evaluates b times c before carrying out the addition with a. Adding parentheses—here really redundant as every self-respecting developer should know those basic math rules, at least in my opinion—makes this ordering explicit:

```
```text
a + (b * c)
```
```

Obviously, if you want to multiply the sum of a and b with c, precedence needs to be overridden by adding a required pair of parentheses:

```
```text
(a + b) * c
```
```

Alternatively, intermediate results could be stored in temporary local variables, which is a good idea in case expressions become too large.

Table 5.1 showcases all available operators.

# TABLE 5.1 Operator Precedence

| Category | Operators |
|---|---|
| Primary | x.y f(x) a[x] x++ x-- new typeof default checked unchecked delegate |
| Unary | +, ! ~ ++x --x (T)x |
| Multiplicative | * / % |
| Additive | + - |
| Shift | << >> |
| Relational, type test | < > <= >= is as |
| Equality | == != |
| Logical AND | & |
| Logical XOR | ^ |
| Logical OR | \| |
| Conditional AND | && |
| Conditional OR | || |
| Null coalescing | ?? |
| Conditional | ?: |
| Assignment, lambda | = *= /= %= += -= <<= >>= &= ^= |= => |

## TIP

Come back to this table after you've reached the end of this chapter. You should be able to name all operators flawlessly, illustrate them with examples, and reason about their resulting types.

Besides precedence, associativity is an important concept when talking about evaluation of expressions. Assuming an operand (for example, the variable b) sandwiched between two operators (for example, the integer addition operator +), what's the order for the operations performed? In other words, does this operand associate with the operator on the left first or the one on the right first? For example:

```
a + b + c
```

Here, operand b is precisely in this situation. Two options exist: When treated in a left-associative manner, a + b is evaluated first. In a right-associative setting, b + c goes first. In this case, as for most binary operators, left associativity is used:

```
(a + b) + c
```
