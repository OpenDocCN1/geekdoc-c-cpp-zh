# UNDERSTANDING REFLECTION

Reflection is when managed code able to read its metadata to figure out assemblies. It allows code to inspect other code within the same System. Elaborate, Java’s static typing system isn’t designed to support the “doSomething” method if the object does not conform to a known interface. But with Reflection, your code can view the object and figure out if it has the “doSomething” method. In addition, you can call it if required.

With Reflection in C#, you can dynamically make an instance of a type and stitch that Type to an existing object. Moreover, you can get the Type from a current object and access its properties. Whenever you use attributes in your code, Reflection provides you access as it gives objects of Type that describe modules, types, and assemblies.

# Defining Reflection in C#

To get an idea about Reflection, there are a few basics you should know about modules, types, and members:

+   - Assemblies include modules.
+   - Modules include types.
+   - Types include members.

You have to use Reflection when you need to check the contents of an assembly as you can get all members of the object by typing “.” before an object when viewing your Visual Studio editor IntelliSense.

A program mirrors itself when it extracts metadata from its assemblies, then uses it to modify its behavior or