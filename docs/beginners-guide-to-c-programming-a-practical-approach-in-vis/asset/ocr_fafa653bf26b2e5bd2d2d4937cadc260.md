![](bbox=[0.3, 0.12, 0.67, 0.45])

Figure 6.42. The contents of test.txt file read and displayed in our program

It is worth noting that we can read all file types with OpenFileDialog using various file reading methods as we will see in the following chapters after learning more about C# programming.

# 6.2.5. SaveFileDialog

SaveFileDialog works similar to the OpenFileDialog but doing the opposite job: saving data to a file. Let’s use a SaveFileDialog in a project and save the text entered in a RichTextBox to a file:

+   1. Create a C# project in Visual Studio.
+   2. Add a SaveFileDialog on the form. It will appear in the pane below the form. Set the Name property of the SaveFileDialog as textSaveFileDialog as shown in Figure 6.43.
+   3. Add a Button and a TextBox to the project as in Figure 6.43.
+   4. Set the Name and Text of the Button as saveButton and Click to save to a file...
+   5. Set the Name of the RichTextBox as inputRichTextBox. After these settings, the form should look as shown in Figure 6.44.
+   6. When the Button’s clicked, the SaveFileDialog window will appear. Therefore, double-click the Button on the form to generate its default event handler method as in Code 6.16.