```
...
if (int.TryParse(ageText, out age))
{
    System.Console.Writeline(
        "Hi {0}! You are {1} months old.", firstName,
        age * 12);
}
else
{
    System.Console.Writeline(
        "The age entered ,{0}, is not valid.", ageText);
}
...
```

With the .NET Framework 4, a TryParse() method was also added to enum types.

With the TryParse() method, it is no longer necessary to include a try/catch block simply for the purpose of handling string-to-numeric conversion.

# SUMMARY

This chapter discussed the details of declaring and calling methods. In many ways, this construct is identical to its declaration in C-like languages. However, the addition of the keywords out and ref is more like COM in syntax (the predecessor to CLI technology) than C-like language's use of “&&”. In addition to method declaration, this chapter introduced exception handling.

Methods are a fundamental construct that is a key to writing readable code. Instead of writing large methods with lots of statements, you should use methods for “paragraphs” within your code, whose lengths target roughly ten lines or less. The process of breaking large functions into smaller pieces is one of the ways you can refactor your code to make it more readable and maintainable.

The next chapter considers the class construct and how it encapsulates methods (behavior) and fields (data) into a single unit.