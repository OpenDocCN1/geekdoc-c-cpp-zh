in response to a +sharedInstance message. A lot of singleton classes put the class name in this message name, in place of Instance.

To get the shared application object in an AppKit application, for example, you will send a +sharedApplication message to NSApplication. This class is a special case of a singleton, because it stores its shared instance in the global NSApp variable. If the application has already started, you can use this variable directly, avoiding the message send to get the application object.

The most common mistake with singletons is to introduce a race condition in creation. This particular singleton is storing an instance of itself in a private variable. It is tempting to create this in the +sharedInstance method. That will work fine for single-threaded applications, but what about multithreaded ones?

If you send the +sharedInstance message simultaneously from two threads, what happens? Both might test the variable, find that it hasn’t been created, and create it. To get around this, you could use a lock.

A much simpler solution is to create the instance in the +initialize method. This method is called by the runtime first time a message is sent to the class. It is the runtime’s responsibility to ensure that this method completes before any messages are delivered to