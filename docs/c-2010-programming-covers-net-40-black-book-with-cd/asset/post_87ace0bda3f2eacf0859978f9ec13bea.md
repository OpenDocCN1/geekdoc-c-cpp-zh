
## Immediate Solutions

## Creating a Simple WF Application

In this section, we create a workflow console application, named SimpleWFApp (also available on the CD). Perform the following steps to create the SimpleWFApp application:

- 1. Open Visual Studio 2010.
- 2. Select File→New→Project. The New Project dialog box opens (Figure 28.1).
- 3. Select Visual C#→Workflow in the Installed Templates section, and then select the Workflow Console Application template. Enter a name and location in the Name and Location text boxes, respectively. In our case, the application name is SimpleWFApp and the location is D:\Black Books\C# 2010\Chapter 28\, as shown in Figure 28.1:

![](img/e073a4882197be4ab61103cbe0bcb394_1411_0.png)

### Figure 28.1: Displaying the New Project Dialog Box

The SimpleWFApp application is displayed in Visual Studio 2010, as shown in Figure 28.2:

![](img/e073a4882197be4ab61103cbe0bcb394_1411_1.png)

### Figure 28.2: Displaying a Newly Created WF Application in Visual Studio 2010

- 4. Drag and drop a Sequence activity from the Control Flow category of the Toolbox to the designer (Figure 28.3).
- 5. Drag and drop a WriteLine activity from the Primitives category of the Toolbox between the arrows of Sequence activity, as shown in Figure 28.3:

![](img/e073a4882197be4ab61103cbe0bcb394_1412_0.png)

Figure 28.3: Adding the Sequence and WriteLine Activities

- 6. Select the WriteLine activity and press the F4 key to open the Properties dialog box. Figure 28.4 shows the properties of a WriteLine activity:

![](img/e073a4882197be4ab61103cbe0bcb394_1412_1.png)

Figure 28.4: Displaying the Properties of a WriteLine Activity

- 7. Select the ellipse button beside the Text property. The Expression Editor dialog box opens (Figure 28.5).
- 8. Enter the "Hello World !!!" text in the Text (String) text area and click the OK button, as shown in Figure 28.5:

### Figure 28.5: Displaying the Expression Editor Dialog Box

- 9. Press the CTRL+F5 keys combination on the keyboard to run the SimpleWFApp application. Figure 28.6 shows the output of the SimpleWFApp application:

![](img/e073a4882197be4ab61103cbe0bcb394_1413_0.png)

### Figure 28.6: Displaying the Output of the SimpleWFApp Application

Now, Let’s discuss about using the If activity and variables.

## Using the If Activity and Variables

In this section, we create a workflow console application, named IfAndVariables (also available on the CD). In this application, we are taking two variables and showing the greatest number.

Perform the following steps to use the If activity and variables:

- 1. Create a workflow console application, IfAndVariables.
- 2. Drag and drop a Sequence Activity from the Control Flow category of the Toolbox to the Workflow1.xaml designer file.

> NOTE
> The Workflow1.xaml file is automatically created when a workflow console application is created.

- 3. Drag and drop a WriteLine Activity from the Primitives category of the Toolbox to the Sequence Activity, as shown in Figure 28.7:

![](img/e073a4882197be4ab61103cbe0bcb394_1413_1.png)

### Figure 28.7: Adding a WriteLine Activity in Sequence Activity

- 4. Set the Text property of the WriteLine activity to There are two numbers x and y.
- 5. Click the Variables button and then click the Create Variable link, as shown in Figure 28.8:

![](img/e073a4882197be4ab61103cbe0bcb394_1414_0.png)

### Figure 28.8: Displaying the Variables Button and the Create Variable Link

- 6. Enter a variable, x, in the Name field, Int32 in the Variable type field, Sequence in the Scope field, and 20 in the Default field, as shown in Figure 28.9:

![](img/e073a4882197be4ab61103cbe0bcb394_1414_1.png)

### Figure 28.9: Creating the x Variable

Similarly, create another variable, y, with Int32 value in the variable type and 50 value in the Default field, as shown in Figure 28.10:

![](img/e073a4882197be4ab61103cbe0bcb394_1414_2.png)

### Figure 28.10: Creating the y Variable

- 7. Drag and drop an If activity from the Toolbox to the designer, below the WriteLine activity, as shown in Figure 28.11:

![](img/e073a4882197be4ab61103cbe0bcb394_1414_3.png)

### Figure 28.11: Displaying the If Activity in the Sequence Activity

