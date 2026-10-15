![](bbox=[0.26, 0.14, 0.82, 0.24])

# FIGURE 13.1 A linked list

> KEY CONCEPT
> A dynamically linked list is managed by storing and updating references to objects.

object’s next reference can refer to a third Node object, and so on, creating a linked list. The first node in the list could be referenced using a separate variable. The last node in the list would have a next reference that is null, indicating the end of the list. Figure 13.1 depicts this situation.

In this example, the information stored in each Node class is a simple integer, but keep in mind that we could define a class to contain any amount of information of any type.

# A Dynamically Linked List

The program in Listing 13.1 sets up a list of Magazine objects and then prints the list. The list of magazines is encapsulated inside the MagazineList class shown in Listing 13.2 and is maintained as a dynamically linked list.

The MagazineList class represents the list of magazines. From outside of the class (an external view), we do not focus on how the list is implemented. We don’t know, for instance, whether the list of magazines is stored in an array or in a linked list. The MagazineList class provides a set of methods that allows the user to maintain the list of magazines. That set of methods, specifically add and toString, defines the operations to the MagazineList ADT.

The MagazineList class uses an inner class called MagazineNode to represent a node in the linked list. Each node contains a reference to one magazine and a reference to the next node in the list. Because MagazineNode is an inner class, it is reasonable to allow the data values in the class to be public. Therefore, the code in the MagazineList class refers to those data values directly.

The Magazine class shown in Listing 13.3 is well encapsulated, with all data declared as private and methods provided to accomplish any updates necessary. Note that because we use a separate class to represent a node in the list, the Magazine class itself does not need to contain a link to the next Magazine in the list. That allows the Magazine class to be free of any issues regarding its containment in a list.

> VideoNote
> Example using a linked list.