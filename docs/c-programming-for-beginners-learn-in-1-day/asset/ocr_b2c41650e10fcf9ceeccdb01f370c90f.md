# C# Interface

Interfaces are used along with classes to define what is known as a contract. A contract is an agreement on what the class will provide to an application.

An interface declares the properties and methods. It is up to the class to define exactly what the method will do.

Let’s look at an example of an interface by changing the classes in our Console application. Note that we will not be running the code, because there is nothing that can be run using an interface.

Let’s create an interface class. The class will be called “Guru99Interface.” Our main class will then extend the defined interface. All the code needs to be written in the Program.cs file.

![](bbox=[0.06, 0.5, 0.92, 0.77])

# Code Explanation:-

+   1. We first define an interface called “Guru99Interface.” Note that the keyword “interface” is used to define an interface.
+   2. Next, we are defining the methods that will be used by our interface. In this case, we are defining the same methods which are used in all of earlier examples. Note that an interface just declares the methods. It does not define the code in them.
+   3. We then make our Guru99Tutorial class extend the interface. Here is where we actually write the code that defines the various methods declared in the interface. This sort of coding achieves the following