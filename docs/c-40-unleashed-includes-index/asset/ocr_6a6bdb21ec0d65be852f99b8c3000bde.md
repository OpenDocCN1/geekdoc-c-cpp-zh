information is also available to the developer through code, by means of what's known as reflection. In particular, the System.Object base type has a GetType method that returns a System.Type object, describing the object's runtime type:

```
object o = "This is a string";
Type t = o.GetType();
Console.WriteLine(t.FullName);
```

The preceding prints System.String as the type object o. Notice how the declared type is different, though: Instead of assigning the string literal to a variable typed as a string, we assigned it to a variable of the System.Object base type. Obviously, this is perfectly fine to do because every string is an object. What this illustrates, though, is that a clear distinction exists between compile-time type information ("I tell you, dear compiler, that o is of type System.Object") and runtime type information. Although the C# compiler will verify your claim that the string literal indeed is an object, thus making the assignment a valid operation, you'll be restricted to invoking only those operations that are defined on System.Object:

```
// Fails to compile, there's no ToUpper on every System.Object.
string upper = o.ToUpper();

// Does compile fine, as every System.Object has a ToString method.
string print = o.ToString();
```

It's clear that the first line shouldn't compile because compile-time type information available for variable o states it's nothing but a System.Object. The compiler doesn't care what got assigned to o and, in fact, it might not even know where o comes from (for example, when it's a parameter or a field):

```
void DoSomething(object o)
{
    string upper = o.ToUpper(); // Oops!
    ...
}
```

In other words, the compiler doesn't make any assumptions about the type beyond what's stated in the code. Any operations it cannot prove positively to exist at runtime for all instances of the stated type get rejected. That's one of the characteristics of static typing.

Notice, however, that the absence of precise type information at compile time doesn't preclude dynamism at runtime. The use of virtual methods in object-oriented languages makes it possible to dispatch a call at runtime to a more specific implementation of the operation, based on the runtime type. One extreme case of this is the use of interfaces, where the compiler knows what operations will be available at runtime but doesn't have any clue where those are defined physically: