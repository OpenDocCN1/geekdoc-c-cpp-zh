
modify the state of a struct. If you can't declare the whole structure type as *readonly*, use the *readonly* modifier to mark the instance members that don't modify the state of the struct.

Within a *readonly* instance member, you can't assign to structure's instance fields. However, a *readonly* member can call a *non-readonly* member. In that case the compiler creates a copy of the structure instance and calls the *non-readonly* member on that copy. As a result, the original structure instance is not modified.

You can't apply the *readonly* modifier to static members of a structure type.

The compiler may make use of the *readonly* modifier for performance optimizations.

## Limitations with the design of a structure type

When you design a structure type, you have the same capabilities as with a class type, with the following exceptions:

- You can't declare a parameterless constructor. Every structure type already provides an implicit parameterless constructor that produces the default value of the type.
- You can't initialize an instance field or property at its declaration. However, you can initialize a static or const field or a static property at its declaration.
- A constructor of a structure type must initialize all instance fields of the type.
- A structure type can't inherit from other class or structure type and it can't be the base of a class. However, a structure type can implement interfaces.
- You can't declare a finalizer within a structure type.

## Instantiation of a structure type

In C#, you must initialize a declared variable before it can be used. Because a structure-type variable can't be *null* (unless it's a variable of a nullable value type), you must instantiate an instance of the corresponding type. There are several ways to do that.

Typically, you instantiate a structure type by calling an appropriate constructor with the `new` operator. Every structure type has at least one constructor. That's an implicit parameterless constructor, which produces the default value of the type. You can also use a default value expression to produce the default value of a type.

If all instance fields of a structure type are accessible, you can also instantiate it without the `new` operator. In that case you must initialize all instance fields before the first use of the instance.

In the case of the built-in value types, use the corresponding literals to specify a value of the type.

## Passing structure-type variables by reference

When you pass a structure-type variable to a method as an argument or return a structure-type value from a method, the whole instance of a structure type is copied. That can affect the performance of your code in high-performance scenarios that involve large structure types. You can avoid value copying by passing a structure-type variable by reference. Use the `ref`, `out`, or `in` method parameter modifiers to indicate that an argument must be passed by reference.

Use `ref return` to return a method result by reference.

```
`ref struct`
```

You can use the `ref` modifier in the declaration of a structure type. Instances of a `ref struct` type are allocated on the stack and can't escape to the managed heap.

Typically, you define a `ref struct` type when you need a type that also includes data members of `ref struct` types.

To declare a `ref struct` as `readonly`, combine the `readonly` and `ref` modifiers in the type declaration (the `readonly` modifier must come before the `ref` modifier).

544

In .NET, examples of a `ref` struct are System.Span and System.ReadOnlySpan.

### Conversions

For any structure type (except `ref` struct types), there exist boxing and unboxing conversions to and from the System.ValueType and System.Object types. There exist also boxing and unboxing conversions between a structure type and any interface that it implements.

### Switch Statement (`switch`)

`switch` is a selection statement that chooses a single *switch section* to execute from a list of candidates based on a pattern match with the *match expression*.

The `switch` statement is often used as an alternative to an *if-else* construct if a single expression is tested against three or more conditions.

#### The match expression

The *match expression* provides the value to match against the patterns in `case` labels. Its syntax is:

```
switch (expr);; {};;
```

The *match expression* can be any non-null expression.

#### The switch section

A `switch` statement includes one or more *switch sections*. Each *switch section* contains one or more `case` labels (either a `case` or `default` label) followed by one or more statements. The `switch` statement may include at most one `default` label placed in any *switch section*. The following example shows a simple `switch` statement that has three *switch sections*, each containing two statements. The second *switch section* contains the `case 2:` and `case 3:` labels.

A `switch` statement can include any number of switch sections, and each section can have one or more case labels, as shown in the following example. However, no two case labels may contain the same expression.

```csharp
switch (caseSwitch)
{
    // The following switch section causes an error.
    case 1:
        Console.WriteLine("Case 1...");
        // Add a break or other jump statement here.
    case 2:
        Console.WriteLine("... and/or Case 2");
        break;
}
```

This requirement is usually met by explicitly exiting the switch section by using a `break`, `goto`, or `return` statement.

Execution of the statement list in the switch section with a case label that matches the match expression begins with the first statement and proceeds through the statement list, typically until a jump statement, such as a `break`, `goto case`, `goto label`, `return`, or `throw`, is reached. At that point, control is transferred outside the `switch` statement or to another case label. A `goto` statement, if it's used, must transfer control to a constant label. This restriction is necessary, since attempting to transfer control to a non-constant label can have undesirable side-effects, such transferring control to an unintended location in code or creating an endless loop.

### Case labels

Each case label specifies a pattern to compare to the match expression (the `caseSwitch` variable in the previous examples). If they match, control is transferred to the switch section that contains the first matching case label. If no case label pattern matches the match expression, control is transferred to the section with the `default` case label, if there's one. If there's no `default` case, no statements in any switch section are executed, and control is transferred outside the switch statement.

Case labels need not define mutually exclusive values, and multiple patterns can match the match expression. Because only the statements in the first switch section that contains the matching pattern are executed, the order in which case statements appear is now important. If C# detects a switch section whose case statement or statements are equivalent to or are subsets of previous statements, it generates a compiler error, CS8120, "The switch case has already been handled by a previous case."

The following example illustrates a switch statement that uses a variety of non-mutually exclusive patterns. If you move the case 0: switch section so that it's no longer the first section in the switch statement, C# generates a compiler error because an integer whose value is zero is a subset of all integers, which is the pattern defined by the case int val statement.

You can correct this issue and eliminate the compiler warning in one of two ways:

- By changing the order of the switch sections.
- By using a when clause in the case label.

## The default case

The default case specifies the switch section to execute if the match expression doesn't match any other case label. If a default case is not present and the match expression doesn't match any other case label, program flow falls through the switch statement.

The default case can appear in any order in the switch statement. Regardless of its order in the source code, it's always evaluated last, after all case labels have been evaluated.

## Pattern matching with the switch statement

Each case statement defines a pattern that, if it matches the match expression,
