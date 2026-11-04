```
class Program
{
    static void Main()
    {
    }
}
```

Main is the managed code entry-point method for our application. Its body, delimited by curly braces, contains the statements that get executed by the application. In this case, our method body is empty.

# CASE SENSITIVITY

Notice the casing of the Main method, with its first character uppercase. C# is a case-sensitive language, just like other C derivatives such as C++ and Java. In other words, method names that differ only in case denote different methods; so main and Main are not the same. C# requires the managed code entry point to be styled exactly as shown in the previous fragment.

Case sensitivity applies not only to method names. Keywords, names for types and their members, namespaces—they all are subject to case-sensitive treatment.

Let’s point out an important point immediately. For an assembly to be Common Language Specification (CLS)-compliant, no publicly visible type or member should differ only in case as compared to one of its peers. If this were the situation, non-case-sensitive languages like Visual Basic would be in trouble, resolving the name unambiguously.

C# doesn’t have the notion of global methods, meaning that all methods (and other sorts of members, as you will see) need to be contained in a type definition. In our example, the type is a class called Program. In the next chapter, we look at the distinction between types and classes, so ignore this detail for now.

# Method Signatures

Methods also have a signature, which you could see as the recipe that describes how the method is to be called. The important parts of a method signature include the method name, the return type, and the parameters. It also contains modifiers that are used to “modify” the behavior of the method.

Let’s decipher our Main method signature shown in Figure 4.1 with regard to these concepts:

+   - One modifier, the static keyword, is applied to the method. This means the method does not operate on a specific instance of the containing type. To explain this further, we first have to learn about types and object-oriented programming, which is subject of Chapter 14, “Object-Oriented Programming.” Stay tuned.