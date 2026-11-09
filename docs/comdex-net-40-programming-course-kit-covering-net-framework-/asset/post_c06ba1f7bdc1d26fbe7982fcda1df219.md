
![](img/9862a98a1a2d3bb14334137965a1ec60_232_0.png)

The **WriteLine** activity is used to display a line of text. You can notice in Fig.VB-6.4 that the **Properties** window displays the properties of the **WriteLine** activity. The **DisplayName** property indicates the name of the **WriteLine** activity. Using the **Text** property, you can specify a text expression that is displayed when the application is run. Note that the text expression must be enclosed within a pair of double quotes.

- 9. *Set* the **Text** property of the **WriteLine** activity to "This is a Workflow Application!" in the **Properties** window (Fig.VB-6.5).
- 10. *Press* the **F5** key on the keyboard to run the application. The output of the application appears (Fig.VB-6.6).

![](img/9862a98a1a2d3bb14334137965a1ec60_232_1.png)

In this section, you have learned to develop a sample workflow application. Next, you learn to implement conditions in workflows.

## Implementing Conditions in Workflows

You can easily create a WF application that can implement a condition in an application. Activities, such as **If** and **While** can be used to implement conditions in a workflow application. Perform the following steps to implement conditions in a workflow application:

- 1. *Start* **Visual Studio 2010**.
- 2. *Select* **File → New → Project** from the menu bar. The **New Project** dialog box opens.
- 3. *Select* **Visual Basic → Workflow** from the **Installed Templates** section in the left pane of the **New Project** dialog box.
- 4. *Select* **Workflow Console Application** in the middle pane to create a workflow console application.
- 5. *Enter* the name of the application as **ImplementingConditions** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** combo box.
- 6. *Click* the **OK** button to close the **New Project** dialog box. The **ImplementingConditions** application is created (Fig.VB-6.7).
- 7. *Drag* the **Sequence** activity from the **Control Flow** tab of the **Toolbox** and *drop* it on the workflow designer (Fig.VB-6.8).

Since a workflow is similar to a Visual Basic program; therefore, it is capable of storing variables, passing arguments or data in and out of workflow, and importing namespaces. You can use the **Variables** button at the bottom of the workflow designer to declare and define variables for your workflow application. Similarly, you can use the **Arguments** and **Imports** button to pass arguments and import namespaces, respectively.

- 8. *Select* the **Sequence** activity and *click* the **Variables** button at the bottom of the workflow designer (Fig.VB-6.8).
- 9. *Enter* **strHello** in the text box under the **Name** column (Fig.VB-6.8).
- 10. *Enter* "**Hello World**" in the text box under the **Default** column (Fig.VB-6.8).

![](img/9862a98a1a2d3bb14334137965a1ec60_233_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_233_1.png)

Fig.VB-6.7

Fig.VB-6.8

In Fig.VB-6.8, the **String** and **Sequence** values are automatically displayed under the **Variable type** and **Scope** columns, respectively.

- 11. *Click* the **Arguments** button to declare an argument for accepting some input from the user (Fig.VB-6.9).
- 12. *Enter* **strName** in the text box under the **Name** column (Fig.VB-6.9).

In Fig.VB-6.9, the **In** and **String** values are automatically displayed under the **Direction** and **Argument type** columns, respectively.

- 13. *Drag* the If activity from the **Control Flow** tabs of the **Toolbox** and *drop* it inside the **Sequence** activity to implement the if-then-else conditional expression (Fig.VB-6.10).

![](img/9862a98a1a2d3bb14334137965a1ec60_233_2.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_233_3.png)

Fig.VB-6.9

Fig.VB-6.10

