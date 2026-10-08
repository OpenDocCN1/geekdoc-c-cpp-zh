# Classy Generics: Writing Your Own 171

```
// See if the object is the right type, then cast it ...
if(aList[i] is Student) // Is the object there a Student?
{
    Student aStudent = (Student)aList[i]; // Yes, so it's safe to cast.
    // Or do the conversion and see it went well...
    Student student = aList[i] as Student; // Extract a Student, if present;
    if(aStudent != null) // if not, "as" returns null.
}
// OK to use aStudent; "as" operator worked.
```

You can avoid all this extra work using generics. Generic collections work like arrays: You specify the one and only type you can hold when you declare them.

# Generics are efficient

Polymorphism allows the Object to hold any other type — as with the egg carton analogy in the previous section. But you can incur a penalty by putting in value-objects — numeric, char, and bool types and structs — taking them out. That's because value-type objects that you have to be boxed (See Book II for more polymorphism).

Boxing isn worthless unless generic is big (although the amount of boxing going on can startle you and be more costly than you imagined). If you're stalling a thousand, or a million, into a generic collection takes about 20 minutes long, plus extra space on the memory heap, reference-type objects are stored. Boxing can also lead to subtle errors that will have you tearing your hair out. Generic collections eliminate boxing and unboxing.

Don't get me wrong: Boxing allows C# to have a unified type system, which has great benefits that usually outweigh the inconvenience and cost of boxing.

# Classy Generics: Writing Your Own

Besides the built-in generic collection classes, C# lets you write your own generic classes, whether they collections or not. The point is that you can create generic versions of classes that you design.

Picture a class definition full of <T>. When you instantiate such a class, you specify a type to replace its generic placeholders, just as you do with the generic collections. How simple these declarations are:

```
LinkedList<int> aList = new LinkedList<int>(); // Built-in LinkedList class
MyClass<int> aClass = new MyClass<int>(); // Custom class
```