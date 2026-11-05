# Events and method calls

In C# an event is delivered to an object by means of a call to a method in that object. In this respect you can regard an event and a message as the same thing. From the point of view of our name editing form we would like to have a particular method called when the "Finished" button is pressed by the user. This method would validate the new name, store it if it was OK and then close down the edit form.

# Button Events

To get back to the problem we are solving: when the user clicks on the button on our form this is registered by the Windows operating system and then passed into the form as an event. The form decides which of the components on the form should be given the event and calls a method in that component to tell it "you've been pressed". The button then does its animation so that it moves in and out. Then it looks for people to tell about the event. The button keeps a list of people to tell about events. The list is actually a list of delegates.

So, to get a button to run a method of ours we need to create a delegate object and then pass that to the button so that it knows to use it when the event occurs. A delegate is an object which can be used to represent a particular method in an instance of a class. In the case of our button, the delegate is going to represent the method that we want to have called when the button is pressed. We pass the button a reference to this delegate and it can then call the method it represents when the button is pressed.

The good news is that creating a delegate instance for a windows component is such a common task that the forms library has provided a delegate class which does this for us. We just need to create an instance of this class to get a delegate to give to the button.

The signature of the method that is called when the event occurs is the same for every kind of event, from mouse movement, to button press, to window closing, so we can use this class every time we need to create a delegate. The actual code to create a delegate and assign it to a method is as follows:

```
using System.Windows.Forms;
using System.Drawing;
using System;

class FormsDemo
{
    public static void Main()
    {
        Form f = new Form();
        Label nameLabel = new Label();
        nameLabel.Text = "Name:";
        nameLabel.Top=50;
        nameLabel.Left=0;
        f.Controls.Add(nameLabel);

        TextBox nameTextBox = new TextBox();
        nameTextBox.Top=50;
        nameTextBox.Left=100;
        nameTextBox.Text = "Rob";
        f.Controls.Add(nameTextBox);

        Button finishButton = new Button();
        finishButton.Top=80;
        finishButton.Left=100;
        finishButton.Text="Finished";
        finishButton.Click +=
            new EventHandler(finishButtonClick);
        f.Controls.Add(finishButton);

        f.ShowDialog();
    }
}
```