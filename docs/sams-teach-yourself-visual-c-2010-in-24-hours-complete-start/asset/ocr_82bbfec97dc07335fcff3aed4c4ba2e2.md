Q. What is meant by garbage collection and why is it important?

A. Garbage collection is a runtime service provided by the .NET Framework that frees you from having to handle memory allocation and deallocation manually. This enables you to create more stable applications by preventing many of those common programming errors and enables you to focus your time on the business logic your application requires.

Q. What is C#?

A. C# is an object-oriented, type-safe programming language that runs on the .NET Framework.

Q. Are C# programs compiled?

A. Yes, C# programs are compiled at development time to common intermediate language (CIL). At runtime, they are compiled to executable object code by the Just-In-Time (JIT) compiler.

# # Workshop

# ## Quiz

+   1. What are the components of the .NET Framework?
2. Why is the common type system important?
3. What is common intermediate language (CIL)?
4. Why is the Framework class library important?
5. What does the dynamic language runtime (DLR) provide to C#?
6. Is the following code valid in C#?

```
```
class Program
{
    static void Main()
    {
        const int LettersInEnglishAlphabet = 26

        System.Console.WriteLine(
            "There are {0} letters in the English alphabet.",
            LettersInEnglishAlphabet)
    }
}
```
```