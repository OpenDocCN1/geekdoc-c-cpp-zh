# Chapter 25

# Linked Lists

+   25.1 The List/Seq ADT ........................................................ 657
+   25.2 Nature of Arrays ............................................................. 658
+   25.3 Nature of Linked Lists ....................................................... 658
+   25.4 Mutable Singly-Linked List .................................................. 660
+       25.4.1 Implementing mutable.Buffer ........................................ 663
+       25.4.2 Iterators ................................................................. 666
+   25.5 Mutable Doubly-Linked List .................................................. 668
+   25.6 Immutable Singly-Linked List ................................................ 671
+   25.7 Linked List-Based Stacks and Queues ....................................... 674
+       25.7.1 Linked List-Based Stack ............................................... 674
+       25.7.2 Linked List-Based Queue ............................................... 675
+   25.8 End of Chapter Material ....................................................... 676
+       25.8.1 Summary of Concepts .................................................... 676
+       25.8.2 Exercises ................................................................... 676
+       25.8.3 Projects ..................................................................... 677

So far in this book we have been very happy to use the collections libraries without having a full understanding of how they work. That is fine for much of what we have done and in a first year of Computer Science (CS) study, but real developers need to have knowledge of what is really happening so that they can make informed opinions about what collection types to use in different situations. This chapter will begin to reveal how we can build our own structures for storing data by linking objects that store small pieces of data together.

# 25.1  The List/Seq ADT

The topic of this chapter is the linked list. This is an approach to storing data in a way that can be applied to some different Abstract Data Types (ADTs). Later in the chapter we will see how a linked list can be used as the storage for stacks and queues. Before that, we want to introduce a new ADT that is a step up on the ladder of capabilities, the list ADT. This ADT provides the ability to store a sequence of data elements that are indexed by integers with functionality for random retrieval, insertion, and removal. In a language-independent way one might expect these to be implemented in methods like these.

```
def get(index:Int) : A
def set(index:Int, data:A)
def insert(index:Int, data:A)
def remove(index:Int) : A
```