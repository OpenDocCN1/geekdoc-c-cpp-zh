> A sealed class cannot declare any virtual methods. An abstract class cannot be sealed.

# Sealed methods

You can also use the sealed keyword to declare that an individual method in an unsealed class is sealed. This means that a derived class cannot override this method. You can only seal a method declared with the override keyword, and you declare the method as sealed override. You can think of the interface, virtual, override, and sealed keywords as follows:

+   - An interface introduces the name of a method.
* A virtual method is the first implementation of a method.
* An override method is another implementation of a method.
* A sealed method is the final implementation of a method.

# Implementing and using an abstract class

The following exercises use an abstract class to rationalize some of the code that you developed in the previous exercise. The Square and Circle classes contain a high proportion of duplicate code. It makes sense to factor this code into an abstract class called DrawingShape because this will help to ease maintenance of the Square and Circle classes in the future.

To create the DrawingShape abstract class

+   1. Return to the Drawing project in Visual Studio.
2. In Solution Explorer, select the Drawing project in the Drawing solution. On the Project method, select Add Class.
   The Add New Item - Drawing dialog opens.
3. In the Name box, type DrawingShape.cs, and then select Add.
   Visual Studio creates the class and displays it in the Code and Text Editor window.