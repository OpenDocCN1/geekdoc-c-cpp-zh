Smalltalk has no built-in classes for stacks, queues, trees, or graphs, but we can easily see how to add them. Let’s develop this idea for queues. There are two common implementations of queues, one based on an array and the other based on linked nodes. An array-based queue class could be a subclass of the Array class or the OrderedCollection class (which is like the array-based ArrayList class in Java). However, subclassing one of these classes for queues would be a poor design choice, because users of such queues would then have at their disposal operations, such as at:put:, which would violate the spirit of restricting access to the front or rear of a queue collection. A better choice would be to subclass the Collection class, whose operations, such as the iterators and the type conversion methods, provide some positive benefits without the negative consequences. The ArrayQueue methods would include not just the standard ones such as enqueue, dequeue, size, and isEmpty but also do: and add:, which are needed to invest queues with the functionality of many of the Collection methods. As for properties, the ArrayQueue class would contain either an array or an ordered collection to hold its data elements. The completion of this version of a queue in Smalltalk is left as an exercise.

The other major implementation, LinkedQueue, is also a subclass of Collection. It has the same interface, or set of methods, as ArrayQueue. However, the elements in a LinkedQueue are contained in a sequence of linked nodes. Linked nodes come in many flavors, among them singly linked, doubly linked, and variations on each of these with a circular link back to the first node or a special header node. To support any of these options, we need a separate class that contains a data element and one or more links. For a simple singly linked structure, the Association class in Smalltalk’s magnitude hierarchy already fills the bill.

Two instance variables that point to the first and last nodes in the linked structure enable the implementation to quickly locate the front and rear elements in the queue, respectively. The size of the queue is also tracked with a separate instance variable. Following is a listing of the properties and methods of a LinkedQueue class in Smalltalk:

```
Collection subclass: #LinkedQueue
    instanceVariableNames:
        'front rear size '
    classVariableNames: ''
    poolDictionaries: ''

new
    "Answer an instance of the receiver, with front and
     rear pointers as empty links and size of 0."
    ^super new initialize

initialize
    "Answer this object. Set the instance variables to initial values."
    | newNode |
    front := nil.
    rear := nil.
    size := 0.
    ^self
```

(continues)