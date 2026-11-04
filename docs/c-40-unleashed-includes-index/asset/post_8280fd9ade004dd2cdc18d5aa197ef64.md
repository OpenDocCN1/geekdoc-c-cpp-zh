
![](img/a16f85e62ce9bdc527f4b09dbfe26092_568_0.png)

**FIGURE 10.22**  A project with good maintainability.

The Code Metrics feature includes a set of different metrics computed from the compiled project. A full explanation of those metrics goes beyond the scope of this book, but you want to try keeping the maintainability index high while reducing both class coupling (the more types are coupled through calls, parameters, and so on, the harder it is to reuse) and cyclomatic complexity (number of distinct code paths makes testing harder).

Although refactoring is a noble goal, never lose sight of correctness of the code. In fact, the idea of refactoring techniques is never to change the functionality of the software. In essence, every refactoring should be nothing but a mechanical rewrite of code such that all original properties are maintained. This can prove quite tricky in an imperative programming language that’s full of side effects. For example, elimination of common subexpressions doesn’t always preserve semantics:

```csharp
// Before: will ask input twice and concatenate it
Console.WriteLine(Console.ReadLine() + Console.ReadLine());

// After: will ask input once and duplicate it
string x = Console.ReadLine();
Console.WriteLine(x + x);
```

Visual Studio contains some refactoring techniques that can be carried out through the code editor. Figure 10.23 shows where to find those. Third-party extensions often come with more-sophisticated refactorings that can become quite addictive once you get the hang of refactoring-assisted development.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_568_1.png)

**FIGURE 10.23**  The Refactor context menu hosts a few simple refactoring techniques.

In the example shown in Figure 10.23, you can think about three possible explanations for the weird definition of Subtract that performs the subtraction operation out of order compared to the method parameters. Maybe it's a bug, perhaps it's an artifact of the code's evolution (unlikely given the simplicity of the example), or maybe it's just some unexplainable strange convention (or oversight) introduced by the original author. In all but the first case, reordering of parameters may be a good idea to make the code look better and behave more predictably. Figure 10.24 shows this refactoring in action, first allowing the user to pick the new order of parameters.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_569_0.png)

FIGURE 10.24 Preview of a new method signature after parameter reordering.

Once we have found a suitable ordering, we can confirm the refactoring and preview the changes. Visual Studio will propose the following refactoring code. Notice how all call sites to the refactoring method are changed, as well.

```
public static void Main(string[] args) {
    Console.WriteLine(Subtract(3, 5));
}

public static int Subtract(int a, int b) {
    return a - b;
}
```

## BEHAVIOR MAINTAINED?

Even those simple refactorings tend not to preserve semantics in more advanced scenarios. For example, reorder parameters will reorder arguments in each call site. But if evaluation of an argument is based on an expression that has possible side effects, those effects will be swapped as well because of C#'s left-to-right evaluation of subexpressions. Whether you should write such code to begin with is another matter.

Perhaps the most useful refactoring is the one to extract methods. Performing this can be triggered by a number of motivations. One is when you notice a method growing too large and a certain portion of it can be factored out as a piece of functionality that can stand on its own (and potentially be reused). Another related one is based on spotting common helper methods being used in different places throughout your source code base.

An example of the extract methods refactoring is shown here. Don't worry too much about the APIs used by this piece of code; all the magic will become clear in Chapter 21. Suffice to say, the code to determine a table name based on some entity type is quite involved and has little to do with the surrounding code. One place where such code would be written is in a LINQ provider's query translation code. It's also not uncommon for such utilities to be useful in different places, so extracting a common helper method is a good practice:

```csharp
public static void Main()
{
    string query = TranslateQuery(typeof(Person) /* more args omitted */);
    Console.WriteLine(query);
}
```

```csharp
public static string TranslateQuery(Type entity /* more params omitted */)
{
    string tableName;
    if (Attribute.IsDefined(entity, typeof(TableAttribute)))
    {
        object[] attributes = entity.GetCustomAttributes(
            typeof(TableAttribute), false);
        TableAttribute table = (TableAttribute)attributes[0];
        tableName = table.Name;
    }
    else
    {
        tableName = entity.Name;
    }

    //
    // Much more (nicely factored) code here...
    //
    string projection = TranslateProjection(/* args omitted */);
    string filter = TranslateFilter(/* args omitted */);

    return "SELECT " + projection + " FROM " + tableName + " WHERE " + filter;
}
```

Instead of having the if-else branch right inside TranslateQuery, we would like to have a separate method that will return a table name for further use. In fact, the code that's

In fact, further refactoring could be done to extract a helper method whose sole purpose is to obtain the single custom attribute applied to a type object. This would hide the complexity of GetCustomAttribute, casts, and indexing. We leave such an experimental cleanup to you.

## Code Analysis

Running Code Analysis (available through the project's context menu) typically yields quite a few warnings related to methods. Figure 10.26 shows the result of running the analysis (with all rules enabled in the project's settings) for a simple program. All the warnings should be understood by now, and fixes should be obvious.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_572_0.png)

FIGURE 10.26 Some Code Analysis warnings related to methods.

Warnings can be suppressed if you have some good reason for it. Using the rule sets feature available through the project's configuration settings, each project can decide what level of strictness to apply with regard to various rules. For example, the naming of parameters may be something you don't care much about. That said, keep in mind that publicly visible methods can be called with parameters specified by name. Once you ship with certain names, you must keep it that way to avoid breaking client code.

Two rules deserve a bit more explanation. CA1822 warns about instance methods that do not access instance state. In this particular case, there's no reason we can't mark the Add
method as static. If we do so, we'll see CA1053 for Calc as well because the class contains only static methods. For utility classes like this one, it does make a lot of sense to mark the whole class as static, as discussed earlier in this chapter. Although some rules produce a lot of noise, these two show useful design improvement suggestions.

## Summary

Right at the center of the code aspect of types are methods. While you learned how to invoke methods while covering C# expressions, this chapter went into the aspect of declaring methods in various ways.

First, you learned about method parameters and various ways they can be passed. This includes input-only parameters as well as parameters that are passed by reference or act as an output for the method. You also learned about parameter arrays and the C# 4.0 features of named and optional parameters.

Next, the discussion led you to the notion of signatures and the ability to overload methods. Overloading methods comes in handy quite often to increase an API's flexibility. Resolution of calls based on method groups and overloads finished off the coverage of this concept.

Special kinds of methods were discussed as well. Introduced in C# 3.0, extension methods provide a means to define a static method that can be applied to an object as if it were an instance method. Partial methods (introduced in C# 2.0) aid with code generation tools, and extern methods allow for interoperability scenarios.

Finally, you learned a few things about refactoring and code analysis aspects of working with methods. In the next chapter, you learn about the data aspect of types, embodied by fields, as well as members to expose the data: properties and indexers.
