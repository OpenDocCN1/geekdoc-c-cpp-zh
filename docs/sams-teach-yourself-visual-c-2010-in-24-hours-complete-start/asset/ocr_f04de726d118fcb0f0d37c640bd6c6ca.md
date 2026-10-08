+   1. Create a new Console application.

+   2. Add a new class file named `Vehicles.cs` and implement the basic class hierarchy shown in Listing 4.1.

+   3. In the `Main` method of the `Program.cs` file, enter the following code:

```
```
Vehicle v1 = new Vehicle();
Car c1 = (Car)v1;
```
```

+   4. Run the application by pressing Ctrl+F5. You should encounter an `InvalidCastException`, as shown in Figure 4.2.

![](bbox=[0.245, 0.35, 0.65, 0.455])

**FIGURE 4.2**
Result showing an InvalidCast Exception

+   5. Remove the statements you previously entered from step 2, and replace it with the code shown in Listing 4.2.

+   6. Run the application again by pressing Ctrl+F5 and observe that the output matches what is shown in Figure 4.3.

![](bbox=[0.255, 0.59, 0.655, 0.695])

**FIGURE 4.3**
Result of working with class inheritance and polymorphism

Listing 4.3 shows a modified version of the code hierarchy from Listing 4.1, providing constructors for some of the derived classes that call one of base class constructors.

**Watch Out!**

# ### Constructor Chaining and Default Constructors

If you don’t explicitly chain a base class constructor, the compiler tries to chain the default constructor.

The problem here is that not all classes have a public default constructor, in which case forgetting to explicitly chain the correct base class constructor can result in a compiler error.