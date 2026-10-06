method explicitly from the DemoExtensionMethod class. The parameter in the method is implied, just as these references are always implied in instance methods. Figure 10-42 shows the execution of the program.

```
Original account number was 49
Revised account number is 493
```

**Figure 10-42** Execution of the DemoExtensionMethod program

You can create methods for your own classes in the same way one was created for the Int32 class in this example. Just like other methods, unlike ordinary class instance methods, extension methods cannot access any private members of classes they extend. Furthermore, if a class contains an instance method with the same signature as an extension method, the instance method takes priority and will be the one that executes.

![](bbox=[0.105, 0.439, 0.839, 0.725])

# Recognizing Inheritance in GUI Applications

When you create a Windows Forms application using Visual Studio's IDE, you automatically get inheritance. Every Form you create is a descendant of the Form class. Figure 10-43 shows a project in which the programmer double-clicked the automatically generated Form to expose the code. You can see that the automatically generated Form1 class extends Form.