- 8. Select the If activity an press the F4 key to open the Properties window.
- 9. Click the ellipse button of the Condition property to open the Expression Editor dialog box (Figure 28.12).
- 10. Set the Condition property of If activity to x>y in the Expression Editor dialog box, as shown in Figure 28.12:

![](img/e073a4882197be4ab61103cbe0bcb394_1415_0.png)

Figure 28.12: Adding a Condition in the Expression Editor Dialog Box

- 11. Add another WriteLine activity in the Then section of the If activity and set its Text property to x=20 is greater than y=50 (Figure 28.13).
- 12. Add another If activity in the Else section of the If activity and set its Condition property to y>x (Figure 28.13).
- 13. Add two WriteLine activities in the Then and Else sections of the second If activity. Set the Text properties of these WriteLine activities to y=50 is greater than x=20 and x=20 and y=50 are equal numbers. Figure 28.13 shows the final design of the application:

![](img/e073a4882197be4ab61103cbe0bcb394_1415_1.png)

Figure 28.13: Displaying the Design of All Specified Activities

- 14. Press the CTRL+F5 keys combination on the keyboard to run the IfAndVariables application. Figure 28.14 shows the output of the IfAndVariables application:

![](img/e073a4882197be4ab61103cbe0bcb394_1415_2.png)

Figure 28.14: Displaying the Output of the IfAndVariables Application

Now, let’s learn how to create and resume a bookmark.

## Creating and Resuming a Bookmark

In this section, we create a workflow console application, named BookmarkResume (also available on the CD). In this application, we are creating and resuming a bookmark.

Perform the following steps to create the BookmarkResume application:

- 1. Create a workflow console application, BookmarkResume.
- 2. Add the following namespace in the Program.cs file:
- using System.Threading;
- 3. Add the following code snippet in the Main() method of the Program class:

```
Variable<string> name = new Variable<string>
{
    Name = "name"
};

Activity wf = new Sequence
{
    Variables =
    {
        name
    },
    Activities =
    {
        new WriteLine()
        {
            Text = "Enter your name:"
        },
        new ReadLine()
        {
            BookmarkName = "YourName",
            Result = name
        },
        new WriteLine()
        {
            Text = new InArgument<string>((env) => "Hello, " + name.Get(env)+"\nYou are reading C# 2010 Black book")
        }
    }
};

AutoResetEvent syncEvent = new AutoResetEvent(false);

WorkflowApplication wfApp = new WorkflowApplication(wf);

wfApp.Completed = delegate(WorkflowApplicationCompletedEventArgs e)
{
    syncEvent.Set();
};

wfApp.Run();

wfApp.ResumeBookmark("YourName", Console.ReadLine());

syncEvent.WaitOne();
```

In the preceding code snippet, a workflow is created that uses the ReadLine activity to get the input from a user. The ReadLine activity also creates a bookmark, YourName, and waits for the bookmark to be resumed. When the host process collects input data and resumes the bookmark, then the workflow is resumed and the input is displayed on the console.

- 4. Add a ReadLine activity by writing the following code snippet outside the Main() method within the Program class:

```
public sealed class ReadLine : NativeActivity<string>
{
    [RequiredArgument]
    public InArgument<string> BookmarkName { get; set; }

    protected override void Execute(NativeActivityContext context)
    {
        context.CreateBookmark(BookmarkName.Get(context), new BookmarkCallback(OnResumeBookmark));
    }
    protected override bool CanInduceIdle
    {
        get { return true; }
    }
    public void OnResumeBookmark(NativeActivityContext context, Bookmark bookmark, object obj)
    {
        Result.Set(context, (string)obj);
    }
}
```

In the preceding code snippet, a ReadLine activity is created. This ReadLine activity creates an instance of Bookmark class and waits for the bookmark to be resumed. When the Bookmark is resumed, the ReadLine activity assigns the data to the result argument.

- 5. Press the CTRL+F5 keys combination on the keyboard to run the BookmarkResume application. When you run the application, it prompts for your name, as shown in Figure 28.15:

![](img/e073a4882197be4ab61103cbe0bcb394_1417_0.png)

After entering a name, for instance Kabir, it shows the output, as shown in Figure 28.16:

![](img/e073a4882197be4ab61103cbe0bcb394_1417_1.png)

Now, let’s summarize the main topics discussed in this chapter.

## Summary

In this chapter, you have learned about the new features of WF and its components. Next, you have learned about activities and types of workflows. Further, you have learned about built-in and bookmark activities. You have also learned how to handle runtime errors using Try and Throw activities. In the end, you have learned how to host workflows by using different classes.

In the next chapter, you learn about file handling.
