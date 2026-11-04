Besides use of the return keyword as a prefix to a custom attribute, other such prefixes exist. One is assembly, to apply an assembly-wide custom attribute. Good examples of this are found in the AssemblyInfo.cs file, which can be found by expanding the Properties node in Solution Explorer:

```
[assembly: AssemblyTitle("CS40Dynamic")]
```

You read more about assemblies in Chapter 25, “Assemblies, and Application Domains.” Other attribute target specifiers include module (a part of an assembly), field, event, property, method, param, and type (most of which are optional and can be inferred from the context in which they occur).

# When to Use dynamic: Case Study with IronPython

All powerful tools should be used with care, and dynamic is no different. By no means is dynamic meant to be a substitute for static typing. Use of static typing provides many benefits, such as compile-time checking, tooling advantages, a more beneficial performance profile, and so on.

The main philosophy of .NET 4 dynamic is to make reaching out to dynamically typed code and data simpler. Or to say it in another way: Why should someone be punished for embracing some piece of dynamically typed code (for example, using some Python-based library), when calling it from languages like C#? In short, C# 4.0 dynamic allows developers to “ease into” the domain of dynamic typing with minimum friction.

To this end, all examples of dynamic shown in this chapter so far have been violating the rule of “static where possible, dynamic where necessary,” because you could have written those simple examples in a statically typed manner. With the example presented here, we use dynamic for what it’s really meant to be used for: building bridges to the dynamic world.

# Getting IronPython

In this example, we call a Python object from inside C#, leveraging the dynamic feature. Any DLR language would actually work to illustrate this kind of bridging, but Python deserves a special treatment in introductory chapters on the subject because it’s the first dynamic language citizen on the DLR. This implementation of the language on the DLR is known as IronPython and is described as follows on the project’s website:

> *IronPython is an open-source implementation of the Python programming language which is tightly integrated with the .NET Framework. IronPython can use the .NET Framework and Python libraries, and other .NET languages can use Python code just as easily.*

We illustrate both statements made in this description. One is to leverage the .NET libraries from inside Python (with something as simple as operator overloads on BCL types), and the other one, indicated in bold, is to call into Python code from C#. The official IronPython home page is http://www.ironpython.net and provides links to downloads hosted on Microsoft’s CodePlex website. The site also has an online interactive Python in the browser playground, based on Silverlight.