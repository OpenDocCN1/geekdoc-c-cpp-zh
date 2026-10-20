
+   1. In the project dialog box, we can see various options for creating different types of projects in Visual Studio. Click the Windows option on the left-hand side.
+   2. When we click the Windows options in the previous step, we will be able to see an option for Windows Forms Application. Click this option.
+   3. We will give a name for the application. In our case, it is demoapplication. We will also provide a location to store our application.
+   4. Finally, we click the ‘OK’ button to let Visual Studio create our project.

If the above steps are followed, you will get the below output in Visual Studio.

Output:-

![](img/e7ca4af023a4148a909dd82c11f81893_174_0.png)

You will see a Form Designer displayed in Visual Studio. It's in this Form Designer that you will start building your Windows Forms application.

![](img/e7ca4af023a4148a909dd82c11f81893_175_0.png)

In the Solution Explorer, you will also be able to see the demoapplication Solution. This solution will contain the below 2 project files

+   1. A Form application called Forms1.cs. This file will contain all of the code for the Windows Form application.
+   2. The Main program called Program.cs is default code file which is created when a new application is created in Visual Studio. This code will contain the startup code for the application as a whole.

On the left-hand side of Visual Studio, you will also see a toolbox. The toolbox contains all the controls which can

be added to a Windows Forms. Controls like a text box or a label are just some of the controls which can be added to a Windows Forms.

Below is a screenshot of how the Toolbox looks like.

![](img/e7ca4af023a4148a909dd82c11f81893_176_0.png)

Step 3) In this step, we will now add a label to the Form which will display "Hello World." From the toolbox, you will need to choose the Label control and simply drag it onto the Form.

![](img/e7ca4af023a4148a909dd82c11f81893_177_0.png)

Once you drag the label to the form, you can see the label embedded on the form as shown below.

![](img/e7ca4af023a4148a909dd82c11f81893_177_1.png)

Step 4) The next step is to go to the properties of the control and Change the text to ‘Hello World’.

To go to the properties of a control, you need to right-click the control and choose the Properties menu option

![](img/e7ca4af023a4148a909dd82c11f81893_178_0.png)

+   - The properties panel also shows up in Visual Studio. So for the label control, in the properties control, go to the Text section and enter “Hello World”.
+   - Each Control has a set of properties which describe the control.

![](img/e7ca4af023a4148a909dd82c11f81893_179_0.png)

If you follow all of the above steps and run your program in Visual Studio, you will get the following output

Output:-

![](img/e7ca4af023a4148a909dd82c11f81893_179_1.png)

## 4.1.2 Adding Controls to a form

We had already seen how to add a control to a form when we added the label control in the earlier section to display “Hello World.”

Let’s look at the other controls available for Windows forms and see some of their common properties. In our Windows form application in C# Example:s, we will create one form which will have the following functionality.

+   1. The ability for the user to enter name and address.
+   2. An option to choose the city in which the user resides in
+   3. The ability for the user to enter an option for the gender.
+   4. An option to choose a course which the user wants to learn. There will make choices for both C# and ASP.Net

So let’s look at each control in detail and add them to build the form with the above-mentioned functionality.

## 4.1.3 Group Box

A group box is used for logical grouping controls into a section. Let’s take an Example: if you had a collection of controls for entering details such as name and address of a person. Ideally, these are details of a person, so you would want to have these details in a separate section on the Form. For this purpose, you can have a group box.

Let’s see how we can implement this with an Example: shown below

Step 1) The first step is to drag the Groupbox control onto the Windows Form from the toolbox as shown below

![](img/e7ca4af023a4148a909dd82c11f81893_181_0.png)

Step 2) Once the groupbox has been added, go to the properties window by clicking on the groupbox control. In the properties window, go to the Text property and change it to “User Details”.

Once you make the above changes, you will see the following output

Output:-

![](img/e7ca4af023a4148a909dd82c11f81893_182_0.png)

![](img/e7ca4af023a4148a909dd82c11f81893_182_1.png)

In the output, you can clearly see that the Groupbox was added to the form. You can also see that the text of the groupbox was changed to “User Details.”

## 4.1.4 Label Control

Next comes the Label Control. The label control is used to display a text or a message to the user on the form. The label control is normally used along with other controls. Common Examples are wherein a label is added along with the textbox control. The label indicates to the user on what is expected to fill up in the textbox. Let’s see how we can implement this with an Example: shown below. We will add 2 labels, one which will be called ‘name’ and the other called ‘address.’ They will be used in conjunction with the textbox controls which will be added in the later section.

**Step 1)** The first step is to drag the label control on to the Windows Form from the toolbox as shown below. Make sure you drag the label control 2 times so that you can have one for the ‘name’ and the other for the ‘address’.

![](img/e7ca4af023a4148a909dd82c11f81893_184_0.png)

Step 2) Once the label has been added, go to the properties window by clicking on the label control. In the properties window, go to the Text property of each label control.

![](img/e7ca4af023a4148a909dd82c11f81893_185_0.png)

Once you make the above changes, you will see the following output

Output:-

![](img/e7ca4af023a4148a909dd82c11f81893_186_0.png)

You can see the label controls added to the form.

## 4.1.5 Textbox

A textbox is used for allowing a user to enter some text on the Windows application in C#. Let’s see how we can implement this with an Example: shown below. We will add 2 textboxes to the form, one for the Name and the other for the address to be entered for the user

**Step 1)** The first step is to drag the textbox control onto the Windows Form from the toolbox as shown below

![](img/e7ca4af023a4148a909dd82c11f81893_187_0.png)

Step 2) Once the text boxes have been added, go to the properties window by clicking on the textbox control. In the properties window, go to the Name property and add a meaningful name to each textbox. For Example:, name the textbox for the user as txtname and that for the address as txtaddress. A naming convention and standard should be made for controls because it becomes easier to add extra functionality to these controls, which we will see later on.

![](img/e7ca4af023a4148a909dd82c11f81893_188_0.png)

In the output, you can clearly see that the Textboxes was added to the form.

## 4.1.6 List box

A Listbox is used to showcase a list of items on the Windows form. Let’s see how we can implement this with an Example: shown below. We will add a list box to the form to store some city locations.

Step 1) The first step is to drag the list box control onto the Windows Form from the toolbox as shown below

Step 2) Once the list box has been added, go to the properties window by clicking on the list box control.

![](img/e7ca4af023a4148a909dd82c11f81893_189_0.png)

![](img/e7ca4af023a4148a909dd82c11f81893_189_1.png)

+   1. First, change the property of the Listbox box control, in our case, we have changed this to lstcity
+   2. Click on the Items property. This will allow you to add different items which can show up in the list
