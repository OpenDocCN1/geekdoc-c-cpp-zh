The collection array is instantiated in the DVDCollection constructor. Every time a DVD is added to the collection (using the addDVD method), a new DVD object is created and a reference to it is stored in the collection array.

Each time a DVD is added to the collection, we check to see whether we have reached the current capacity of the collection array. If we didn’t perform this check, an exception would eventually be thrown when we try to store a new DVD object at an invalid index. If the current capacity has been reached, the private increaseSize method is invoked, which first creates an array that is twice as big as the current collection array. Each DVD in the existing collection is then copied into the new array. Finally, the collection reference is set to the larger array. Using this technique, we theoretically never run out of room in our DVD collection. The user of the DVDCollection object (the main method in this case) never has to worry about running out of space, because it’s all handled internally.

Figure 8.3 shows a UML class diagram of the Movies program. Recall that the open diamond indicates aggregation. The cardinality of the relationship is also noted: a DVDCollection object contains zero or more DVD objects.

The toString method of the DVDCollection class returns an entire report summarizing the collection. The report is created, in part, using calls to the toString method of each DVD object stored in the collection. Listing 8.9 shows the DVD class.

![](bbox=[0.25, 0.6, 0.85, 0.9])

FIGURE 8.3 A UML class diagram of the Movies program