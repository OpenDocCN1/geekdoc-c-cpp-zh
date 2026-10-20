same object that the original does. A deep copy creates a new object that copies all member variables as well. All reference types are cloned recursively in the copy. In built-in types, such as integers, the deep and shallow copies produce the same results. Which one does a type support? That depends on the type. But mixing shallow and deep copies in the same object causes quite a few inconsistencies. When you go wading into the ICloneable waters, it can be hard to escape. Most often, avoiding ICloneable altogether makes a simpler class. It’s easier to use, and it’s easier to implement.

Any value type that contains only built-in types as members does not need to support ICloneable; a simple assignment copies all the values of the struct more efficiently than Clone(). Clone() must box its return so that it can be coerced into a System.Object reference. The caller must perform another cast to extract the value from the box. You’ve got enough to do. Don’t write a Clone() function that replicates an assignment.

What about value types that contain reference types? The most obvious case is a value type that contains a `string`:

```
public struct ErrorMessage
{
    private int errCode;
    private int details;
    private string msg;

    // details elided
}
```

string is a special case because this class is immutable. If you assign an error message object, both error message objects refer to the same string. This does not cause any of the problems that might happen with a general reference type. If you change the msg variable through either reference, you create a new string object (see Item 16).

The general case of creating a struct that contains arbitrary reference variables is more complicated. It’s also far rarer. The built-in assignment for the struct creates a shallow copy, with both structs referring to the same object. To create a deep copy, you need to clone the contained reference type, and you need to know that the reference type supported a deep copy with its Clone() method. Even then, that will only work if the contained reference type also supports ICloneable, and its Clone() method creates a deep copy.