# Chapter 2: Data Types

```
}
"";
Console.WriteLine(jsonDialogue);
```

The text for the jsonDialogue variable in Listing 2.21 is, in fact, a special format called JSON. The text is a collection of hierarchical name value pairs that is compatible with JavaScript. Initially it was only prevalent when programming for the web but the format is now a common means (at a minimum) for transferring data. Support for raw string literals is especially important for JSON because it allows direct placement of JSON strings into C# programs without complex and error-prone escape sequences.

The backlashes within the raw string literal assigned to jsonDialogue have no C# significance. Each string, both the name and the value within JSON, is surrounded by quotes. Therefore, JSON text within the value is escaped with a backslash. However, because the text within the entire value is a raw string literal with backslashes has no special significance, backslashes are just normal characters within the represented JSON string. This is a huge advantage using raw string literals for placing JSON within C#. (Representing regular expressions in C# is another format where raw string literals prove extremely helpful.)

In addition, there is the invocation of the Replace() method embedded in the JSON. A list of the string method methods appears in the next section.

# ADVANCED TOPIC

# Understanding the Internals of String Interpolation

String interpolation is shorthand for invoking the string.Format() method. For example, a statement such as

```
Console.WriteLine("
```

```
\$Your full name is {firstName}{lastName}";
```

will be transformed into the C# equivalent of

```
object[] args = new object[] { firstName, lastName };
```