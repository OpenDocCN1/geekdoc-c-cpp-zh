True
False
False
False

The s and t variables refer to two distinct string instances containing the same characters. The first comparison outputs True because the predefined string equality operator (§7.10.7) is selected when both operands are of type string. The remaining comparisons all output False because the predefined reference type equality operator is selected when one or both of the operands are of type object.

Note that the above technique is not meaningful for value types. The example

```
class Test
{
    static void Main() {
        int i = 123;
        int j = 123;
        System.Console.WriteLine((object)i == (object)j);
    }
}
```

outputs False because the casts create references to two separate instances of boxed int values.

# 7.10.7 String equality operators

The predefined string equality operators are:

```
bool operator ==(string x, string y);
bool operator !=(string x, string y);
```

Two string values are considered equal when one of the following is true:

+   - Both values are null.
+   - Both values are non-null references to string instances that have identical lengths and identical characters in each character position.

The string equality operators compare string values rather than string references. When two separate string instances contain the exact same sequence of characters, the values of the strings are equal, but the references are different. As described in §7.10.6, the reference type equality operators can be used to compare string references instead of string values.

# 7.10.8 Delegate equality operators

Every delegate type implicitly provides the following predefined comparison operators:

```
bool operator ==(System.Delegate x, System.Delegate y);
bool operator !=(System.Delegate x, System.Delegate y);
```

Two delegate instances are considered equal as follows:

+   - If either of the delegate instances is null, they are equal if and only if both are null.
+   - If the delegates have different run-time type they are never equal.
+   - If both of the delegate instances have an invocation list (§15.1), those instances are equal if and only if their invocation lists are the same length, and each entry in one’s invocation list is equal (as defined below) to the corresponding entry, in order, in the other’s invocation list.

The following rules govern the equality of invocation list entries:

+   - If two invocation list entries both refer to the same static method then the entries are equal.