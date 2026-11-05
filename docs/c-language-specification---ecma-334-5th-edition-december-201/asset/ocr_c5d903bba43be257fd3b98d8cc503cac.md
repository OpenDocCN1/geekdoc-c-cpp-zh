+   - No white space is placed in the string.
+   - The first part of the string identifies the kind of member being documented, via a single character followed by a colon. The following kinds of members are defined:

| Character | Description |
|---|---|
| E | Event |
| F | Field |
| M | Method (including constructors, finalizers, and operators) |
| N | Namespace |
| P | Property (including indexers) |
| T | Type (such as class, delegate, enum, interface, and struct) |
| ! | Error string; the rest of the string provides information about the error. For example, the documentation generator generates error information for links that cannot be resolved. |

+   - The second part of the string is the fully qualified name of the element, starting at the root of the namespace. The name of the element, its enclosing type(s), and namespace are separated by periods. If the name of the item itself has periods, they are replaced by # (U+0023) characters. (It is assumed that no element has this character in its name.)
+   - For methods and properties with arguments, the argument list follows, enclosed in parentheses. For those without arguments, the parentheses are omitted. The arguments are separated by commas. The encoding of each argument is the same as a CLI signature, as follows:

+   - Arguments are represented by their documentation name, which is based on their fully qualified name, modified as follows:
+     - Arguments that represent generic types have an appended "`" character followed by the number of type parameters
+     - Arguments having the out or ref modifier have an @ following their type name. Arguments passed by value or via params have no special notation.
+     - Arguments that are arrays are represented as [ lowerbound : size , ... , lowerbound : size ] where the number of commas is the rank less one, and the lower bounds and size of each dimension, if known, are represented in decimal. If a lower bound or size is not specified, it is omitted. If the lower bound and size for a particular dimension are omitted, the ":" is omitted as well. Jagged arrays are represented by one "[]" per level.
+     - Arguments that have pointer types other than void are represented using a * following the type name. A void pointer is represented using a type name of System.Void.
+     - Arguments that refer to generic type parameters defined on types are encoded using the "`" character followed by the zero-based index of the type parameter.
+     - Arguments that use generic type parameters defined in methods use a double-backtick "``" instead of the "`" used for types.
+     - Arguments that refer to constructed generic types are encoded using the generic type, followed by "{", followed by a comma-separated list of type arguments, followed by "}".