# # Observing the Mailbox class

Consider the characteristics and capabilities of the `Mailbox` class. Each `Mailbox` has these properties:

+   - Width: 6 inches
+   - Height: 6 inches
+   - Depth: 18 inches
+   - Address: A unique integer

And each `Mailbox` has these methods:

+   - Open its door.
+   - Close its door.

Notice that the methods are from the perspective of the `Mailbox`, not the person opening the `Mailbox`.

Now think about the question regarding the address printed on the `Mailbox`. There are 16 different `Mailbox` objects, and each one gets a different number. So it’s possible to say this: The `Mailbox` class includes an address, which is an integer. Each instance of the `Mailbox` class gets its own number. The first may get 1, the second may get 2, and so on. So you have two concepts here for representing the mailboxes in code:

+   - **Mailbox class:** This is the general description of a mailbox. It includes no specifics, such as the actual address. It simply states that each mailbox has an address.
+   - **Mailbox instance:** This is the actual object. The `Mailbox` instance belongs to the class `Mailbox`. There can be any number of instances of the `Mailbox` class.

Think of the `Mailbox` class as a cookie cutter — or, in C++ terminology, the *type*. The `Mailbox` instance is an actual example of the class. In C++, you can create a variable of class `Mailbox` and set its Address integer to 1. Then, you can create another variable of class `Mailbox` and set its Address integer to 2. Thus, you’ve created two distinct `Mailbox` objects, each of class `Mailbox`.