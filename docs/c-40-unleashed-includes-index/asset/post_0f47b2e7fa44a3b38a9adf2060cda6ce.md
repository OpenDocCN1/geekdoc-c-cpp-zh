
Use of the performance counter infrastructure in Windows, and various ways to interact with a debugger from code.

Finally, as a little extra, we cover the Process class, which can be used to spawn processes and query them for various properties. The common thread between this class and most of the other topics covered in this chapter is the System.Diagnostics namespace, which we consider to be an integral part of the Base Class Library (BCL).

## Ensuring Code Quality

Getting code quality to high levels right from the start of development is a very valuable thing to do. Issues uncovered later in the development cycle of a product tend to have exponentially higher costs compared to issues discovered early on. Different tools can be leveraged to ensure high levels of code quality.

Focusing on facilities in the BCL, our exposition of code quality tools and techniques doesn't include a praise of unit testing virtues, a good development process, and so on. I strongly recommend enterprise-class developers invest their time in learning about those aspects, too. Keywords such as *test driven development (TDD)* and *software development in teams* jump to mind immediately. Unfortunately, we don't have the room to dive into those aspects. Books dedicated to those subjects, also focusing on tools like Visual Studio Team System, are highly recommended.

### Code Analysis

One of the biggest merits of good framework design is to have common patterns and conventions that make developers feel at home when discovering your application programming interface (API). It should be no surprise that tools have been written to enforce those goals by means of static, compile-time analysis of code. It turns out such tools can also be used to point out a plethora of common bugs or suboptimal development practices.

Collectively known as “code analysis” in Visual Studio, all those static compile-time checks provide a great means to be vigilant about certain aspects of code quality in a continuous manner. Starting with Visual Studio 2010, code analysis rules have been grouped in so-called rule sets, which control the amount of “noise” you can tolerate.

I recommend turning on code analysis as shown in Figure 27.1 early in the development cycle of an application, library, or whatnot. This is also the ideal time to study rule sets and determine which one is best for you. In addition to enabling the build-time code analysis, it also might be a good idea to check the Build flag to treat errors as warnings. If someone introduces a new violation, one is required to tackle the problem (either by fixing it or by suppressing it) before checking in code. In fact, such rules can be enforced in Team Foundation Server, as well.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1394_0.png)

FIGURE 27.1 Enabling code analysis with the minimum recommended set of rules.

A thorough discussion of all the rules implemented in this feature is beyond the scope of this discussion. The best way to familiarize yourself with the rules is to just run the code analysis tools, with the maximum rule set, on a non-trivial-sized project that didn't have the feature turned on previously. Doing so will be an eye-opener and reveal a whole lot of potential defects you might want to examine.

## HOW RULES ARE WRITTEN

Rules are basically implementations of some IRule interface that gets a chance to look at compiled code by means of an expression tree format. Those trees are built from the compiled intermediate language (IL) code and provided by a framework known as CCI, or the Common Compiler Infrastructure, which can be downloaded from CodePlex. One key difference with the System.Linq.Expressions trees is the origin of the trees. Whereas the LINQ ones are crafted at compile time, CCI extracts them from already compiled code.

Recommended corrective actions can be found by highlighting the warning in Visual Studio's Errors and Warnings pane and pressing F1 to open Help. After studying this guidance, you may still decide the error is a false positive or you have good reasons to dismiss the advice. In such a case, errors can be suppressed, as shown in Figure 27.2.

Suppressions should be used with care and be based on good justification. All a suppression does is insert a custom attribute from the System.Diagnostics.CodeAnalysis namespace in the place you indicate, either on top of the member or in a GlobalSuppressions.cs file. Tools use this information to suppress messages in subsequent runs.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1395_0.png)

FIGURE 27.2 Use of suppressions to disable a warning.

## Asserts and Contracts

Statically discovering typical code defects is a big convenience, but it isn't a silver bullet. Lots of conditions are intrinsic to the algorithms you're coding up and simply cannot be detected by tools without particular knowledge of the developer's intent.

To communicate intent, various mechanisms have been created over the years. The oldest and simplest one is to use asserts, which are pieces of code that perform a logical check, typically only in special builds of your software. If the check fails, the developer is notified and invited to break in the debugger to analyze what's going wrong. Maybe the condition makes a false assumption about code invariants, or you've just caught a problem on the spot before it can do further damage.

Code contracts were introduced in .NET 4 based on a Microsoft Research project that was run in the years before the release. Contracts allow a more declarative approach to stating the code's intent, also communicating various conditions and expected code invariants to tools. Examples include pre- and post-conditions of methods, exception behavior, and assumed absence of null references. Based on this knowledge, tools can try to detect problems statically, by theorem provers that reason about your code. Alternatively, runtime checks can be generated.

Before we delve into both of those approaches, it's useful to contrast both models and relate them to the use of runtime checks. First of all, asserts are typically used as a tool to be leveraged at (extended) development time only. The reason we mention extended in this definition is that so-called checked builds may be used in tests or sometimes even in preproduction to uncover issues. Nonetheless, the excessive number of checks that could arise from asserts is likely not a price you want to pay at runtime, especially if you're dealing with internal implementation details that should never be violated unless a bug exists in your code. This is different from issues that can arise from unexpected or even malicious user input, which should always be checked at runtime.

This choice between development time and runtime checking of conditions has been quite black and white in the past. Runtime checks use exceptions, while asserts get compiled away in release builds and trigger developer alerts when violated during debugging. With the advent of code contracts, this choice can be controlled more tightly. In fact, you can balance between compile-time checks and runtime checks by leveraging post-build tools that essentially rewrite assemblies to omit or insert runtime checks.

### Developing with Asserts

Asserts are a code-driven way to document invariants that should hold in your code (for example, the fact a reference should not be null in nonpublic code or an integer denoting an index should be within valid bounds). Formulating an assert is simply done using a Boolean-valued expression passed to the Debug.Assert method, which is defined in the System.Diagnostics namespace. For example:

```
private static void Sort<T>(T[] values, int from, int to)
{
    Debug.Assert(from <= to, "Expected from to be less than to.");
    ...
}
```

I’ll leave it to you to implement a sort algorithm that divides the input array in two halves and recursively calls the Sort method to sort the halves. Doing so implies the need to compute indices in preparation of a recursive call. Those kinds of calculations are prone to subtle off-by-one errors and such. The goal of the assert is to catch such issues. Also when implementing the Sort method, think of other assumptions you’re making with regard to the input (and that therefore warrant the declaration of additional asserts).

A publicly exposed Sort method will simply wrap this, passing in the bounds of the entire array, effectively causing the whole array to be sorted if the private recursive Sort method is implemented correctly:

```
public static void Sort<T>(this T[] values)
{
    if (values == null)
        throw new ArgumentNullException("values");

    Sort(values, 0, values.Length - 1);
}
```

You should observe that for private calls, we don’t use exceptions here to signal invalid inputs. Instead, asserts are used to catch issues where asserts are broken. Because the private Sort method with sorting bounds is really an implementation detail, it’s our sole responsibility to ensure we’re calling the method in an appropriate manner. Using exceptions is an option but introduces an unnecessary exception checking cost simply to guard for mistakes that we should have caught during development.
