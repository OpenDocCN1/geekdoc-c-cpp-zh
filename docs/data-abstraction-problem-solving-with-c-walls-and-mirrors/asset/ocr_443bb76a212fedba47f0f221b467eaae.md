# 4.5 Comparing Array-Based and Link-Based Implementations

Typically, the various implementations that a programmer contemplates for a particular ADT have advantages and disadvantages. When you select an implementation, you should weigh these advantages and disadvantages before you make your choice. As you will see, the decision among implementations of an ADT is one you must often make. As an example of how you should proceed in general, we compare the two implementations of the ADT that you have seen.

The array-implementation that you saw in Chapter 3 appears to be a reasonable approach. Arrays are easy to use, but as already mentioned, an array has a fixed size, and it is possible for the number of items in the bag to exceed this fixed size. In practice, when choosing implementations of an ADT, you must ask the question whether the fixed-size restriction of an array-based implementation presents a problem in the context of a particular application. The answer depends on two factors. One obvious factor is, for a given application, you can increase the maximum number of items in the ADT at any time. If you cannot, it is possible that your approach—and hence your engine—fails because the ADT in the context of a particular application requires more than the array can provide.

On the other hand, if for your given application you can increase the maximum number of items in the ADT at any time, then you have a more flexible structure. Would you waste storage by declaring an array to be enough to accommodate your maximum number of items? Consider a case in which the maximum number of items is large, but you suspect that this will rarely be reached. For example, suppose that your bag could contain 50 items. If you allocate 100 locations, at least 50 will be wasted for most of the time. In both of the two cases, the array-based implementation in Chapter 3 is not needed.

What if you use a dynamically allocated array? Because you use the new operator to allocate storage dynamically, you would be able to provide as much storage as the bag needs (within the bounds of the particular computer), or double the size of the array each you reach the end of the array—which is a reasonable approach to enlarging the array—you might still have many unused locations. In the given example, you could allocate an array of 50 locations. If you add 10,000 items to your bag, doubling it will eventually give you an array of 12,000 locations, which is 2,800 more than you need. Remember that you waste time by copying the array and deallocating each time you need more space.

Now suppose that your bag will contain more than 25 items. You could allocate enough storage in the array for the bag so that you would waste little storage when the bag contains only a few items relative to its size, an array-based implementation is perfectly acceptable in this case.

A link-based implementation can avoid any difficulties related to the fixed-size of an array-based implementation. You use the new operator to allocate storage dynamically, so you do not need to predict the maximum size of the bag. Because you allocate one item at a time, the bag will be allocated as much as it needs. You will not waste space.

Array-based and link-based implementations have other differences, and these differences affect both the time and memory of implementations. When you use a collection of data in an array or a linked chain, the data items are ordered; that is, there is a first, a second, and so on. In an array, the location of the next item after the item in `array[i]` is implicit—it is in `array[i+1]`. In a linked chain, however, you explicitly define the location of the next item by using the pointer in the current node. This notion of an implicit versus explicit next next item is one of the primary differences between an array and a linked chain. Therefore, an advantage of an array-based implementation

![](bbox=[0.788, 0.22, 0.933, 0.265])

![](bbox=[0.788, 0.297, 0.933, 0.342])

![](bbox=[0.788, 0.374, 0.933, 0.419])

![](bbox=[0.788, 0.524, 0.933, 0.569])

![](bbox=[0.788, 0.582, 0.933, 0.627])

![](bbox=[0.788, 0.659, 0.933, 0.704])

![](bbox=[0.788, 0.788, 0.933, 0.873])