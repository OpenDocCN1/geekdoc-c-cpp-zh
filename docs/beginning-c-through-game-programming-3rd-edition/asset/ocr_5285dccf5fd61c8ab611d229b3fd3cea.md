members declared in the derived class and losing access to member functions of the derived class.

Q: What good are abstract classes if you can’t instantiate any objects from them?

A: Abstract classes can be very useful. They can contain many common class members that other classes will inherit, which saves you the effort of defining those members over and over again.

# Discussion Questions

+   1. What benefits does inheritance bring to game programming?
+   2. How does polymorphism expand the power of inheritance?
+   3. What kinds of game entities might it make sense to model through inheritance?
+   4. What kinds of game-related classes would be best implemented as abstract?
+   5. Why is it advantageous to be able to point to a derived class object with a base class pointer?

# Exercises

+   1. Improve the Simple Boss 2.0 program by adding a new class, FinalBoss, that is derived from the Boss class. The FinalBoss class should define a new method, MegaAttack(), that inflicts 10 times the amount of damage as the SpecialAttack() method does.
+   2. Improve the Blackjack game program by forcing the deck to repopulate before a round if the number of cards is running low.
+   3. Improve the Abstract Creature program by adding a new class, OrcBoss, that is derived from Orc. An OrcBoss object should start off with 180 for its health data member. You should also override the virtual Greet() member function so that it displays: The orc boss growls hello.