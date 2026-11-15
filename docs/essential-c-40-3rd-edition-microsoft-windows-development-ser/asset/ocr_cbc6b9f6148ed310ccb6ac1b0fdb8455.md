field, Program.CommandLine is relevant only to the Program class in this application. The use of the private access modifier defines the intended scope of the class and prevents access from outside the class. You can do this only if the class is nested.

The this member within a nested class refers to an instance of the nested class, not the containing class. One way for a nested class to access an instance of the containing class is if the containing class instance is explicitly passed, such as via a constructor or method parameter.

Another interesting characteristic of nested classes is that they can access any member on the containing class, including private members. The converse to accessing private members is not true, however. It is not possible for the containing class to access a private member on the nested class.

Nested classes are rare. Furthermore, treat public nested classes suspiciously; they indicate potentially poor code that is likely to be confusing and hard to discover.

> **Language Contrast: Java—Inner Classes**
> 
> Java includes not only the concept of a nested class, but also the concept of an inner class. Inner classes correspond to objects that are associated with the containing class instance rather than just a syntactic relationship. In C#, you can achieve the same structure by using an instance field of a nested type within the outer class. A factory method or constructor can ensure a reference to the corresponding instance of the outer class is set within the inner class instance as well.

# Partial Classes

Another language feature added in C# 2.0 is partial classes. Partial classes are portions of a class that the compiler can combine to form a complete class. Although you could define two or more partial classes within the same file, the general purpose of a partial class is to allow the splitting of a class definition across multiple files. Primarily this is useful for tools that