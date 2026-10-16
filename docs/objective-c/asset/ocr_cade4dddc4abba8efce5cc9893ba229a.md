# Reading and Writing Data with NSCoder

Many modern languages include the ability to encode objects into data, which can be archived to disk or sent over a network connection. This process is known as serialization. The idea is that in cases where you want to send an object from one process to another, either via disk or via network, you need a mechanism that freezes the object in place, including all of its data in a platform agnostic form so that it can be thawed and reconstituted by the recipient of the object and have all of its data intact.

Objective-C uses a suite of classes and protocols to implement serialization. The centerpiece of the Objective-C serialization system is the NSArchiver and NSUnarchiver classes. Using them, you feed them objects which conform to the NSCoding protocol, and they take the objects and serialize the objects to a data format which is transferable to disk or over the network.

So to use Objective-C serialization, the first thing you need to do is implement the NSCoding protocol on your objects.

# Implementing the NSCoding Protocol in Your Objects

The NSCoding protocol defines two methods that must be implemented on your object in order to be NSCoding compliant. The first is the -encodeWithCoder: method. This method is called by the archiver when it needs to serialize your object. It takes an NSCoder as a parameter. NSCoder is an abstract base class. Typically the actual objects that will be passed to you will be instances of NSArchiver or NSKeyedArchiver. Using the NSCoder, you then archive the member variables of your object into it.

# Encoding objects

To serialize your member variables into the NSCoder, you use the methods on the instance of NSCoder which has been passed into your -encodeWithCoder: method. NSCoder provides a variety of methods for the purposes of encoding basic types as well as

+   In This Chapter
+   Learning about serialization
+   Implementing the NSCoding protocol
+   Using NSArchiver and NSUnarchiver to archive objects to disk