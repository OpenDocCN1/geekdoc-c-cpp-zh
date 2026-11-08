```
```cpp
City(const wchar_t* name)
{
    Name = wstring(name);
}
wstring Name;
};
}
int _pmain(int /*argc*/, _pchar* /*argv*/[])
{
    auto nyc = Places::Cities::City(L"New York City");

    wcout << L"City name is " << nyc.Name.c_str() << L"\n" << endl;

    return 0;
}
```
```

As you can see, we can nest namespaces and in turn access those namespaces and the types contained within them using the scope resolution operator. You’ll also notice that we used the auto keyword. This is the C++ equivalent of C#’s var keyword.

# The using namespace Directive

Looking at the **NamespacesSample**, notice that we’ve included the line `using namespace std;`. This line looks very similar to the using directive in C#, and it is; however, in C# the using directive automatically brings into scope any types in that namespace which are in any of the referenced assemblies. By contrast, in C++ a using directive only brings into scope the types in the included header files, not all of the types in the libraries that will be linked into your program or library. What are header files you ask? That question provides a good segue into the next chapter.

> > **Note:** Never include a using directive in a header file. If you do that, you don’t just import the types and namespaces in that namespace into the header file, you also import them into any source or header file that includes the header file. This causes really nasty namespace pollution issues. We’ll be discussing header files next, so anything that’s unclear about this should make sense then. Just remember that having a using namespace directive in a header file is a bad idea; only use them in your source code files.