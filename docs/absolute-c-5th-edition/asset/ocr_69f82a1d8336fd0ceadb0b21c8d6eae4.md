# CHAPTER 14 Inheritance

One problem with this implementation is that it is unwieldy to add new creatures. Rewrite the class to use inheritance, which will eliminate the need for the variable type. The Creature class should be derived from the base class. The classes Demon, Elf, and Human should be derived from Creature. The cyberdemon and Balrog should be derived from Demon. You will need to rewrite the getSpecies() and getDamage() functions so they are appropriate for each class.

For example, the getDamage() function in each class should only compute the appropriate damage for that object. The total damage is then calculated by combining results of each level of the inheritance hierarchy. As an example, invoking getDamage() for a Balrog object should invoke getDamage() for the Demon object, which should invoke getDamage() for the Creature object, followed by the random 5% damage that demons infict, followed by the double damage that Balrog inflicts.

Also include mutator and accessor functions for the private variables. Write a main function that contains a driver to test your classes. Create an object for each type of creature and repeatedly outputs the results of getDamage().

+   11. Define a Bird class...
Finally, write a test program that creates instances of pet rocks and pet dogs that exercise the inherited and redefined functions.