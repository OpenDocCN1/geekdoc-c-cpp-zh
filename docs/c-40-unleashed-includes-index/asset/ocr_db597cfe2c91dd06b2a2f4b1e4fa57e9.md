are parameterized on other types by their very nature, you can mix and match all sorts of types together to build up a new one:

```
List<HashSet<Dictionary<string, Tuple<int,int>>>>
```

Having to specify such long type names repeatedly is not only tedious, it also reduces code readability significantly. Starting from C# 3.0, type inference for local variables can be used to shorten code:

```
var lotteryNumbers = new Dictionary<string, List<int>>();
```

Now it fits again on a single line, reducing the syntactical noise a lot.

# ABOUT SEMICOLONS AND UNEMPLOYED UNDERSCORES

If it wasn’t clear yet, C# allows code to be split across multiple lines. The end of a statement is indicated by the use of a semicolon character, as is common in C-style languages. Other languages, such as Visual Basic, initially chose an opposite approach: To split a code line, use a line continuation marker. In Visual Basic’s case, that was the underscore character. I’m using the past tense here because the need for a line continuation has been removed almost completely in Visual Basic 10. In tough economic times, to assist the unemployed underscores in finding their next challenge, a website was created for them: www.unemployedunderscores.com.

But there’s more. Although the usage simplification for generic types is a very convenient effect that comes from introducing this form of type inference, it’s not a requirement. You could live perfectly without it (although maybe just a little annoyed). However, in C# 3.0, another feature was introduced as part of the LINQ mission: anonymous types. We defer exhaustive coverage of this feature until Chapter 19, “Language Integrated Query Essentials,” in the section, “Anonymous Types and Object Initializers,” but here’s a sample:

```
var person = new { Name = "Bart", Age = 26 };
```

This creates an instance of a type with two properties called Name and Age, of type string and int, respectively, initialized with the specified data. What’s special about the code is the fact that we didn’t specify a type name at all. Instead, we let the compiler bake a type on the fly, with the desired “shape” to hold the contained data. But if the compiler generated a type for us, of which we can’t know the name because we didn’t have to specify it, how can we refer to it? The rescue lies in the use of var to let the compiler insert the type name on our behalf.

To see this in action, type the preceding code in some C# project and observe the IntelliSense in Visual Studio once more, as shown in Figure 4.23. As you can see, the tool knows precisely what we’re talking about; we haven’t lost any of the type information.