When your program begins execution, it sends the initialize call method to all your classes. If you have a class and associated subclasses, the parent class gets the message first. This message is sent only once to each class, and it is guaranteed to be sent before any other messages are sent to the class. The purpose is for you to perform any class initialization at that point. For example, you might want to initialize some static variables associated with that class at that time.

# Scope Revisited

You can influence the scope of the variables in your program in several ways. You can do this with instance variables as well as with normal variables defined either outside or inside functions. In the following discussion, we use the term module to refer to any number of method or function definitions contained within a single source file.

# Directives for Controlling Instance Variable Scope

You know by now instance variables have scope that is limited to the instance methods defined for the class. So any instance method can access its instance variables directly by name, without having to do anything special.

You also know that instance variables declared in the interface section are inherited by a subclass. Inherited instance variables can also be accessed directly by name from within any method defined in that subclass. Again, this is without having to do anything special.

You can put directives in front of your instance variables when they are declared in the interface section, to more precisely control their scope:

+   - @protected—Methods defined in the class and any subclasses can directly access the instance variables that