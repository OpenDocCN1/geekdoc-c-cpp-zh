# Types

In C#, **types** describe values. Any time you want to use a value, you need a type. As you saw when you learned about the common type system, a type defines the allowed values and operations supported by those values. Every value in C# is fully described by its exact type and is an **instance** of that exact type. Being fully described means that the type unambiguously defines both the representation and operations of a value.

Types in C# are divided into value types and reference types. **Value types** describe values that are completely self-contained and include numeric types, enumerated types, and structures. **Reference types**, however, store a reference to a value rather than the actual value.

C# provides many predefined value types and a few predefined reference types. It also enables you to create your own user-defined types. In upcoming hours, you explore, in more detail, the difference between value types and reference types and how to create your own. For now, however, the most important difference is that a value type is copied “by value” because it contains the actual value, whereas a reference type contains a reference to the actual data.

# Statements and Expressions

A **statement** is simply a single, complete program instruction that must end with a semicolon (;). Only specifying a single instruction seems like it would be restrictive, but C# also gives us the idea of a **statement block**, which is simply a group of statements enclosed by braces. You can use a statement block anywhere you would normally use a single statement.

Because statements end with a semicolon, you are free to use whitespace (such as a space character, tab character, or newline) in a way that helps visually orient your code. The best approach is to adopt a simple and consistent style (if your company or team does not already have one) to make your code easier to read and maintain.

**Whitespace**  
Even though the compiler generally ignores whitespace, the whitespace between a type declaration, its identifier, and any other keywords is important. Without whitespace here, the compiler can’t distinguish the keywords.

An **expression** evaluates to a value. If you consider a statement to be a program action, an expression is a computation. Expressions that result in a Boolean value (either `true` or `false`) are most commonly used to test if one or more conditions are true and are called **Boolean expressions**.

![](bbox=[0.8, 0.26, 0.95, 0.4])

![](bbox=[0.8, 0.73, 0.95, 0.79])