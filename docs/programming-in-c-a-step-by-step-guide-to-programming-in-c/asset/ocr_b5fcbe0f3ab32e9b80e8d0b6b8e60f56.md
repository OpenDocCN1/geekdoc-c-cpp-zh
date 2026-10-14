Some programming languages provide explicit mechanisms to support the distinction between specification and implementation. Although C does not have an explicit mechanism for implementing ADTs, it is still possible and desirable to design your data types using the same notion.

How does the specification of the operations of an ADT differ from the implementation of the operations? The specification consists of the names of every function, the type of its arguments, and the type of its result. There should also be a description of what the function does, but without appealing to internal representation or implementation details. This requirement is quite important, and it implies that an abstract data type is implementation independent. Furthermore, it is possible to classify the functions of a data type into several categories:

+   1) **Creator/constructor:** These functions create a new instance of the designated type.
+   2) **Transformers:** These functions also create an instance of the designated type, generally by using one or more other instances.
+   3) **Observers/reporters:** These functions provide information about an instance of the type, but they do not change the instance.

Typically, an ADT definition will include at least one function from each of these three categories.

# 14.4 Stack as an Abstract Data Type

A stack is simply a list of elements with insertions and deletions permitted at one end – called the stack top. That means that it is possible to remove elements from a stack in reverse order from the insertion of elements into the stack. Thus, a stack data structure exhibits the LIFO (last in first out) property. Push and pop are the operations that are provided for insertion of an element into the stack and the removal of an element from the stack, respectively. Shown in Figure 14.1 are the effects of push and pop operations on the stack.