- 14. *Add* a condition in the **Condition** text box inside the If activity to check whether the length of the string that the user has entered is greater than 6 or not (Fig.VB-6.11).
- 15. *Drag* the **WriteLine** activity from the **Primitives** tab of the **Toolbox** and *drop* it inside the **Then** part of the If activity (Fig.VB-6.11).
- 16. *Enter* the text "The length of the string is greater than 6" in the **Text** text box inside the **WriteLine** activity (Fig.VB-6.11).
- 17. *Drag* another **WriteLine** activity from the **Primitives** tab of the **Toolbox** and *drop* it inside the **Else** part of the If activity (Fig.VB-6.12).
- 18. *Enter* the text "The length of the string is less than 6" in the **Text** text box inside the second **WriteLine** activity (Fig.VB-6.12).

![](img/9862a98a1a2d3bb14334137965a1ec60_234_0.png)

Fig.VB-6.11

![](img/9862a98a1a2d3bb14334137965a1ec60_234_1.png)

Fig.VB-6.12

- 19. *Open* **Solution Explorer** by selecting the **View → Solution Explorer** option from the menu bar.
- 20. *Right-click* the **Module1.vb** file in **Solution Explorer** and select the **View Code** option from the context menu to open the **Module1.vb** file in Code Editor, as shown in Fig.VB-6.13.

![](img/9862a98a1a2d3bb14334137965a1ec60_234_2.png)

Fig.VB-6.13

- 21. *Add* the highlighted code snippet shown in Listing 6.1 to Code Editor:

### Listing 6.1: Implementing the If-Else Condition

```vb
Sub Main()
    Dim myWorkflow As New Workflow()
    Console.Write("Enter your name")
    myWorkflow.strName = Console.ReadLine()
    workflowInvoker.Invoke(myWorkflow)
    Console.ReadLine()

End Sub
```

In the highlighted lines of Listing 6.1, you are asked to enter your name. When you enter your name, the Invoke method of the **WorkflowInvoker** class is called to invoke the workflow created in the **ImplementingConditions** application. When the workflow is executed, the condition inside the If activity checks whether the length of the entered string is greater than 6 or not. Depending on the length of the entered string, a corresponding message is displayed on the output screen.

- 22. Press the `F5` key on the keyboard to run the application. The output of the application appears asking you to enter your name (Fig.VB-6.14).
- 23. Enter your name (Fig.VB-6.14). A message appears indicating whether the length of the name string is greater than or less than 6, as shown in Fig.VB-6.14:

![](img/9862a98a1a2d3bb14334137965a1ec60_235_0.png)

Fig.VB-6.14

In this section, you learned to implement conditions in workflows. Let's now learn how to create and use custom activities.

## Creating and Using Custom Activities

Although the built-in activity library provides you with a large set of activities; yet sometimes, it may happen that the desired activity is not available in the built-in activity library. In such a situation, you can create custom workflow activities from scratch to meet specific business needs. WF allows you to create your own custom activities that you can later use with your workflow applications.

Perform the following steps to create a custom activity:

- 1. *Start* *Visual Studio 2010*.
- 2. Select *File → New → Project* from the menu bar. The *New Project* dialog box opens (Fig.VB-6.15).
- 3. Select *Visual Basic → Workflow* from the *Installed Templates* section in the left pane of the *New Project* dialog box (Fig.VB-6.15).
- 4. Select *Activity Library* in the middle pane to create a custom activity library (Fig.VB-6.15).
- 5. Enter a name for the application in the *Name* text box (Fig.VB-6.15). In our case, we have entered *MyCustomActivity* (also available on the CD) as the name of the application.
- 6. Enter an appropriate location for the application in the *Location* combo box (Fig.VB-6.15). In our case, we have entered `D:\Comdex\Applications\Visual Basic 2010\Chapter 6\`.
- 7. Click the *OK* button to close the *New Project* dialog box, as shown in Fig.VB-6.15.

![](img/9862a98a1a2d3bb14334137965a1ec60_235_1.png)

Fig.VB-6.15

The *MyCustomActivity* application is created, as shown in Fig.VB-6.16:
