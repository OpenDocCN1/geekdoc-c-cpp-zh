We can declare constructor methods just like usual method declarations but having the same name as the class.

It is worth noting that a class may have multiple constructor methods which allow different ways of passing parameters to member variables.

Let’s develop a small project where we will pass values to member variables using constructor methods.

+   1. Create a new C# project.
+   2. Add two TextBoxes and a Button on the form.
+   3. Set the Names and of the TextBoxes as input1 and input2.
+   4. Set the Name and Text of the Button as showButton and Show, respectively. The form will look as follows:

![](bbox=[0.3, 0.58, 0.7, 0.78])

Figure 12.15. Layout of the form

+   5. Right-click somewhere empty on the form and click View Code as we did before to open Form1.cs in the editor.
+   6. We will insert our class inside the Form1.cs file as it was done in Subsection 12.2. Declare our custom class named ShowText in Form1.cs file as below:

```
```csharp
public class ShowText
{
}
```
```

Code 12.16

Remember that we declare classes inside the namespace below the Form1 class in Form1.cs file.