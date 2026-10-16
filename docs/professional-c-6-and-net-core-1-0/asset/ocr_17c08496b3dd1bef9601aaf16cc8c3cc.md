+   - Prefix generic type names with the letter T.
+   - If the generic type can be replaced by any class because there’s no special requirement, and only one generic type is used, the character T is good as a generic type name:
+     ```
+     public class List<T> { }
+     public class LinkedList<T> { }
+     ```
+   - If there’s a special requirement for a generic type (for example, it must implement an interface or derive from a base class), or if two or more generic types are used, use descriptive names for the type names:
+     ```
+     public delegate void EventHandler<TEventArgs>(object sender, TEventArgs e);
+     public delegate TOutput Converter<TInput, TOutput>(TInput from);
+     public class SortedList<TKey, TValue> { }
+     ```

# Creating Generic Classes

The example in this section starts with a normal, non-generic simplified linked list class that can contain objects of any kind, and then converts this class to a generic class.

With a linked list, one element references the next one. Therefore, you must create a class that wraps the object inside the linked list and references the next object. The class LinkedListNode contains a property named Value that is initialized with the constructor. In addition to that, the LinkedListNode class contains references to the next and previous elements in the list that can be accessed from properties (code file LinkedListObjects/LinkedListNode.cs):

```
public class LinkedListNode
{
    public LinkedListNode(object value)
    {
        Value = value;
    }

    public object Value { get; private set; }

    public LinkedListNode Next { get; internal set; }
    public LinkedListNode Prev { get; internal set; }
}
```

The LinkedList class includes First and Last properties of type LinkedListNode that mark the beginning and end of the list. The method AddLast adds a new element to the end of the list. First, an object of type LinkedListNode is created. If the list is empty, then the First and Last properties are set to the new element; otherwise, the new element is added as the last element to the list. By implementing