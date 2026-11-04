+   - **culture:** This sets the `System.Globalization` culture. You know, like en-US or en-GB.
+   - **debug:** Just like the ASP.NET debugger, this sets the return of debug symbols.
+   - **hostspecific:** This is for use with custom hosts — you'll run into it if you are writing for custom hosts.

# Including includes

Includes are nice and easy.

Remember ASP classic? No, I don't mean ASP.NET pre-MVC. I mean the old ASP, with VB script, pre-.NET. This is like that. (If you don't, that's okay; I explain it in the next section.)

If you want to include the contents of a file somewhere in your template, just drop the include directive in there and the name of the file in a file attribute.

```
<#@ include file="c:\specialsource.cs" #>
```

That's all there is to it.

# Importing items and assemblies

The import and assembly directives assist with writing code in a template. In the example in the previous section, I emitted text, but in the real examples that you find in MSDN, you write C# or VB code to modify the text.

If you want that code to use .NET Framework constructs, you need to reference the assembly and import the namespace. For instance, if you are going to get values from a file in your template, you need the System.IO library.

First you need to reference the assembly, unless you are certain the assembly will be referenced in the project. Then you should import the namespace so that you don't have to reference items via fully qualified names, like this:

```
<#@ assembly name="System.IO.DLL" #>
<#@ import namespace="System.IO" #>
```

Then, you can reference the file maintenance classes inside the code of the template. You reference code using the <# and #> statements.