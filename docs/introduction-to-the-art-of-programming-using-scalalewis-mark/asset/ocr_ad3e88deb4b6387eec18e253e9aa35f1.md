# Chapter 26

# Priority Queues

+   26.1 Two Approaches ......................................................... 679
+   26.1.1 Searching by Priority ................................................... 680
+   26.1.2 Sorted Linked List ...................................................... 680
+   26.1.3 Problems with Arrays .................................................... 682
+   26.2 Project Integration: Discrete Event Simulation ................................ 683
+   26.2.1 Cell Splitting ........................................................... 683
+   26.2.2 Collision Handling ...................................................... 686
+   26.3 End of Chapter Material .................................................... 693
+   26.3.1 Summary of Concepts ..................................................... 693
+   26.3.2 Exercises ................................................................ 694
+   26.3.3 Projects ................................................................. 694

The queue Abstract Data Type (ADT) that we have looked at previously can be thought of as modeling a service line. All the entities that are added in are considered equal, and they are taken off in the order they arrive. Not every system works in such an equitable way. In real life there are things like VIP lines. Some systems have a serious reason to treat entities differently. An example of such a system is an emergency room. If you show up to an ER with a paper cut, you can expect to wait for a very long time. This is because the order in which people are served in an ER is based much more on the seriousness of the person’s condition than on the time of arrival. Situations where people set up appointments are another example. Arriving long before your appointment time generally does not lead to you being seen significantly earlier.

These types of systems call for a new ADT, the priority queue. A priority queue has the same methods as a normal queue, but there is a different behavior for the dequeue and peek methods in that they give the highest priority object on the queue and only consider length of time in the queue if the highest priority items have equal priority.

# 26.1 Two Approaches

We will consider two different approaches to writing a priority queue in this chapter, both use a linked list for storage. The difference between the two is whether extra work is done when new items are added to the queue or if that work is put off until the items are removed. We will discuss both and compare their efficiency, but only code the one that is better. Unlike the normal queue, it is not possible to get O(1) performance for all the methods in a priority queue. For the implementations we will talk about here, some methods will be O(n). We will discuss another implementation that can improve on that in chapter 32.

All implementations of the priority queue will extend the following trait.