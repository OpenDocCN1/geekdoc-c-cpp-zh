For example, FindFirstRedEyePixel() returns a reference to an item in the image array, which was a parameter to the function. Similarly, if the image was stored as a field within the class, you could return the field by reference:

```
byte[] _Image;
public ref byte[] Image { get { return ref _Image; } }
```

Second, ref locals are initialized to refer to a particular variable and can’t be modified to refer to a different variable.

There are several return-by-reference characteristics of which to be cognizant:

+   - If you’re returning a reference, you obviously must return it. This means, therefore, that in the example in Listing 5.16, even if no red-eye pixel exists, you still need to return a reference byte. The only workaround would be to throw an exception. In contrast, the by-reference parameter approach allows you to leave the parameter unchanged and return a bool indicating success. In many cases, this might be preferable.

+   - When declaring a reference local variable, initialization is required. This involves assigning it a ref return from a function or a reference to a variable:

```
ref string text; // Error
```

+   - Although it’s possible in C# 7.0 to declare a reference local variable, declaring a field of type ref isn’t allowed:

```
class Thing { ref string _Text; /* Error */ }
```

+   - You can’t declare a by-reference type for an auto-implemented property:

```
class Thing { ref string Text {get;set; } /* Error */ }
```

+   - Properties that return a reference are allowed:

```
class Thing { string _Text = "Inigo Montoya";
ref string Text { get { return ref _Text; } } }
```

+   - A reference local variable can’t be initialized with a value (such as null or a constant). It must be assigned from a by-reference-returning member or a local variable, field, or array element:

```
ref int number = null; ref int number = 42; // ERROR
```