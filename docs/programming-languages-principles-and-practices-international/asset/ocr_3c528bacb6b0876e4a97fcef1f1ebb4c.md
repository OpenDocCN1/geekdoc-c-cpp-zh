The two iterators select: and inject:into: can be used to generate the sum of the odd numbers in a collection named col, as follows:

```
(col select: [ :n | n odd])
    inject: 0 into: [ :n1 :n2 |
        n1 + n2]
"Returns the sum of the odd numbers in col"
```

The implementations of Smalltalk iterators rely on the methods do: and add:, both of which are implemented by subclasses of Collection. Here is the code for one of the iterators, collect:, which is the polymorphic equivalent of a map in functional languages:

```
collect: aBlock
    "For each element in the receiver, evaluate aBlock with
     that element as the argument. Answer a new collection
     containing the results as its elements from the aBlock
     evaluations."
    | answer |
    answer := self species new.
    self do: [ :element |
        answer add: (aBlock value: element)].
    ^answer
```

Note that this code creates a new instance of the same class as the receiver object. To this new collection object are added the results of evaluating a block with each element of the receiver collection. The new collection is then returned. A similar do: loop pattern is used in the implementations of the other iterators.

Another interesting set of methods in the Collection class allows the programmer to convert any type of collection, including newly added ones, to many of the built-in types of collections. Most of these methods, such as asBag and asSet, create an instance of the specified type of collection and send it the addAll: message with the receiver object as an argument. The addAll: method, which is also included in the Collection class, runs a do: loop on its parameter object to add each of its elements to the receiver with the receiver's add: method. The add: method is, naturally, implemented by a subclass. Here is the code for the Collection methods asBag and addAll:.

```
asBag
    "Answer a Bag containing the elements of the receiver."
    ^(Bag new)
        addAll: self;
        yourself

addAll: aCollection
    "Answer aCollection. Add each element of
     aCollection to the elements of the receiver."
    aCollection do: [ :element | self add: element].
    ^aCollection
```