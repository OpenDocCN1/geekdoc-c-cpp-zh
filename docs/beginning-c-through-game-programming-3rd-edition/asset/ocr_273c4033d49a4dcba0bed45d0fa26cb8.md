# CHAPTER 9

# ADVANCED CLASSES
AND DYNAMIC MEMORY:
GAME LOBBY

C++ gives a game programmer a high degree of control over the computer. One of the most fundamental abilities is direct control over memory. In this chapter, you’ll learn about *dynamic memory*—memory that you manage yourself. But with great power comes great responsibility, so you’ll also see the pitfalls of dynamic memory and how to avoid them. You’ll learn a few more things about classes, too. Specifically, you’ll learn to:

+   - Combine objects
+   - Use friend functions
+   - Overload operators
+   - Dynamically allocate and free memory
+   - Avoid memory leaks
+   - Produce deep copies of objects

# USING AGGREGATION

Game objects are often composed of other objects. For example, in a racing game, a drag racer could be seen as a single object composed of other individual objects, such as a body, four tires, and an engine. Other times, you might see an object as a collection of related objects. In a zookeeper simulation, you might see the zoo as a collection of an arbitrary number of animals. You can mimic these

![](bbox=[0.579, 0.117, 0.905, 0.393])