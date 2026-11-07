# # 7 User-Defined Types: Classes

This is the first chapter in which we use C++ as an object-oriented language. In previous chapters we discussed the basics, and we will need what we learned in those chapters to understand the materials we use in this chapter and the rest of the book. In this chapter, we show how to create new types and how to use them. The mechanism for creating new types uses a *class* or an enumerated type. We will discuss classes in this chapter but we will ignore discussion on enumerated types because they are not common.

+   **Objectives**
+   
+   After you have read and studied this chapter, you should be able to:
+   
+   * Introduce object-oriented concepts, including types and instances, attributes and behaviors, and data members and member functions.
+   * Discuss the class definition that declares data members and member functions.
+   * Discuss three types of constructors: parameter constructors, default constructors, and copy constructors.
+   * Discuss destructors that are used to clean up the objects before they are recycled.
+   * Discuss instance data members and instance member functions.
+   * Discuss static data members and static member functions.
+   * Discuss how we divide the three sections of a program into three separate files—interface file, implementation file, and application file—and achieve one of the goals of object-oriented programming: encapsulation.

# ## 7.1 INTRODUCTION

In Chapter 1, we mentioned that C++ is a combination of a procedural and an object-oriented language. In previous chapters, we have used the language mostly as a procedural language; in this chapter we start using it as an object-oriented language.

# ### 7.1.1 Types and Instances in Real Life

A *type* is a concept from which an *instance* is created. In other words, a type is an abstraction; an **instance** of that type is a concrete entity. The word *clock* is a type; it defines a general concept that we are familiar with. The clock in John's office, the clock in Sue's office, or the clock in a train station are instances of this type. The word *circle* is a type. We can draw circles with different radii as instances of that type. We can even go further and say that the word *person* is a type, and that John, Sue, and Michelle are instances of the type person.

The relationship between a type and its instances is a one-to-many relation. We can have many instances from one single type. Figure 7.1 shows the type *Circle* and four instances that we call *circle1*, *circle2*, *circle3*, and *circle4*.