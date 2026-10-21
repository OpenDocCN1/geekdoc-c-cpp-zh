This catch block catches the exception because it now has the correct type.

To throw the exception so that it can be caught by the original catch block, you must change the code in the try block:

```
try
{
    throw gcnew String(L"Catch me if you can.");
}
catch(String^ ex)                // OK. Exception thrown is of this type
{
    Console::WriteLine(L"String^: {0}",ex);
}
```

Now the exception is a String object and is thrown as type String^, a handle that references the string.

You can use function templates in your C++/CLI programs, but you have an additional capability called generic functions that looks remarkably similar; however, there are significant differences.

# Understanding Generic Functions

Although generic functions appear to do the same thing as function templates and therefore at first sight seem superfluous, generic functions work rather differently from template functions and the differences make them a valuable additional capability in CLR programs. When you use a function template, the compiler generates the source code for functions that you require from the template; this generated code is then compiled along with the rest of your program code. In some cases this can result in many functions being generated and the size of the execution module may be increased substantially. On the other hand a generic function specification is itself compiled, and when you call a function that matches the generic function specification, actual types are substituted for the type parameters at execution time. No extra code is generated at compile time and the code-bloat that can arise with template functions does not occur.

Some aspects of defining generic function depend on a knowledge of stuff that comes in later chapters but it will al be clear eventually. I'll provide minimal explanations here of the things that are new and you'll learn the detail later in the book.

# Defining Generic Functions

You define a generic function using type parameters that are replaced by actual types when the function is called. Here's an example of a generic function definition:

```
generic<typename T> where T:IComparable
T MaxElement(array<T>^ x)
{
    T max = x[0];
    for(int i = 1; i < x->Length; i++)
        if(max->CompareTo(x[i]) < 0)
            max = x[i];
    return max;
}
```