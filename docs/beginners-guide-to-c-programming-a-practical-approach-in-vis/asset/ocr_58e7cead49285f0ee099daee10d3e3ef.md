will be displayed when an object is created from this class using one of these constructor methods.

8. Let’s return to the form and then double-click the Button to create its click event. We'll take the Texts entered in the TextBoxes and use them in constructor methods for creating two different objects as follows:

```
```csharp
private void showButton_Click(object sender, EventArgs e)
{
    string input1Text = input1.Text;
    string input2Text = input2.Text;
    ShowText object1 = new ShowText(input1Text);
    ShowText object2 = new ShowText(input1Text, input2Text);
}
```
```

Code 12.18

The constructor method with single parameter is utilized when creating object1 and the constructor method with double parameter is used for creating object2. Therefore, the respective code lines in these constructors (Code 12.17) will be executed one after another.

9. Build and run the project. The program will be shown as follows:

![](bbox=[0.22, 0.7, 0.68, 0.88])

Figure 12.16. The program window

When we enter two strings to the TextBoxes and click the Show Button, object1 and object2 will be created using the two constructor methods we declared inside the class block. Then, the respective message boxes will be displayed in order during the creation of the objects as shown in Figure 12.17 and 12.18.