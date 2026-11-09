
### Object Hash Codes

The designers of the FCL decided that it would be incredibly useful if any instance of any object could be placed into a hash table collection. To this end, System.Object provides a virtual GetHashCode method so that an Int32 hash code can be obtained for any and all objects.

If you define a type and override the Equals method, you should also override the GetHashCode method. In fact, Microsoft's C# compiler emits a warning if you define a type that overrides Equals without also overriding GetHashCode. For example, compiling the following type yields this warning: warning CS0659: 'Program' overrides Object.Equals(object o) but does not override Object.GetHashCode()

```csharp
public sealed class Program {
  public override Boolean Equals(Object obj) { ... }
}
```

The reason a type that defines Equals must also define GetHashCode is that the implementation of the System.Collections.Hashtable type, the System.Collections.Generic.Dictionary type, and some other collections require that any two objects that are equal must have the same hash code value. So if you override Equals, you should override GetHashCode to ensure that the algorithm you use for calculating equality corresponds to the algorithm you use for calculating the object's hash code.

Basically, when you add a key/value pair to a collection, a hash code for the key object is obtained first. This hash code indicates which "bucket" the key/value pair should be stored in. When the collection needs to look up a key, it gets the hash code for the specified key object. This code identifies the "bucket" that is now searched sequentially, looking for a stored key object that is equal to the specified key object. Using this algorithm of storing and looking up keys means that if you change a key object that is in a collection, the collection will no longer be able to find the object. If you intend to change a key object in a hash table, you should remove the original key/value pair, modify the key object, and then add the new key/value pair back into the hash table.

Defining a GetHashCode method can be easy and straightforward. But depending on your data types and the distribution of data, it can be tricky to come up with a hashing algorithm that returns a well-distributed range of values. Here's a simple example that will probably work just fine for Point objects.

```csharp
internal sealed class Point {
  private readonly Int32 m_x, m_y;
  public override Int32 GetHashCode() {
    return m_x ^ m_y; // m_x XOR'd with m_y
  }
  ...
}
```

When selecting an algorithm for calculating hash codes for instances of your type, try to follow these guidelines:

- Use an algorithm that gives a good random distribution for the best performance of the hash table.
- Your algorithm can also call the base type's GetHashCode method, including its return value. However, you don't generally want to call Object's or ValueType's GetHashCode method, because the implementation in either method doesn't lend itself to high-performance hashing algorithms.
- Your algorithm should use at least one instance field.
- Ideally, the fields you use in your algorithm should be immutable; that is, the fields should be initialized when the object is constructed, and they should never again change during the object's lifetime.
- Your algorithm should execute as quickly as possible.
- Objects with the same value should return the same code. For example, two String objects with the same text should return the same hash code value.

System.Object's implementation of the GetHashCode method doesn't know anything about its derived type and any fields that are in the type. For this reason, Object's GetHashCode method returns a number that is guaranteed not to change for the lifetime of the object.

![](img/857bdf6cef9e242b53a37f88df9a1287_168_0.png)

> **Important** If you're implementing your own hash table collection for some reason, or you're implementing any piece of code in which you'll be calling GetHashCode, you should never, ever persist hash code values. The reason is that hash code values are subject to change. For example, a future version of a type might use a different algorithm for calculating the object's hash code.
>
> There is a company that was not heeding this important warning. On their website, users could create new accounts by selecting a user name and a password. The website then took the password String, called GetHashCode, and persisted the hash code value in a database. When users logged back on to the website, they entered their password. The website would call GetHashCode again and compare the hash code value with the stored value in the database. If the hash codes matched, the user would be granted access. Unfortunately, when the company upgraded to a new version of the CLR, String's GetHashCode method had changed, and it now returned a different hash code value. The end result was that no user was able to log on to the website anymore!

## The dynamic Primitive Type

C# is a type-safe programming language. This means that all expressions resolve into an instance of a type and the compiler will generate only code that is attempting to perform an operation that is valid for this type. The benefit of a type-safe programming language over a non-type-safe programming language is that many programmer errors are detected at compile time, helping to ensure that the code is correct before you attempt to execute it. In addition, compile-time languages can typically produce smaller and faster code because they make more assumptions at compile time and bake those assumptions into the resulting IL and metadata.

However, there are also many occasions when a program has to act on information that it doesn't know about until it is running. Although you can use type-safe programming languages (like C#) to interact with this information, the syntax tends to be clumsy, especially because you tend to work a lot with strings, and performance is hampered as well. If you are writing a pure C# application, then the only occasion you have for working with runtime-determined information is when you are using reflection (discussed in Chapter 23). However, many developers also use C# to communicate with components that are not implemented in C#. Some of these components could be .NET-dynamic languages such as Python or Ruby, or COM objects that support the IDispatch interface (possibly implemented in native C or C++), or HTML Document Object Model (DOM) objects (implemented using various languages and technologies). Communicating with HTML DOM objects is particularly useful when building a Microsoft Silverlight application.

To make it easier for developers using reflection or communicating with other components, the C# compiler offers you a way to mark an expression's type as dynamic. You can also put the result of an expression into a variable and you can mark a variable's type as dynamic. This dynamic expression/variable can then be used to invoke a member such as a field, a property/indexer, a method, delegate, and unary/binary/conversion operators. When your code invokes a member by using a dynamic expression/variable, the compiler generates special IL code that describes the desired operation. This special code is referred to as the payload. At run time, the payload code determines the exact operation to execute based on the actual type of the object now referenced by the dynamic expression/variable.

Here is some code to demonstrate what I’m talking about.

```csharp
internal static class DynamicDemo {
   public static void Main() {
      dynamic value;
      for (Int32 demo = 0; demo < 2; demo++) {
         value = (demo == 0) ? (dynamic) 5 : (dynamic) "A";
         value = value + value;
         M(value);
      }
   }

   private static void M(Int32 n) { Console.WriteLine("M(Int32): " + n); }
   private static void M(String s) { Console.WriteLine("M(String): " + s); }
}
```
