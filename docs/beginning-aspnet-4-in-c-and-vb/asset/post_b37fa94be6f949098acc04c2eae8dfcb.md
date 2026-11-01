
```csharp
{
    Console.WriteLine("Element {0} = {1}", i, *(pArray + i));
}

Console.ReadLine();
}
}
}
```

The output from the QuickArray example is illustrated in Figure 13-7.

![](img/d7d2ffa0a76feaab821930e95daace93_393_0.png)

**FIGURE 13-7**

## SUMMARY

Remember, to become a truly proficient C# programmer, you must have a solid understanding of how memory allocation and garbage collection work. This chapter described how the CLR manages and allocates memory on the heap and the stack. It also illustrated how to write classes that free unmanaged resources correctly, and how to use pointers in C#. These are both advanced topics that are poorly understood and often implemented incorrectly by novice programmers.

This chapter should be treated as a companion to what you learn from Chapter 15 on error handling and in Chapter 20 when dealing with threading. The next chapter of this book looks at reflection in C#.

## 14 Reflection

### WHAT'S IN THIS CHAPTER?

- Using custom attributes
- Inspecting the metadata at runtime using reflection
- Building access points from classes that enable reflection

This chapter focuses on custom attributes and reflection. Custom attributes are mechanisms that allow you to associate custom metadata with program elements. This metadata is created at compile time and embedded in an assembly. Reflection is a generic term that describes the ability to inspect and manipulate program elements at runtime. For example, reflection allows you to:

- Enumerate the members of a type
- Instantiate a new object
- Execute the members of an object
- Find out information about a type
- Find out information about an assembly
- Inspect the custom attributes applied to a type
- Create and compile a new assembly

This list represents a great deal of functionality and encompasses some of the most powerful and complex capabilities provided by the .NET Framework class library. Although this chapter does not have the space to cover all the capabilities of reflection, it focuses on those elements that you are likely to use most frequently.

To demonstrate custom attributes and reflection, you develop an example based on a company that regularly ships upgrades of its software and wants to have details of these upgrades documented automatically. In the example, you define custom attributes that indicate the date when program elements were last modified, and what changes were made. You then use reflection to develop an application that looks for these attributes in an assembly, and can automatically display all the details about what upgrades have been made to the software since a given date.

Another example in this chapter considers an application that reads from or writes to a database and uses custom attributes as a way of marking which classes and properties correspond to which database tables and columns. By reading these attributes from the assembly at runtime, the program is able to automatically retrieve or write data to the appropriate location in the database, without requiring specific logic for each table or column.

error. For example, if the attribute class indicates that the attribute can be applied only to classes, but you have applied it to a struct definition, a compilation error will occur.

To continue with the example, assume that you have defined the FieldName attribute like this:

```csharp
[AttributeUsage(AttributeTargets.Property,
    AllowMultiple=false,
    Inherited=false)]
public class FieldNameAttribute: Attribute
{
    private string name;
    public FieldNameAttribute(string name)
    {
        this.name = name;
    }
}
```

The following sections discuss each element of this definition.

### AttributeUsage Attribute

The first thing to note is that the attribute class itself is marked with an attribute — the System.AttributeUsage attribute. This is an attribute defined by Microsoft for which the C# compiler provides special support. (You could argue that AttributeUsage isn’t an attribute at all; it is more like a meta-attribute, because it applies only to other attributes, not simply to any class.) The primary purpose of AttributeUsage is to identify the types of program elements to which your custom attribute can be applied. This information is given by the first parameter of the AttributeUsage attribute — this parameter is mandatory, and is of an enumerated type, AttributeTargets. In the previous example, you have indicated that the FieldName attribute can be applied only to properties, which is fine, because that is exactly what you have applied it to in the earlier code fragment. The members of the AttributeTargets enumeration are:

- `All`
- `Assembly`
- `Class`
- `Constructor`
- `Delegate`
- `Enum`
- `Event`
- `Field`
- `GenericParameter` (.NET 2.0 and higher only)
- `Interface`
- `Method`
- `Module`
- `Parameter`
- `Property`
- `ReturnValue`
- `Struct`

This list identifies all the program elements to which you can apply attributes. Note that when applying the attribute to a program element, you place the attribute in square brackets immediately before the element. However, two values in the preceding list do not correspond to any program element: Assembly and Module. An attribute can be applied to an assembly or module as a whole instead of to an element in your

can download from the Wrox web site at www.wrox.com) as a combined Visual Studio solution, as discussed in Chapter 16, “Visual Studio 2010.” The download includes the required Visual Studio 2010 solution files.

### The WhatsNewAttributes Library Assembly

This section starts with the core WhatsNewAttributes assembly. The source code is contained in the file WhatsNewAttributes.cs, which is located in the WhatsNewAttributes project of the WhatsNewAttributes solution in the example code for this chapter. The syntax for doing this is quite simple. At the command line, you supply the flag target:library to the compiler. To compile WhatsNewAttributes, type the following:

```
csc /target:library WhatsNewAttributes.cs
```

The WhatsNewAttributes.cs file defines two attribute classes, LastModifiedAttribute and SupportsWhatsNewAttribute. The attribute LastModifiedAttribute is the attribute that you can use to mark when an item was last modified. It takes two mandatory parameters (parameters that are passed to the constructor): the date of the modification and a string containing a description of the changes. There is also one optional parameter named issues (for which a public property exists), which can be used to describe any outstanding issues for the item.

In practice, you would probably want this attribute to apply to anything. To keep the code simple, its usage is limited here to classes and methods. You will allow it to be applied more than once to the same item (AllowMultiple=true) because an item might be modified more than once, and each modification will have to be marked with a separate attribute instance.

SupportsWhatsNew is a smaller class representing an attribute that doesn’t take any parameters. The idea of this attribute is that it is an assembly attribute that is used to mark an assembly for which you are maintaining documentation via the LastModifiedAttribute. This way, the program that will examine this assembly later on knows that the assembly it is reading is one on which you are actually using your automated documentation process. Here is the complete source code for this part of the example:

```csharp
using System;

namespace WhatsNewAttributes
{
    [AttributeUsage(
        AttributeTargets.Class | AttributeTargets.Method,
        AllowMultiple=true, Inherited=false)]
    public class LastModifiedAttribute: Attribute
    {
        private readonly DateTime _dateModified;
        private readonly string _changes;

        public LastModifiedAttribute(string dateModified, string changes)
        {
            _dateModified = DateTime.Parse(dateModified);
            _changes = changes;
        }

        public DateTime DateModified
        {
            get { return _dateModified; }
        }

        public string Changes
        {
            get { return _changes; }
        }

        public string Issues { get; set; }
    }
}
```
