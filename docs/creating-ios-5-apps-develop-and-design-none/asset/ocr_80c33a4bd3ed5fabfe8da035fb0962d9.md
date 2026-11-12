![](bbox=[0.06, 0.15, 0.92, 0.36])

Each class should have a designated initializer, a single method responsible for performing all of the object's setup and initialization. Typically, this is the initializer with the largest number of arguments. All the other initializers should call the designated initializer—letting it do all the heavy lifting.

Similarly, your designated initializer needs to call your superclass's designated initializer. By chaining our class hierarchy together, designated initializer to designated initializer, we guarantee that the object gets initialized properly all the way up the class hierarchy.

Finally, your class should always override its superclass's designated initializer. This will re-route any calls to any of the superclass's initializers (or any initializer anywhere in the class hierarchy) back through your designated initializer and then up the class hierarchy.

Let's take a concrete example. Imagine we are making an Employee class. This will be a subclass of NSObject. NSObject has only one initializer, init. This is (by default) its designated initializer. Our Employee class, on the other hand, will have three instance variables: _firstName, _lastName, and _id. Its designated initializer will set all three values.

Let's start by pulling a blank init method from the Code Snippet library. At the bottom of the Utilities area, click the Code Snippet tab (it looks like a pair of curly braces) and then scroll down until you find the Objective-C init method (Figure 2.2). You can click and drag this out into your implementation block.

Modify the template as shown here. You will also need to copy the method's signature into the Employee class's interface block.