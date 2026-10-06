# Selecting an Implementation

you really need the application at hand. It is tempting to want all possible operations, but this strategy is a poor one, because often one implementation supports some of the operations more efficiently than another implementation. Therefore, if you include an operation that you do not need, you might end up with an implementation of the ADT that does not suit your purpose.

In addition to knowing what operations are needed for a given application, the ADT implementer should know how often the application will perform each operation. Although some applications may require many of every operation, other applications may not. For example, if you invented a dictionary of cities—such as those in Figure 18–1—you would expect to perform many retrieval operations than additions or removals. If you seldom add items to a dictionary, you could insert an implementation that results in an inefficient add operation, as frequently used operations are efficient. Course, as Chapter 10 mentioned, if an ADT operation is to be used in a life-or-death situation, operation must be efficient if you rarely need it. The necessary operations, their expected frequency of occurrence, and their required response times are some factors that influence implementation of an ADT you select for a particular application. You should, however, remain conscious of factors other than efficiency, as discussed in Chapter 10.

What operations are needed?

How often is each operation required?

# 18.3 Three Scenarios

Consider now several application scenarios, each of which requires a particular mix of the dictionary operations. The analysis of various implementations of the ADT will illustrate some of the basic concerns of algorithms. You will see, given an application, how to select an implementation that supports in a reasonably efficient manner the required mix of dictionary operations.

Scenario A: Insertion and traversal in no particular order. Mary’s sorry plans to raise money for a local charity. Tired of previous fund-raisers, Mary suggests a brainstorming session to cover a new money-making strategy. As members voice their ideas, Mary records them by adding each new word to the dictionary. Later, she will insert each of the ideas in the dictionary. Also assume that the organization of the order is relevant—the items can be sorted or unordered. Also assume that operations such as retrieval, removal, or traversal in the linked array do not occur or so infrequently that they do not influence your choice of an implementation.

An unordered order is efficient

For this application, maintaining the items in a sorted order has no advantage. In fact, by not maintaining a sorted order, the add operation can be efficient. For unordered linear implementation, you can easily insert a new item in any convenient location. For an unordered array-based implementation, you can easily insert the new item at the itemCount. Figure 18–6 shows the result of this insertion after each itemCount has been updated. For a linked-based implementation, you can simply insert a new item at the beginning of the linked chain. As Figure 18–6 illustrates, the head pointer points to the new item, and the new item points to the item that was first in the chain. Thus, you can insert a new item quickly into either unordered implementation of a dictionary; in fact, the add operation is O(1). It requires a constant time for either implementation regardless of the size.

Array-based versus pointer-based

Should you choose the array-based or the linked-based implementation? As you see with other ADTs, an implementation that dynamically uses allocated memory is appropriate if you do not have a good estimate of the maximum possible size of the dictionary. By brainstorming session likely falls into this category. On the other hand, if you know that the dictionary’s maximum size is not drastically larger than its expected size, the choice is mostly a matter of style. An array-based

Section 4.5 of Chapter 4 discussed the expected and maximum number of items in an ADT affect array-based implementation.