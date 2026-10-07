The Foundation classes for working with arrays provide many conveniences. However, in the case of manipulating large arrays of numbers with complex algorithms, learning how to perform such a task using the lower-level array constructs provided by the underlying C language might be more efficient, in terms of both memory usage and execution speed. Refer to the section titled "Arrays" in Chapter 13 for more information.

# # Making an Address Book

Let's take a look at an example that starts to combine a lot of what you've learned to this point by creating an address book. Your address book will contain address cards. For the sake of simplicity, your address cards will contain only a person's name and email address. Extending this concept to other information, such as address and phone number, straightforward, and we leave that as an exercise for you at the end of this chapter.

The two classes we'll create, an AddressBook and an AddressCard class, and the relation between the two is depicted in Figure 15.5.

![](bbox=[0.175, 0.435, 0.825, 0.575])

Figure 15.5 An AddressBook that contains AddressCards

# # Creating an Address Card

We start by defining the AddressCard class. You'll want the capability to create a new address card, set its name and email fields, retrieve those fields, and print the card. In a graphics environment, you could use some handy methods to draw your card on your computer's screen or iOS device's window. But here you stick to a simple Console interface to display your address cards.

Program 15.8 shows the interface file for your new AddressCard class. We're not going to synthesize the accessor methods yet; writing them yourself offers valuable lessons.

 Mac OS X and iOS provide an entire Address Book framework that offers extremely powerful capabilities for working with address books.