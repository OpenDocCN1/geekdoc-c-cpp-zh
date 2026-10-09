The problem is that in a managed environment, data can move, thereby invalidating the address. The error message is “You can only take the address of [an] unfixed expression inside a fixed statement initializer.” In this case, the byte referenced appears within an array, and an array is a reference type (a movable type). Reference types appear on the heap and are subject to garbage collection or relocation. A similar problem occurs when referring to a value type field on a movable type:

```
int\* a = &“message”.Length;
```

Either way, to assign an address of some data requires the following:

+   • The data must be classified as a variable. • The data must be an unmanaged type. • The variable needs to be classified as fixed, not movable.

If the data is an unmanaged variable type but is not fixed, use the fixed statement to fix a movable variable.

# **Fixing Data**

To retrieve the address of a movable data item, it is necessary to fix, or pin, the data, as demonstrated in Listing 21.14.

# **LISTING 21.14: Fixed Statement**

```
byte[] bytes = new byte[24];
fixed (byte* pData = &bytes[0])  // pData = bytes also allowed
{
    // ….
}
```

Within the code block of a fixed statement, the assigned data will not move. In this example, bytes will remain at the same address, at least until the end of the fixed statement.

The fixed statement requires the declaration of the pointer variable within its scope. This avoids accessing the variable outside the fixed statement, when the data is no longer fixed. However, it is your responsibility as a programmer to ensure that you do not assign the pointer to another variable that survives beyond the scope of the fixed statement—possibly in an API call, for example. Unsafe code is called “unsafe” for a reason; you are required to ensure that you use the pointers safely rather than relying