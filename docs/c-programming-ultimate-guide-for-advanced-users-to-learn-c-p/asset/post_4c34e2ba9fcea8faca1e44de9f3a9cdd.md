
```csharp
string s = "overloaded operators " + "are cool"
```

It is instinctively comprehended that the statement is performing string concatenation.

Overloaded operators are methods. In particular, they are methods with a special syntax. You can understand operators by considering overloaded operators as two parts. The first part implements a standard named method that performs the operation that the operator would perform. The second part defines the operator method using the special syntax and calls the named method within the operator. (Obviously, you could generally skip overloading operators, but that would be unpleasant.)

## Coding Operator Methods

The method signature for operator methods is fundamentally the same as ordinary methods. Determine a return type and argument types and names; at the same time, rather than a method name, you use the keyword operator and the operator token where you would have used the method name.

Drawing from the help file examples, we could implement a complex number class. (Complex numbers have a real and imaginary part.) We could implement an overloaded addition operator that includes the real parts and the imaginary parts of two complex numbers, yielding another complex number that is the sum of the two included complex numbers.

The code listing is excerpted from a struct that characterizes a complex number as a number that is initialized with a real number and scalar part of the imaginary number. For instance, if you construct a complex number with 2 for the real argument and 3 for the imaginary part, then you get the complex number 2 + 3i. The overloaded operator in the previous example characterizes the + operator for Complex types as a static method that takes two Complex objects and returns another Complex object that is the sum of the two arguments. In the example, you would invoke this operator+ method by composing a statement that includes two complex numbers.

When you select the resource file from the Solution Explorer, a resource editor is shown, as appeared in Figure 2-5. You can add resource content to the resource file using the editor. As appeared in the figure, string resource entries are presented as a table of name, value, comment, type, and mimetype data. This is like resource files. The greatest difference is that resource files in C# are stored as XML documents, as opposed to plain text. You can see the XML by clicking the XML tab (appeared in Figure 2-5).

The Utility.cs module shows how to use a ResourceManager to read information from the resource (.resx) file. To read string data from a resource file, make an instance of the ResourceManager class defined in the System.Resources namespace and call the GetString method. The following code listing shows using the ResourceManager as it is implemented in the Utility.cs module.

The ResourceManager has to know the resource file that you need to load and the assembly that contains that resource file. In the example, we are getting the default-named resource file in the executing assembly.

At long last, we come to multithreading. Multithreading is a complex subject. There are a few facets to multithreading, so we will confine our discussion to multithreading in this section to the manner in which it was used to help implement the AssemblyViewer.

The AssemblyViewer utilizes a different thread to show the Splash screen while the application is loaded. A luxury no doubt, yet what is the purpose of a splash screen if it is executed in a linear fashion? That is, while the splash screen is loading, no genuine initialization happens, and I never liked letting the splash screen contain the initialization code. (You are probably going to discover, nonetheless, that many splash screens do really contain initialization code.)

In our example application, the splash screen is on its own thread. There are four different ways to imagine apparently asynchronous behavior in C#. The Timer control and Application.Idle event give event-driven synchronous behavior. Controls support the asynchronous BeginInvoke and EndInvoke.

The Show method is defined on lines 11 through 26 in Listing 2-3. This Show method gradually blurs in the form by modifying the Opacity. Shockingly, because Windows Forms controls are not thread safe, the Opacity must be changed on the same thread as the one it lives on. The Show method isn't on that thread.

The way that we really update the Opacity value is by calling the form's Invoke method. Invoke is thread safe; Invoke marshals the delegate argument into the same thread as the thread that the calling item is on. (Once more, without delegates safe threading would not be conceivable.)

Invoke requires a MethodInvoker delegate and executes the code inside the method used to initialize the delegate. The Increment method refreshes the Opacity value. The done field is used to indicate that the form is obscured. We lock the Done method while we are refreshing it, preventing the thread running Show from looking at the Done value until it has been refreshed.

The first two statements make instances of two complex numbers. The last statement invokes the operator+ method, returning another object to the variable e. The most ideal approach to understand overloaded operators is to write some basic examples and set breakpoints on the statements that invoke the operator and in the operator method. You will rapidly observe that the operation results in a method invocation.

## Overloading Operator Guidelines and Limitations

Be prudent about defining overloaded operators. The most significant thing to abstain from doing is making operators that are outlandish. For instance, overloading the addition operator to perform subtraction. Do not do this. Following these essential rules for overloading operators will keep you out of trouble:

- Define methods that perform the operation using the op_ prefix followed by the name of the operator to support languages like Visual Basic .NET that don't support operator overloading.
- Implement the overloaded operator by calling the named method. (Why classify the operator behavior twice?)
- Overload an operator only in the class the operator applies to.
- Use operator overloading when the operation is instinctive and the outcome appears to be coherent.
- Overload operators evenly. If you implement addition, then implement subtraction.

## Attributes

It is colloquialisms like interface and attributes that push us into difficulty as software engineers. The explanation is that these terms carry out double duty. For a considerable length of time, "interface" implied essentially the members declared in a class. When COM was presented, interface took on another significance; interface turned into a construct—a great deal like a class. (For VB developers, interfaces and classes blur a lot.)

A similar issue exists for "attribute" and the figure of speech Attribute. In the general sense, "attribute" is synonymous with "property." An attribute is a property of a type. The C# Attribute itself is really a class. (There are probably going to be the same number of confounding dialogs encompassing attributes as there are about parent and child, superclass and subclass, and object and class.)

In ADVANCED C# an Attribute with a capital A will be a class that adds metadata to your assembly.

Metadata, or extra information, was added to help annihilate "DLL Hell." Historically outer information that an application required was stored in a library or INI file. Properties enable this supporting cast of information to go with the assembly. Attribute classes enable you to add the metadata to your assemblies, and Reflection enables you to remove that metadata when you need it. This is closely resembling reading and writing from the library. Because of having the metadata cunningly collapsed into the assembly, conveying C# applications is more
