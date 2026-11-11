which hides it from all other classes. Its members are public, however, so they are visible to the nesting class, single_linked_list. If they were private, node would need to declare the nesting class to be a friend to make them visible in the nesting class. Note that nested classes have no special access to members of the nesting class. Only static data members of the nesting class are visible to methods of the nested class.^10

The enclosing class, single_linked_list, has just a single data member, a pointer to act as the list's header. It contains a constructor function, which sets head to the null pointer value. The four member functions allow nodes to be inserted at either end of a list object, nodes to be removed from one end of a list, and lists to be tested for empty.

The following definitions provide stack and queue classes, both based on the single_linked_list class:

```
```cpp
class stack : public single_linked_list {
  public:
    stack() {}
    void push(int value) {
        insert_at_head(value);
    }
    int pop() {
        return remove_at_head();
    }
};
class queue : public single_linked_list {
  public:
    queue() {}
    void enqueue(int value) {
        insert_at_tail(value);
    }
    int dequeue() {
        return remove_at_head();
    }
};
```
```

Note that objects of both the stack and queue subclasses can access the empty function defined in the base class, single_linked_list (because it is a public derivation). Both subclasses define constructor functions that do nothing. When an object of a subclass is created, the proper constructor in the subclass is implicitly called. Then, any applicable constructor in the base class is called. So, in our example, when an object of type stack is created, the constructor in single_linked_list is called, which does the necessary initialization. Then the stack constructor is called, which does nothing.

The classes stack and queue both suffer from the same serious problem: Clients of both can access all of the public members of the parent class,

10. A class can also be defined in a method of a nesting class. The scope rules of such classes are the same as those for classes nested directly in other classes, even for local variables declared in the method in which they are defined.