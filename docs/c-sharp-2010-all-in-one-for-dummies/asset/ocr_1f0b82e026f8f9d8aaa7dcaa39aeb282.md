+   - BigEndianUnicode
+   - Unicode
+   - UTF32
+   - UTF7
+   - UTF8

If you need to represent special characters in your files, you need to specify your encoding.

# ## Configuring a template

Template is a directive that specifies the various properties of the T4 text itself. The goal is to affect how the parsing engine interprets the code in the template itself. The options include

+   - **language:** This is the language for the code that does the work. You can emit anything, but the code in the template has to be VB or C#.
+   - **inherits:** This is a class that derives from TextTransformation to be used as the base class.
+   - **culture:** This sets the System.Globalization culture. You know, like en-US or en-GB.
+   - **debug:** Just like the ASP.NET debugger, this sets the return of debug symbols.
+   - **hostspecific:** This is for use with custom hosts — you'll run into it if you are writing for custom hosts.

# ## Including includes

Includes are nice and easy.

Remember ASP classic? No, I don't mean ASP.NET pre-MVC. I mean the old ASP, with VB script, pre-.NET. This is like that. (If you don't, that's okay; I explain it in the next section.)

If you want to include the contents of a file somewhere in your template, just drop the include directive in there and the name of the file in a file attribute.

```
```
<#@ include file="c:\specialsource.cs" #>
```
```

That's all there is to it.