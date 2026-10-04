# CHAPTER 12

# Generics

In this chapter:

+   - Generics in the Framework Class Library ................................. . . 270
- Generics Infrastructure ................................................................. . . . . . . 271
- Generic Interfaces ....................................................................................................... 277
- Generic Delegates ................................................................................................................... 278
- Delegate and Interface Contra-variant and ....................................................................
- Covariant Generic Type Arguments ................................................................................... 279
- Generic Methods ..................................................................................................................... 281
- Generics and Other Members ........................................................................................ 284
- Verifiability and Constraints ................................................................................ 284

Developers who are familiar with object-oriented programming know reuse the benefits it offers. One of the big benefits that makes developers extremely productive is code reuse, which is the ability to derive a class that inherits all of the capabilities of a base class. The derived class can simply override virtual methods or add new methods to customize the behavior of the base class to meet the developer's needs. *Generics* is another mechanism offered by the common language runtime (CLR) and programming languages that provides one more form of code reuse: algorithm reuse.

Basically, one defines an algorithm such as sorting, searching, swapping, or converting. However, the developer defining the algorithm does not specify what data type(s) the algorithm operates on; the algorithm can be generically applied to objects of different types. Another developer can then use this algorithm as long as he indicates the specific data type(s) the algorithm should operate on, for example, a sorting algorithm that operates on Int32s, Strings, etc., or a comparing algorithm that operates on DateTimes, Versions, etc.

Most algorithms are encapsulated in a class, and the CLR allows the creation of generic reference types as well as generic value types, but it does not allow the creation of generic enumerated types. In addition, the CLR allows the creation of generic interfaces and generic delegates. Occasionally, a single method can encapsulate a useful algorithm, and therefore, the CLR allows the creation of generic methods that are defined in a reference type, value type, or interface.

Let's look at a quick example. The Framework Class Library (FCL) defines a generic list algorithm that knows how to manage a set of objects; the data type of these objects is not specified by the generic algorithm. Someone wanting to use the generic list algorithm can specify the exact data type to use with it later.

265