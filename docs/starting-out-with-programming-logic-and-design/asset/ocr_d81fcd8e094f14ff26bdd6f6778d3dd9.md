4. In pseudocode, write the first line of the definition for a Poodle class. The class should extend the dog class.

5. Look at the following pseudocode class definitions:
Class Plant
  Public Module message()
  Display "I'm a plant."
  End Module
End Class
Class Tree Extends Plant
  Public Module message()
Display "I'm a tree."
  End Module
End Class

Given these class definitions, what will the following pseudocode design?
Declare Plant p
Set p = New Tree()
Call p.message()

# Programming Exercises

+   1. Pet Class

Design a class named Pet, which should have the following fields:

+   - name: The name field holds the name of the pet.
- type: The type field holds the type of animal that a pet is. Examples values are "Dog", "Cat", and "Bird".
- age: The age field holds the pet's age.

The Pet class should have the following methods:

+   - setName: The setName method stores a value in the name field.
- setType: The setType method stores a value in the type field.
- setAge: The setAge method stores a value in the age field.
- getName: The getName method returns the value of the name field.
- getType: The getType method returns the value of the type field.
- getAge: The getAge method returns the value of the age field.

Once you have designed the class, design a program that creates an object of the class and prompts the user to enter name, type, and age of his or her pet. This data should be stored in the object. Use the object's accessor methods to retrieve the pet's name, type, and age and display this data on the screen.

# 2. Car Class

Design a class Car that has the following fields:

+   - yearModel: The yearModel field is an Integer that holds the car's year model.
- make: The make field references a String that holds the make of the car.
- speed: The speed field is an Integer that holds the car's current speed.

In addition, the class should have the following constructor and other methods:

+   - Constructor: The constructor should accept the car's year model and make as arguments. These values should be assigned to the object's yearModel and make fields. The constructor should also assign 0 to the speed field.

![](bbox=[0.128, 0.406, 0.175, 0.453])