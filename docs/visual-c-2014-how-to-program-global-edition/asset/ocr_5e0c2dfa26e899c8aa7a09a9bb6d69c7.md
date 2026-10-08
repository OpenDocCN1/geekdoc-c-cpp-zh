# 19.5 Stacks 831

hello popped
The stack is: 34567 $ True

34567 popped
The stack is: $ True

$ popped
The stack is: $ True

True popped
Empty stack
at LinkedList.List.RemoveFrom() in C:\Users\PaulDeitel\nDocuments\examples\ch19\Fig19_04\LinkedList\nLinkedList\LinkedList.cs: line 81
at StackInheritanceLibrary.StackInheritance.Pop() in C:\Users\PaulDeitel\nDocuments\examples\ch19\Fig19_13\StackInheritance\nStackInheritanceLibrary.StackInheritance.cs: line 24
at StackInheritanceTest.Stack() in C:\Users\PaulDeitel\nDocuments\examples\ch19\Fig19_14\StackInheritance\nStackInheritanceTest.StackInheritanceTest.cs: line 35

Fig. 19.14 | Testing class That Contains a Reference to a List (Part 2 of 2)

Stack Class That Contains a Reference to a List
Another way to implement a stack is by reusing a list through composition. ClassComposition (Fig.15) uses a private object of class list (line 10). Composition enables us to hide the methods of class list that should not be in our public interface by providing public interface methods only to the required list methods. Each class implements stack method by delegating its work to an appropriate list method. StackComposition's methods call list methods AtFront, RemoveFrom, IsEmpty and Display. In this example, we do not show StackComposition, because the only differences in this example are that we change the name of the stack class from StackInheritance to StackComposition and update a using directive.

```
// Fig.19.15: StackComposition.class.cs
// StackComposition encapsulates functionality of class list.
using LinkedListList;

namespace StackCompositionLibrary
{
    // StackComposition encapsulates List's capabilities
    public class StackComposition
    {
        private List stack;

        public StackComposition()
        {
            stack = new List("stack");
```

Fig. 19.15 | StackComposition class encapsulates functionality of class list. (Part I of 2)