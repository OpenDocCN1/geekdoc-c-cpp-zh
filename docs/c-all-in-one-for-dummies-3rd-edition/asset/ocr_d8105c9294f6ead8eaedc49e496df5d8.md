+   - Depth: 18 inches
+   - Address: A unique integer. But what number exactly? That depends on *which Mailbox* you’re talking about.

And each Mailbox has these capabilities:

+   - Open its door.
+   - Close its door.

Notice that we wrote the capabilities from the perspective of the Mailbox, not the person opening the Mailbox.

Now think about the question regarding the address printed on the Mailbox. What number goes on it? There are 16 different Mailbox objects, and each one gets a different number. So we can say this: The Mailbox class includes an address, which is an integer. Each instance of the Mailbox class gets its own number. The first may get 1, the second may get 2, and so on.

And so you have two concepts here for representing the mailboxes in code:

+   - **Mailbox class:** This is the general description of a mailbox. It includes no specifics, such as the actual address. It simply states that each mailbox has an address.
+   - **Mailbox instance:** This is the actual object. The Mailbox instance belongs to the class Mailbox. There can be several instances of the Mailbox class.

Think of the Mailbox class as a cookie cutter — or, in C++ terminology, the *type*. The Mailbox instance is an actual example of the class. In C++, you can create a variable of class Mailbox and set its Address integer to 1. Then you can create another variable of class Mailbox and set its Address integer to 2. Thus, you’ve created two distinct Mailbox objects, each of class Mailbox.

But all these have a width of 6, a height of 6, and a depth of 18. These are the same throughout the Mailboxes collection. Thus, you would probably not set those manually; instead, you would probably set them in the constructor for the class Mailbox. Nevertheless, the values of width, height, and depth go with each instance, not with the class; and the instances could, conceivably, each have their own width, height, and depth. However, when you design the class, you would probably put some stipulation in the class that these member variables cannot be changed. (You would do that by making them private and including a single function for each of them that retrieves their values.)