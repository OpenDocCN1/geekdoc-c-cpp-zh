# Using the Java API Documentation

# E.1 Introduction

The Java class library contains thousands of predefined classes and interfaces that programmers can use to write their own applications. These classes are grouped into packages based on their functionality. For example, the classes and interfaces used for file processing are grouped into the java.io package, and the classes and interfaces for networking applications are grouped into the java.net package. The Java API documentation lists the public and protected members of each class and the public members of each interface in the Java class library. The documentation overviews all the classes and interfaces, summarizes their members (i.e., the fields, constructors and methods of classes, and the fields and methods of interfaces) and provides detailed descriptions of each member. Most Java programmers rely on this documentation when writing programs. Normally, programmers would search the API to find the following:

+   1. The package that contains a particular class or interface.
+   2. Relationships between a particular class or interface and other classes and interfaces.
+   3. Class or interface constants—normally declared as public static final fields.
+   4. Constructors to determine how an object of the class can be initialized.
+   5. The methods of a class to determine whether they’re static or non-static, the number and types of the arguments you need to pass, the return types and any exceptions that might be thrown from the method.

In addition, programmers often rely on the documentation to discover classes and interfaces that they have not used before. For this reason, we demonstrate the documentation with classes you know and classes you may not have studied yet. We show how to use the documentation to locate the information you need to use a class or interface effectively.

# E.2 Navigating the Java API

The Java API documentation can be downloaded to your local hard disk or viewed online. To download the Java API documentation, go to www.oracle.com/technetwork/java/javase/downloads/index.html/ scroll down to the Additional Resources section and click the Download Zip button to the right of Java SE 6 Documentation. You’ll be asked to accept a license agreement. To do this, click Accept, then click Continue. Click the link to