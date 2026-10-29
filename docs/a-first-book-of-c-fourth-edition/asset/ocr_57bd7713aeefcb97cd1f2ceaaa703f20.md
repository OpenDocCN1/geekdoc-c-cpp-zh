# Point of Information

# Dr. Lukasiewicz and RPN

Dr. Jan Lukasiewicz, born in 1878, studied and taught mathematics at the University of Lvov in Poland before becoming a respected professor at the University of Warsaw. He was appointed to the post of Minister of Education in Poland in 1919 and, with Stanislaw Lesniewski, founded the Warsaw School of Logic. After World War II, Dr. Lukasiewicz and his wife, Regina, were exiled in Belgium. When he was offered a professorship at the Royal Academy in Dublin, they moved to Ireland, where they remained until his death in 1956.

In 1951, Dr. Lukasiewicz developed a new set of postfix algebraic notation, which was critical in the design of early microprocessors in the 1960s and 1970s. The actual implementation of postfix algebra was done by using stack arithmetic, in which data was pushed on a stack and popped off when an operation needed to be performed. These stack-handling instructions required no address operands and made it possible for very small computers to handle large tasks effectively.

Stack arithmetic, which is based on Dr. Lukasiewicz's work, reverses the more commonly known prefix algebra and became known as Reverse Polish Notation (RPN). Early pocket calculators developed by Hewlett-Packard Corporation were especially notable for their use of RPN and made stack arithmetic the favorite of many scientists and engineers.

Although Figure 13.7 is an accurate representation of a list of names, it contains additional information that a true stack object doesn't provide. When names are added to or removed from a stack, no count is kept of how many names have been added or deleted or of how many items the stack contains at any time. For example, by examining each part of Figure 13.7, you can determine how many names are on the list. In a true stack, the only item that can be seen and accessed is the top one on the list. Finding out how many items the list contains would require removing the top item continually until no more items exist.

# Stack Implementation with the deque Class

Creating a stack requires the following four components:

+   - A container for holding items in the list
+   - A method of designating the current top stack item
+   - An operation for placing a new item on the stack
+   - An operation for removing an item from the stack

By convention, the operation of placing a new item on the top of a stack is called a push, and the operation of removing an item from a stack is called a pop. How these operations are implemented depends on the container type used to represent a stack. In C++, a stack can be created easily with STL's deque class. This class creates a double-ended list, where objects can be pushed and popped from either end. To create a stack, only the front end of the deque is used. Table 13.4 summarizes the deque class's methods and operations.