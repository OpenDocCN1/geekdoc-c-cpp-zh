Examine Example 4–16 closely. Each of the constructors are tested and the values are displayed using the `Console.WriteLine()` method. As you type the program statements, you will be aided with intellisense as shown in Figure 4–4.

![](bbox=[0.176, 0.16, 0.766, 0.204])

**Figure 4-4**  Intellisense displays available constructors

In addition to revealing the available constructors methods as shown in Figure 4–4, intellisense also displays all public members of the class once an object is instantiated. As you examine Figure 4–5, notice that none of the data members are present.

![](bbox=[0.176, 0.323, 0.731, 0.54])

**Figure 4-5**  Public members of the Student class

The data members were defined with an access mode of `private`. They are accessible only inside the `Student` class.

The `StudentApp` class has a number of class methods that are called from `Main()`. You will recall that class methods require the keyword `static` and are not associated with a specific object. These methods, `AskForExamScore()`, `AskForStudentName()`, `AskForMajor()`, and `AskForStudentNumber()` are used by `Main()` to enable the user to input data. The values that are returned are assigned to data members of `firstStudentObject`. However, since the data members of the class are defined as `private`, the `public` properties must be used for the assignments. The output from the application is shown in Figure 4–6.