```
```cpp
nodeType<Type> *first; //pointer to the first node of the list
nodeType<Type> *last;  //pointer to the last node of the list

private:
    void copyList(const LinkedListType<Type>& otherList);
    //Function to make a copy of otherList.
    //Postcondition: A copy of otherList is created and
    //              assigned to this list.
};
```
```

Figure 17-20 shows the UML class diagram of the class `linkedListType`.

![](bbox=[0.204, 0.286, 0.889, 0.735])

**FIGURE 17-20**  UML class diagram of the class `linkedListType`

Note that typically, in the UML diagram, the name of an abstract class and abstract function is shown in italics.

The instance variables `first` and `last`, as defined earlier, of the class `linkedListType` are protected, not private, because as noted previously, we will derive the classes `unorderedLinkedList` and `orderedLinkedList` from the class `linkedListType`. Because each of the classes `unorderedLinkedList`