# A Closer Look at Methods and Classes

This chapter resumes the examination of classes and methods. It begins by explaining how to control access to the members of a class. It then discusses the passing and returning of objects, method overloading, the various forms of Main(), recursion, and the use of the keyword static.

# Controlling Access to Class Members

In its support for encapsulation, the class provides two major benefits. First, it links data with code. You have been taking advantage of this aspect of the class since Chapter 6. Second, it provides the means by which access to members can be controlled. It is this second feature that is examined here.

Although C#'s approach is a bit more sophisticated, in essence, there are two basic types of class members: public and private. A public member can be freely accessed by code defined outside of its class. This is the type of class member that we have been using up to this point. A private member can be accessed only by methods defined by its class. It is through the use of private members that access is controlled.

Restricting access to a class' members is a fundamental part of object-oriented programming because it helps prevent the misuse of an object. By allowing access to private data only through a well-defined set of methods, you can prevent improper values from being assigned to that data—by performing a range check, for example. It is not possible for code outside the class to set the value of a private member directly. You can also control precisely how and when the data within an object is used. Thus, when correctly implemented, a class creates a “black box” that can be used, but the inner workings of which are not open to tampering.

# C#'s Access Modifiers

Member access control is achieved through the use of four access modifiers: public, private, protected, and internal. In this chapter, we will be concerned with public and private. The protected modifier applies only when inheritance is involved and is described in Chapter 11.