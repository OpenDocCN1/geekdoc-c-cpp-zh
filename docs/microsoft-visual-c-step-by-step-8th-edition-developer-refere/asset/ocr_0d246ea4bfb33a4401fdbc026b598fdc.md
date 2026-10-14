# Initializing a variable defined with a type parameter

You should have noticed that the statement that defines and initializes the currentItem variable uses the default keyword. The currentItem variable is defined by using the type parameter TItem. When the program is written and compiled, the actual type that will be substituted for TItem might not be known—this issue is resolved only when the code is executed. This makes it difficult to specify how the variable should be initialized. The temptation is to set it to null. However, if the type substituted for TItem is a value type, this is an illegal assignment. (You cannot set value types to null, only reference types.) Similarly, if you set it to 0 with the expectation that the type will be numeric, this will be illegal if the type used is actually a reference type. There are other possibilities as well—TItem could be a boolean, for example. The default keyword solves this problem. The value used to initialize the variable will be determined when the statement is executed. If TItem is a reference type, default(TItem) returns null; if TItem is numeric, default(TItem) returns 0; if TItem is a boolean, default(TItem) returns false. If TItem is a struct, the individual fields in the struct are initialized in the same way. (Reference fields are set to null, numeric fields are set to 0, and boolean fields are set to false.)

# Implementing the IEnumerable interface

In the following exercise, you will modify the binary tree class to implement the IEnumerable<T> interface. The GetEnumerator method will return a TreeEnumerator<TItem> object.

# Implement the IEnumerable<TItem> interface in the Tree<TItem> class

+   1. In Solution Explorer, double-click the file Tree.cs to display the Tree<TItem> class in the Code and Text Editor window.

+   2. Modify the definition of the Tree<TItem> class so that it implements the IEnumerable<TItem> interface, as shown in bold in the following code:

Click here to view code image

```
public class Tree<TItem> : IEnumerable<TItem> where TItem :
IComparable<TItem>
```

Notice that constraints are always placed at the end of the class definition.

+   3. Hover over the IEnumerable<TItem> interface in the class definition. On the drop-down context menu that appears, click Implement Interface Explicitly.

This action generates implementations of the IEnumerable<TItem>.GetEnumerator and IEnumerable.GetEnumerator