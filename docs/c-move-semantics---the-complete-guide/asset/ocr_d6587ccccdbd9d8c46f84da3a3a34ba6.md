# Dealing with Move Assignments of Objects to Themselves

You might wonder whether you should check for assignments of an object to itself when implementing the move assignment operator. For example, a self move might happen as follows:

```
Customer c{"GNU's Not Unix"};
 c = std::move(c);                     // move assigns c to itself
```

This looks easy to avoid but we might use references and pointers, and in that case, it is not necessarily that obvious that two objects are the same. Consider the following code as a still quite simple example:

```
std::vector<Customer> coll;
 coll.emplace_back("GNU's Not Unix");   // coll has 1 element
 coll[0] = std::move(coll.back());       // move assigns the only element to itself
```

As written, all types in the C++ standard library receive a valid but unspecified state when objects are moved to themselves. This means that by default, you might lose the values of your members and you might even have a more severe problem if your type does not work properly with members that have arbitrary values. In fact, the resulting state might be a problem in the following situations:

+   - Some values of a moved-from member are a problem
+   - The values of members depend on each other

The traditional/naive way to protect against self-assignments is to check whether both operands are identical (have the same address). You can also do this when implementing the move assignment operator:

```
Customer& operator= (Customer&& cust) {  // noexcept declaration missing
    std::cout << "MOVEASSIGN " << cust.name << '\n';
    if (this != &cust) {                  // move assignment to myself?
        name = std::move(cust.name);
        values = std::move(cust.values);
    }
    return *this;
}
```

Having a check like this is pretty cheap and would have the benefit that the object keeps its value on a self-move-assignment. However, note that in recursive data structures, it can also be a problem if you (move) assign a child object to a parent object. If we delete the old value of the parent (which owns the child) first before we assign the new value, you might then assign a deleted object. In this case, the objects are not identical, which means that comparing their addresses does not help.

In addition, consider the following from style guides:

+   - In his book Effective C++ Scott Meyers says that self-assignments are usually not a problem when resource management is encapsulated properly by helper classes (but we did not have move semantics at that time). Furthermore, he points out that otherwise, you also have to ensure that the operator is exception-safe.
+   - The C++ Core Guidelines categorize this problem as a “one-in-a-million problem” that does not appear to be relevant in practice.²

It seems that in most cases, you can ignore self-move-assignments, which usually means that in your types, you give the same guarantee as the C++ standard library: after move assigning an object to itself, the object is in a valid but unspecified state.

2 See http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rc-move-self.