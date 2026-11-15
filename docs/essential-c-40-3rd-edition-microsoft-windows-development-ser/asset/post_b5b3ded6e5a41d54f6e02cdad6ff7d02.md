
The reason for this is to enable IntelliSense, or the ability to predict the members on the objects being selected. For example, because from appears first and identifies the string array Keywords as the data source, the code editor knows that word is of type string. This enables IntelliSense—member access (a dot operation) on word will display only the members of string. If the from clause appeared after the select, then any dot operations prior to the from clause would not know what the data type of word was, and, therefore, would not be able to display a list of word’s members. In Listing 15.1, for example, it wouldn’t be possible to predict that Contains() was a possible member of word. word is referred to as a range variable; it represents each item in the collection.

## Projection

The output of a query expression is an IEnumerable<T> or IQueryable<T> collection.¹ The data type of T is inferred from the select or groupby clause. In Listing 15.1, for example, the data type of string is inferred from select word because word is a string, word’s data type is the type argument of the IEnumerable<T> collection in the from clause. Since Keywords is a string array, it implements IEnumerable<string>, and therefore, word is a string.

The type resulting from an expression which queries a collection of a certain type is by no means limited to be a sequence of that original type. Rather, the select clause allows for projection of data into an entirely different type. Consider the query expression in Listing 15.2, and its corresponding output in Output 15.2.

```
LISTING 15.2: Projection Using Query Expressions
using System;
using System.Collections.Generic;
using System.Linq;
using System.IO;

// ...

static void List1(string rootDirectory, string searchPattern)
{
    IEnumerable<FileInfo> files =
        from fileName in Directory.GetFiles(
            rootDirectory, searchPattern)
        select new FileInfo(fileName);

    foreach (FileInfo file in files)
    {
        Console.WriteLine("{0} ({1})",
            file.Name, file.LastWriteTime);
    }
}

// ...
```

1. Query expression output is practically always IEnumerable<T>, but theoretically, not necessarily. Nothing is stopping anyone from coming up with an implementation of the query operators that returns something else. To do so would be somewhat perverse, but there is no requirement in the language that query operators return IEnumerable<T>.

## OUTPUT 15.2:

```
Account.cs(10/1/2007 11:56:11 AM)
Bill.cs(6/10/2007 9:33:55 PM)
Contact.cs(6/14/2007 11:40:30 PM)
Customer.cs(11/17/2007 2:02:52 AM)
Employee.cs(8/17/2007 1:33:22 AM)
Person.cs(10/22/2007 10:00:03 PM)
```

Notice that this query expression returns an IEnumerable<FileInfo>
rather than the IEnumerable<string> data type returned by System.IO.Directory.GetFiles(). The select clause of the query expression
can potentially project out a data type that is different from what was collected by the from clause expression (Directory.GetFiles()).

In fact, projection such as this is the key driving factor for why C# 3.0
includes anonymous types within the language. Via anonymous types, it
becomes possible to select out the exact data you seek without having to
define an explicit type. For example, Listing 15.3 provides output similar
to that in Listing 15.2, but via anonymous types rather than FileInfo.

## LISTING 15.3: Anonymous Types within Query Expressions

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.IO;

// ...

static void List2(string rootDirectory, string searchPattern)
{
    var files =
        from fileName in Directory.GetFiles(
            rootDirectory, searchPattern)
        select new
        {
            Name = fileName,
            LastWriteTime = file.GetLastWriteTime(fileName)
        };

    foreach (var file in files)
    {
        Console.WriteLine("{0}({1})",
            file.Name, file.LastWriteTime);
    }
}

// ...
```

In this example, the query projects out only the filename and its last file write time. A projection such as the one in Listing 15.3 makes little difference when working with something small such as FileInfo. However, horizontal projection that filters down the amount of data associated with each item in the collection is extremely powerful when the amount of data is significant and retrieving it (perhaps from a different computer over the Internet) is expensive. Rather than retrieving all the data when a query executes, the use of anonymous types enables the capability of storing and retrieving only the required data into the collection. Imagine, for example, a large database that has tables with 30 or more columns. If there were no anonymous types, developers would be required to either use objects containing unnecessary information or define small, specialized classes useful only for storing the specific data required. Instead, anonymous types enable support for types to be defined by the compiler—types that contain only the data needed for their immediate scenario. Other scenarios can have a different projection of only the properties needed for that scenario.

## BEGINNER TOPIC

## Deferred Execution with Query Expressions

The topic of deferred execution appeared in the preceding chapter as well. The same principles also apply to query expressions. Consider again the assignment of selection in Listing 15.1. The assignment itself does not execute the query expression. In other words, during the assignment of selection, word.Contains("**") is not called. Rather, the query expression saves off the selection criteria to be used when iterating over the collection identified by the selection variable.

To demonstrate this point, consider Listing 15.4 and the corresponding output (Output 15.3).

## LISTING 15.4: Deferred Execution and Query Expressions (Example 1)

```
using System;
using System.Collections.Generic;
using System.Linq;

// ...

private static void ShowContextualKeywords2()
{
    IEnumerable<string> selection = from word in Keywords
                                    where IsKeyword(word)
                                    select word;

    foreach (string keyword in selection)
    {
        Console.Write(keyword);
    }
}

// Side effect (console output) included in predicate to show
// deferred execution not as a best practice.
private static bool IsKeyword(string word)
{
    if (word.Contains("**"))
    {
        Console.Write("");
        return true;
    }
    else
    {
        return false;
    }
}

// ...
```

## OUTPUT 15.3:

```
add* alias* ascending* by* descending* dynamic* equals* from* get*
global* group* into* join* let* on* orderby* partial* remove* select*
set* value* var* where* yield*
```

Notice that in Listing 15.4, no space is output within the foreach loop. The space between the contextual keywords is output in the IsKeyword() function, demonstrating that the IsKeyword() function isn't called until the code iterates over selection rather than when selection is assigned.

The point is that although selection is a collection (it is of type IEnumerable<T> after all), at the time of assignment everything following the from clause comprises the selection criteria. Not until we begin to iterate over selection are the criteria applied.

Consider a second example (see Listing 15.5 and Output 15.4).

## LISTING 15.5: Deferred Execution and Query Expressions (Example 2)

```
using System;
using System.Collections.Generic;
using System.Linq;

// ...

private static void CountContextualKeywords()
{
    int delegateInvocations = 0;
    Func<string, string> func =
        text =>
        {
            delegateInvocations++;
            return text;
        };

    IEnumerable<string> selection =
        from keyword in Keywords
        where keyword.Contains("*")
        select func(keyword);

    Console.WriteLine(
        "1. delegateInvocations={0}", delegateInvocations);

    // Executing count should invoke func once for
    // each item selected.
    Console.WriteLine(
        "2. Contextual keyword count={0}", selection.Count());

    Console.WriteLine(
        "3. delegateInvocations={0}", delegateInvocations);

    // Executing count should invoke func once for
```
