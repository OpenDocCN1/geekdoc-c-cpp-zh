# CHAPTER 1 Data Abstraction: The Walls

```
/**
 * Tests whether this bag contains a given entry.
 * @param anEntry The entry to locate.
 * @return True if bag contains anEntry, or false otherwise. */
virtual bool contains(const Item& anEntry) const = 0;

/**
 * Empties and fills a given vector with all entries that
 * are in this bag.
 * @return A vector containing all the entries in the bag. */
virtual vector<Item> toVector() const = 0;
};\ // BagInterface
```

The specifications of these operations are the sole terms of the contract for the ADT. If you request that these operations are performed, this is what will happen. The specifications contain no mention of how to store the bag or how to perform the operations; they tell you only what to do with the bag. It is of fundamental importance that the specification of an ADT does not limit implementation issues. This restriction on the specification of an ADT allows you to build a wall between an implementation of an ADT and the program that uses it—that is, it, the client. The behavior of the operations is the only thing on which a program should depend.

> Note: Although writing an interface is certainly not required, doing enables you to document your specifications in a concise way. Then you can use the code in the interface as an outline for the actual class. Having an interface also provides a data type for an ADT that is independent of a particular class definition. Chapters 3 and 4 will develop different implementations of a class of bags. Code written with respect to an interface allows you to more easily replace one implementation of a bag with another.

# 1.5.4 Using the ADT Bag

Imagine we have a programmer to implement the ADT bag in C++, given the interface and specifications that we have developed so far. If we assume that these specifications are enough for the programmer to complete the implementation, we can use the bag's operations in a program without knowing the details of the implementation. We do not need to know how the programmer implemented the bag to be able to use it. We need to know only what the ADT bag does.

The following example demonstrates how we can use a bag and assumes that we are using a C++ class bag, that implements the C++ abstract class BagInterface given in Listing 1.

Example. Suppose you invite three friends to your home to watch your favorite soccer team on election. To make the breaks more interesting, you make up the following game. From a deck of cards, you remove the entire suit of clubs: Ace, Two, Three... Jack, Queen, and King of clubs. You randomly select six of these cards and place them into a bag. Your friends guess which cards are in the bag. Each time they correctly guess a card, it is removed from the bag.