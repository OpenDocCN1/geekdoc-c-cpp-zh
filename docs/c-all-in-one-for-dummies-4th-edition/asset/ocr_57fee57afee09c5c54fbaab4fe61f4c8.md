# IN THIS CHAPTER

+   - Understanding what design patterns are and how you can use them
+   - Implementing an observer pattern
+   - Building a mediator pattern

# Chapter 4

# Building with Design Patterns

When you work as a developer, eventually you start to notice that you do certain things repeatedly. For example, when you need to keep track of how many instances of a certain class you create, you define a static property called something like `InstanceCount`, include a line that increments `InstanceCount` in the constructor, and include a line that decrements `InstanceCount` in the destructor. You make `InstanceCount` private and include a static method that retrieves the value, such as `getInstanceCount()`.

Because you use it so often, it becomes a pattern. The first time you used it, you had to think about it — how to design and implement it. Now, you barely have to think about it; you just do it. Thus, it’s a *design pattern* that you use.

This chapter takes a practical look at design patterns that you use when creating applications. It helps you understand why using design patterns reduces development time, makes code less error prone, and improves application efficiency. The chapter delves just a bit into history and usage, with the usage considerations relying on the singleton pattern as a starting point.

You also see how to create and use two common design patterns: observer and mediator. You may or may not actually use these patterns in your applications, but by seeing how they’re put together, you can find or create other patterns that will make your development process easier.