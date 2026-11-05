attribute. A declarative tag is depicted by square ([ ]) brackets placed above the element it is used for.

+   3. Attributes are used for adding metadata, such as compiler instruction and other information such as comments, description, methods and classes to a program. The .Net Framework provides two types of attributes: *the pre-defined attributes and custom built attributes*.

+   4. Attribute get inherited in the derived classes.

# 13.3.1.1 Types of Attribute

Attributes can be either **Predefined attributes (intrinsic)** or custom. **Intrinsic attributes** are supplied as part of the Common Language Runtime (CLR), and they are integrated into .NET. **Custom attributes** are attributes one creates for own purposes. Most programmers will use only intrinsic attributes, though custom attributes can be a powerful tool when combined with reflection.

# Attribute targets

The entity on which the attribute is applied is termed as the target. Some attributes are applied to an assembly, others to a class or interface, and some, such as [WebMethod], are applied to class members. These are called the attribute targets. **Possible attribute targets are described below.**

| Possible attribute targets | |
|---|---|
| **Member name** | **Usage** |
| All | Applied to any of the following elements: assembly, class, constructor, delegate, enum, event, field, interface, method, module, parameter, property, return value, or struct |
| Assembly | Applied to the assembly itself |
| Class | Applied to instances of the class |
| Constructor | Applied to a given constructor |
| Delegate | Applied to the delegated method |
| Enum | Applied to an enumeration |