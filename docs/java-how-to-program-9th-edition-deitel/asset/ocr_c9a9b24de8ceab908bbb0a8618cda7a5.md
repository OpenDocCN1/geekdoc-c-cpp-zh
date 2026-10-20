```
The stack is: -1
The stack is: 0 -1

The stack is: 1 0 -1
The stack is: 5 1 0 -1

5 popped
The stack is: 1 0 -1

1 popped
The stack is: 0 -1

0 popped
The stack is: -1

-1 popped
Empty stack
com.deitel.ch22.EmptyListException: stack is empty
  at com.deitel.ch22.List.removeFromFront(List.java:81)
  at com.deitel.ch22.StackInheritance.pop(StackInheritance.java:22)
  at StackInheritanceTest.main(StackInheritanceTest.java:30)
```

Fig. 22.11 | Stack manipulation program. (Part 2 of 2.)

# Stack Class That Contains a Reference to a List

You can also implement a class by reusing a list class through composition. Figure 22.12 uses a private List<T> (line 7) in class StackComposition<T>’s declaration. Composition enables us to hide the List<T> methods that should not be in our stack’s public interface. We provide public interface methods that use only the required List<T> methods. Implementing each stack method as a call to a List<T> method is called delegation—the stack method invoked delegates the call to the appropriate List<T> method. In particular, StackComposition<T> delegates calls to List<T> methods insertAtFront, removeFromFront, isEmpty and print. In this example, we do not show class StackCompositionTest, because the only difference is that we change the type of the stack from StackInheritance to StackComposition (lines 3 and 10–11 of Fig. 22.11).

```
1  // Fig. 22.12: StackComposition.java
2  // StackComposition uses a composed List object.
3  package com.deitel.ch22;
4
5  public class StackComposition< T >
6  {
7      private List< T > stackList;
8
9      // no-argument constructor
10     public StackComposition()
11     {
12         stackList = new List< T >( "stack" );
13     } // end StackComposition no-argument constructor
14
```

Fig. 22.12 | StackComposition uses a composed List object. (Part 1 of 2.)