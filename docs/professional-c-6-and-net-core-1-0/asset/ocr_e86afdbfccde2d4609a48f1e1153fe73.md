This section starts with the core `WhatsNewAttributes` assembly. The source code is contained in the file `WhatsNewAttributes.cs`, which is located in the `WhatsNewAttributes` project of the `WhatsNewAttributes` solution in the example code for this chapter.

The sample code for `WhatsNewAttributes` makes use of the following dependencies and namespaces:

# Dependencies

NETStandard.Library

# Namespaces

System

The `WhatsNewAttributes.cs` file defines two attribute classes, `LastModifiedAttribute` and `SupportsWhatsNewAttribute`. You use the attribute `LastModifiedAttribute` to mark when an item was last modified. It takes two mandatory parameters (parameters that are passed to the constructor): the date of the modification and a string containing a description of the changes. One optional parameter named `issues` (for which a `public` property exists) can be used to describe any outstanding issues for the item.

In practice, you would probably want this attribute to apply to anything. To keep the code simple, its usage is limited here to classes and methods. You allow it to be applied more than once to the same item (`AllowMultiple=true`) because an item might be modified more than once, and each modification has to be marked with a separate attribute instance.

`SupportsWhatsNew` is a smaller class representing an attribute that doesn’t take any parameters. The purpose of this assembly attribute is to mark an assembly for which you are maintaining documentation via the `LastModifiedAttribute`. This way, the program that examines this assembly later knows that the assembly it is reading is one on which you are actually using your automated documentation process. Here is the complete source code for this part of the example (code file `WhatsNewAttributes/WhatsNewAttributes.cs`):

```
using System;

namespace WhatsNewAttributes
{
    [AttributeUsage(AttributeTargets.Class |
AttributeTargets.Method,
        AllowMultiple=true, Inherited=false)]
    public class LastModifiedAttribute: Attribute
    {
        private readonly DateTime _dateModified;
        private readonly string _changes;

        public LastModifiedAttribute(string dateModified, string changes)
        {
            _dateModified = DateTime.Parse(dateModified);
            _changes = changes;
```