the node’s value available via the Value property) and appends this node to the end of the list. There’s also an AddFirst method that inserts a node at the beginning of the list.

Line 25 invokes the constructor that takes an IEnumerable<T> parameter. All arrays implement the generic interfaces IList<T> and IEnumerable<T> with the array’s element type as the type argument, so a string array implements IEnumerable<string>. Thus, colors2 is an IEnumerable<string> and can be passed to the List<string> constructor to initialize the List. This constructor copies array colors2’s contents into list2.

# *Methods That Test Class LinkedList*

Line 27 calls *generic method* Concatenate (lines 55–64) to append all elements of list2 to the end of list1. Line 28 calls method PrintList (lines 42–52) to output list1’s contents. Line 31 calls method ToUppercaseStrings (lines 67–78) to convert each string element to uppercase, then line 32 calls PrintList again to display the modified strings. Line 35 calls method RemoveItemsBetween (lines 81–94) to remove the elements between “BLACK” and “BROWN”—not including either. Line 37 outputs the list again, then line 38 invokes method PrintReversedList (lines 97–111) to display the list in *reverse* order.

# *Generic Method Concatenate*

Generic method Concatenate (lines 55–64) iterates over its second parameter (list2) with a foreach statement and calls method AddLast to append each value to the end of its first parameter (list1). The LinkedList class’s enumerator loops over the values of the nodes, not the nodes themselves, so the iteration variable is inferred to be of the LinkedList’s element type T. Notice that this creates a new node in list1 for each node in list2. One LinkedListNode cannot be a member of more than one LinkedList. If you want the same data to belong to more than one LinkedList, you must make a copy of the node for each list to avoid InvalidOperationExceptions.

# *Generic Method PrintList and Method ToUppercaseStrings*

Generic method PrintList (lines 42–52) similarly uses a foreach statement to iterate over the values in a LinkedList, and outputs them. Method ToUppercaseStrings (lines 67–78) takes a linked list of strings and converts each string value to uppercase. This method replaces the strings stored in the list, so we cannot use a foreach statement as in the previous two methods. Instead, we obtain the first LinkedListNode via the First property (line 70) and use a sentinel-controlled while statement to loop through the list (lines 72–77). Each iteration of the while statement obtains and updates the contents of currentnode via property Value (line 74), using string method ToUpper to create an uppercase version of the string (line 75). Then line 76 moves to the next node in the list by assigning to currentnode the value of currentnode.Next, which refers to the LinkedList’s next node. The Next property of the LinkedList’s last node is null, so when the while statement iterates past the end of the list, the loop exits.

# *Method ToUppercaseStrings is not a Generic Method*

It does not make sense to declare ToUppercaseStrings as a generic method, because it uses the string-specific values of the values in the nodes.

> **Software Engineering Observation 19.1**
> *For maximal code reuse, define methods with generic type parameters whenever possible.*