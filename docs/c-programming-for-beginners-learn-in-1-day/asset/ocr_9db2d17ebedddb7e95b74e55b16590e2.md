# # C# Abstract classes

An abstract class is used to define what is known as a base class. A base class is a class which has the most basic definition of a particular requirement.

A typical example of an abstract class is given below. Below is the definition of a class called ‘Animal’. When the ‘Animal’ class is defined, there is nothing known about the animal, whether it is a dog or a cat. The method called description is just a generic method defined for the class.

![](bbox=[0.308, 0.27, 0.691, 0.502])

Now when it is known what exactly the Animal is going to be, we create another class which inherits the base class. If we know that the animal is in fact a Dog, we create Dog class which inherits the main base class. The key difference here is that the Dog class cannot change the definition of the Description method of the Animal class. It has to define its own method called Dog-Description. This is the basic concept of abstract classes.

![](bbox=[0.308, 0.695, 0.691, 0.938])