```
// Fig. 19.13: StackInheritanceLibrary.cs
// Implementing a stack by inheriting from class List.
using LinkedList;

namespace StackInheritanceLibrary
{
    // Class StackInheritance inherits class List's capabilities
    public class StackInheritance : List
    {
        // pass name "stack" to List constructor
        public StackInheritance() : base("stack") { }

        // dataValue at top of stack by inserting
        // dataValue at front of linked list
        public void Push(object dataValue)
        {
            InsertFront(dataValue);
        }

        // remove item from top of stack by removing
        // item at front of linked list
        public object Pop()
        {
            return RemoveFromFront();
        }
    }
}
```

Fig. 19.13 | implementing a stack by inheriting from class List.

The implementation of each StackInheritance method calls the appropriate List method—method Push calls InsertFront, method calls RemoveFromFront. Class StackInheritance does not define methods IsEmpty and Display, because StackInheritance inherits its methods from class List into StackInheritance's public interface. Class StackInheritance uses namespace LinkedList (Fig. 19.4); thus, the class library that defines StackInheritance must have a reference to the LinkedList class library.

StackInheritanceTest's Main method (Fig. 19.4) uses class StackInheritance to create objects of objects called stack (line 12). Lines 15–18 define four values that are pushed onto the stack and popped off. The program pushes the stack (lines 21, 23 and 25) and a boolean true, a char containing '$', an int containing 34567 and a string containing "Hello!". An infinite while loop (lines 33–38) pops the elements from the stack. When the stack is empty, method Pop throws an EmptyListException, and the program displays the exception. The program uses method Display (inherited by StackInheritance from class List) to output the contents of the stack after each operation. Class StackInheritanceTest uses namespace LinkedList (Fig. 19.4) and namespace StackInheritanceLibrary (Fig. 19.13); thus, the solution for class StackInheritanceTest must have references to both class libraries.