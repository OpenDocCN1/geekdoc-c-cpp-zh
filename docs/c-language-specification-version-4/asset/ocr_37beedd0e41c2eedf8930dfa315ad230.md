+   - Arguments are represented by their documentation name, which is based on their fully qualified name, modified as follows:

Arguments that represent generic types have an appended “`” character followed by the number of type parameters

Arguments having the out or ref modifier have an @ following their type name. Arguments passed by value or via params have no special notation.

Arguments that are arrays are represented as [ lowerbound : size , ... , lowerbound : size ] where the number of commas is the rank less one, and the lower bounds and size of each dimension, if known, are represented in decimal. If a lower bound or size is not specified, it is omitted. If the lower bound and size for a particular dimension are omitted, the “:” is omitted as well. Jagged arrays are represented by one “[]” per level.

Arguments that have pointer types other than void are represented using a * following the type name. A void pointer is represented using a type name of System.Void.

Arguments that refer to generic type parameters defined on types are encoded using the “`” character followed by the zero-based index of the type parameter.

Arguments that use generic type parameters defined in methods use a double-backtick “``” instead of the “`” used for types.

Arguments that refer to constructed generic types are encoded using the generic type, followed by “{”, followed by a comma-separated list of type arguments, followed by “}”.

# A.3.2 ID string examples

The following examples each show a fragment of C# code, along with the ID string produced from each source element capable of having a documentation comment:

+   - Types are represented using their fully qualified name, augmented with generic information:

```
```csharp
enum Color { Red, Blue, Green }
namespace Acme
{
    interface IProcess {...}
    struct ValueType {...}
    class Widget: IProcess
    {
        public class NestedClass {...}
        public interface IMenuItem {...}
        public delegate void Del(int i);
        public enum Direction { North, South, East, West }
    }
    class MyList<T>
    {
        class Helper<U,V> {...}
    }
}
```
```