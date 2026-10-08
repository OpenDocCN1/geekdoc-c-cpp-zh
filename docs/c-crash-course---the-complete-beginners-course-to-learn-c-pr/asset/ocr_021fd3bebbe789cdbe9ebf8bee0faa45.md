# # Chapter 9
Inheritance

**Objective:** Classes and OOP give you the ability to derive from parent classes. This chapter explains inheritance within your class structure.

OOP is more than just creating classes and building a program that can call other classes. You can derive your child classes from parent classes, so you don't need to repeat code for similar objects. Inheritance can be complex if you don't create a good class design, so this chapter attempts to explain inheritance and how you should set up your class structure for the best scalable code.

# **Understanding Basic Inheritance

Inheritance lets you derive child classes from parent classes. Think about animals. If you have a lion and a parrot, both of these animals have very different characteristics, and they have similar ones as well. They are both animals, but one is a bird and one is a mammal. If you didn't use inheritance, you would need to create two classes that describe both animals from top to bottom.

With inheritance, you can create one class that describes basic features of an animal, and then derive child classes from the main parent class. For instance, both birds and lions have eyes and feet. Their eyes and feet might look different, but they still have them. Other characteristics are different, but all lions and birds have feet. You can create a parent animal class that defines feet and eyes, and then the child lion and bird classes can define characteristics specific to their respective animals.

The purpose of inheritance is to make it unnecessary to repeat your code. Without it, you'd have to create a bird and a lion class that defined the eyes and feet of each animal, which would create redundant code. When you create redundant code, you make it more difficult to manage your code. When you create ten classes that define the eyes of an animal and you need to change that description, you need to change all ten of those classes. This opens up more room for bugs and issues when you try to scale your code, which you want to avoid.

Not every class must be a parent or child class. You can create code with standalone classes that aren't derived from any other code. The way you design your code is up to you and the needs of the program you want to create.

# **Inheriting from a Parent Class

Before you create your child class, you need to create a parent class. Since we're using