have it output to a file, edit the hex section of the file, and run the reverse encoding to get back a binary file. Doing so is a somewhat delicate operation because it is easy to mess up.

# Big Endian vs. Little Endian

The data in a file produced by a DataOutputStream probably does not exactly match what was in the memory of your computer because Java libraries write the data out in a platform-independent way. The discussion of binary data from chapter 3 is a generally accurate description of binary arithmetic, and it is perfectly correct at the byte level. However, when computer makers start laying out bytes in memory for larger groups like Int or Double, different computer makers picked different orders. For the x86 chips, Intel put the least significant byte first. This order is called Little Endian. Most other chip makers used the opposite ordering, called Big Endian. (The terms Big Endian and Little Endian are a reference to Gulliver's Travels where the Lilliputians were fighting a bitter war over which end of an egg one should crack when eating a soft-boiled egg.)

Looking closely at the hex dump above, you can see that Java writes files out in Big Endian order. You can tell this because we know that the first thing in the file is the Int value 10. An Int is stored in four bytes so the hex is the eight characters "0000000a". If the file were written using Little Endian this would be "0a000000". The reason Java uses this format, even though your computer inevitably does not (as you are most likely using an x86 based machine to run Scala), is inevitably related to the fact that when Sun®created Java, they had their own SPARC®architecture that was Big Endian.

# 22.4.3 Serialization

Often when you are saving data to a file, you want to write out whole objects. The process of converting an object to some format that you can write out and read back in later is called serialization. Java and a number of other modern platforms have built in serialization methods. The Java serialization method uses a binary output format. You can also write your own code to serialize objects in other formats. XML happens to be a useful serialization format. We will look at each of these separately.

# 22.4.3.1 Binary Serialization

The Java platform has a rather powerful form of serialization that is built into the system. Other systems have different ways of supporting this. To make a type that can be serialized in Scala have it inherit from Serializable.³ The reason you would want to have things that are serializable is that they can be used with ObjectInputStream and ObjectOutputStream. These types have the same methods as DataInputStream and DataOutputStream plus readObject():AnyRef and writeObject(obj:AnyRef):Unit, respectively.

To help illustrate this, consider the following little application that includes a serializable class and some code to either write an instance of it to a file or read one in from a file and print it.

³Case classes automatically inherit from Serializable.