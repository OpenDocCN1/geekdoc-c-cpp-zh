# TASK LIST

In this chapter we'll explore the ways in which WPF extends the way that .NET objects can communicate and interact with the dependency property system.

![](bbox=[0.093, 0.226, 0.253, 0.306])

# CALCULATING DEPENDENCY PROPERTY VALUES

As we'll see, dependency properties can do a lot of cool things, but the one you'll rely on most often is their ability to calculate their values, so we'll begin by exploring exactly how that happens.

![](bbox=[0.093, 0.366, 0.253, 0.446])

# DEPENDENCY PROPERTY CLASSES

Like any set of .NET objects, the class hierarchy defines how dependency properties function and interact, so after we've explored how they arrive at their final values, we'll take a quick look at the class hierarchy that defines them.

![](bbox=[0.093, 0.516, 0.253, 0.596])

# CREATING DEPENDENCY PROPERTIES

There are several steps to creating a dependency property in the classes you define, and, frankly, the syntax is pretty complex. Fortunately, Visual Studio includes a code snippet that does (almost) all the heavy lifting. We'll see how that works in the next section of the chapter.

![](bbox=[0.093, 0.676, 0.253, 0.756])

# DEPENDENCY PROPERTY CALLBACKS

At the end of the chapter, we'll come full circle when we explore how you can control the calculated value of a dependency property using callback methods. A callback is rather like an event handler—it's a method that's called at specific points during processing. Dependency properties support three callbacks, and we'll finish the chapter by examining them.