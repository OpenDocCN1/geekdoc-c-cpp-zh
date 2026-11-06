```
```cpp
lastPtr = currentPtr; // remove last node
currentPtr->nextPtr = nullptr; // this is now the last node
}

value = tempPtr->data; // return value from old last node
delete tempPtr; // reclaim former last node
return true; // delete successful
}
}

// is List empty?
bool isEmpty() const {
    return firstPtr == nullptr;
}

// display contents of List
void print() const {
    if (isEmpty()) { // List is empty
        std::cout << "The list is empty\n\n";
        return;
    }

    ListNode<NODETYPE>* currentPtr{firstPtr};

    std::cout << "The list is: ";

    while (currentPtr != nullptr) { // get element data
        std::cout << currentPtr->data << ' ';
        currentPtr = currentPtr->nextPtr;
    }

    std::cout << "\n\n";
}

private:
    ListNode<NODETYPE>* firstPtr{nullptr}; // pointer to first node
    ListNode<NODETYPE>* lastPtr{nullptr}; // pointer to last node

    // utility function to allocate new node
    ListNode<NODETYPE>* getNewNode(const NODETYPE& value) {
        return new ListNode<NODETYPE>{value};
    }
};

#endif
```
```

Fig. 19.5 *List* class-template definition.