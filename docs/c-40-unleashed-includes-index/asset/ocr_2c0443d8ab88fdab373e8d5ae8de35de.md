An odd-number lottery if you will. As soon as an even random number is found, we break out of the loop. Break is one of those statements that justify the omission of curly braces when used as the embedded statement for an if statement.

# BREAKING... ONE LEVEL AT A TIME

In contrast to some other languages, C#'s break statement only allows us to break out of the closest loop or switch statement. That is, if you have nesting going on—such as loops inside loops or a switch inside a loop—you can only break out of the inner-most construct.

Why doesn't C#'s break account for that? There are probably a few reasons: Perhaps it's historically rooted; perhaps it's because C and C++, the spiritual parents of C#, don't supply such a multilevel break either. Or perhaps it's because such multilevel breaks are not common, so there's no reason to bloat the language.

“Too weak arguments,” you say. So what about this? Refactoring. Assume a multilevel break is done by labeling loops and specifying the label as an “argument” to the break statement, as shown here:

```
```csharp
// Warning: this is not a valid C# program.
outer:
while (conditionOuter)
{
    // Do stuff.
    while (conditionInner)
    {
        // Some inner loop code.
        break outer;
    }
    // Do more stuff.
}
```
```

When the inner loop grows too big, it'll be a good idea to have the refactoring functionality in Visual Studio do its thing and extract a method for it. But in the presence of labeled breaks, the code to be refactored is dependent on code much higher up, making straightforward refactoring impossible. Obviously, this problem also exists when using regular (much to be avoided) goto statements. Using labeled breaks, we've essentially brought back part of the goto hell. In fact, you can explicitly use C#'s goto statement to achieve this break effect if you really want.

One last argument I can bring up against labeled breaks is the fact that they don't improve code readability, requiring scrolling to find labels. With some flag-based plumbing—as you will see—you can follow the break path one level at a time. You can think of alternatives to labeled breaks, but they are at best cumbersome, too. For example, specifying the nesting level to break out of (0 for current loop, 1 for outer one, and so forth) is error-prone in the face of making updates to the code. Changing the nesting levels requires us to patch up all break statements that depend on it.