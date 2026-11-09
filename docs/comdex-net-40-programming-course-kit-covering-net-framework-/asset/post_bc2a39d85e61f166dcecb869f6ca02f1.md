
- **Maximized:** Sets the state of the form to the maximized state and as a result covers the entire screen area.

Perform the following steps to set the initial position and state of the form at run time:

1. Open the SETTITLE Windows forms application.
2. Select the form in the designer and change its initial position by setting its **StartPosition** property to an appropriate value in the **Properties** window. In our case, we set the **StartPosition** property to **CenterScreen** (Fig.VB-2.4).
3. Change the initial position of the form by setting its **WindowState** property to an appropriate value in the **Properties** window. In our case, we set the **WindowState** property to **Normal** (Fig.VB-2.4).
4. Press the F5 key on the keyboard to run the application. As a result, the form appears at the center of the screen (Fig.VB-2.5).

![](img/9862a98a1a2d3bb14334137965a1ec60_92_0.png)

Fig.VB-2.4

![](img/9862a98a1a2d3bb14334137965a1ec60_92_1.png)

Fig.VB-2.5

## Hiding the Minimize, Maximize, and Close Buttons

A form has three buttons, **Minimize, Maximize, and Close**, at its top right corner that allow you to minimize, maximize, and close the form. In certain cases, such as while designing a dialog box, you do not need the **Minimize** and **Maximize** buttons. In such a situation, you can prevent these buttons from displaying on the form. You can hide the **Minimize** button or **Maximize** button by setting the **MinimizeBox** property or **MaximizeBox** property, respectively, of the form to **False**. You can also hide all the three buttons, **Minimize, Maximize, and Close**, by setting the **ControlBox** property of the form to **False**.

Perform the following steps to hide the Minimize and Maximize buttons of a form:

1. Open the SETTITLE Windows forms application.
2. Select the form in the designer and set its **MaximizeBox** property to **False** in the **Properties** window (Fig.VB-2.6).
3. Set the **MinimizeBox** property of the form to **False** in the **Properties** window (Fig.VB-2.6).
4. Press the F5 key on the keyboard to run the application. The output is displayed (Fig.VB-2.7).

![](img/9862a98a1a2d3bb14334137965a1ec60_92_2.png)

Fig.VB-2.6

![](img/9862a98a1a2d3bb14334137965a1ec60_92_3.png)

Fig.VB-2.7

## Adding Controls to a Form

You can design the user interface of your Windows forms application by adding controls to the forms included in the application. Controls have in-built functionality and they help you to design a functionality-rich and user-friendly interface for your application. You can add controls to a form from the Toolbox. You can add a number of controls, such as **Label**, **Button**, **TextBox**, **ListBox**, **RadioButton**, and **PictureBox**, from the **Toolbox** to a form.

Perform the following steps to add controls to a form:

1. *Start* Visual Studio 2010.
2. *Select* **File→New→Project** from the menu bar. The **New Project** dialog box opens.
3. *Select* **Visual Basic→Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box.
4. *Select* **Windows Forms Application** in the middle pane to create a Windows forms application.
5. Enter the name of the application as **ADDINGCONTROLS** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** combo box.
6. *Click* the **OK** button to close the **New Project** dialog box. As a result, the **ADDINGCONTROLS** application is created (Fig.VB-2.8).
7. *Drag* and drop a **Label** control from the **Toolbox** on the form (Fig.VB-2.9).

![](img/9862a98a1a2d3bb14334137965a1ec60_93_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_93_1.png)

Fig.VB-2.8　　　　　　　　　　　　　　　　Fig.VB-2.9

8. *Drag* and drop a **TextBox** control and a **Button** control on the form from the **Toolbox**, as shown in Fig.VB-2.10:

![](img/9862a98a1a2d3bb14334137965a1ec60_93_2.png)

Fig.VB-2.10

9. *Press* the **F5** key on the keyboard to run the application. As a result, the output is displayed, as shown in Fig.VB-2.11:

![](img/9862a98a1a2d3bb14334137965a1ec60_94_0.png)

Let’s now learn to set the tab order of controls.

### Setting the Tab Order of Controls

You can make the controls present on a form to be navigated at run time by setting the tab order of the controls. The tab order of a control can be set by setting its **TabIndex** property to an integer value, such as 0, 1, 4, or 8, at either design time or run time. After setting the tab order of the controls present on a form, you can navigate through controls at run time by pressing the **TAB** key on the keyboard. While setting the tab order of a set of controls, you need to ensure that the **TabStop** property of each control is set to **True**. If the **TabStop** property of a control is **False**, then you cannot access the control at run time by pressing the **TAB** key.

Perform the following steps to set the tab order of controls present on a form:

1. Open the **ADDINGCONTROLS** application.
2. Select the **TextBox** control on the form and set its **TabIndex** property to 0 in the **Properties** window (Fig.VB-2.12).
3. Select the **Button** control on the form and set its **TabIndex** property to 1 in the **Properties** window, as shown in Fig.VB-2.13.

![](img/9862a98a1a2d3bb14334137965a1ec60_94_1.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_94_2.png)

4. Press the **F5** key on the keyboard to run the application. The output is displayed with the focus on the text box (Fig.VB-2.14).
5. Press the **TAB** key. The button gets focus, as shown in Fig.VB-2.15:

![](img/9862a98a1a2d3bb14334137965a1ec60_94_3.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_94_4.png)

As you enlarge the form, the **Button** control also enlarges in the same proportion, as shown in Fig.VB-2.20:

![](img/9862a98a1a2d3bb14334137965a1ec60_96_0.png)

Fig.VB-2.20

## Adding Forms to a Windows Forms Application

Suppose, you have to create a Windows forms application with an introductory form to welcome the user, a data entry form to get data from the user, and a summary form to display the data analysis results. To create such an application, you need to add more forms to your application in addition to the form that is by default created with your Windows forms application. First of all, you need to create a Windows forms application, then add one more form to the application, and then see how to access data of one form from another form.

Perform the following steps to add one more form to a Windows forms application:

1. *Start* Visual Studio 2010.
2. *Select* File→New→Project from the menu bar. The **New Project** dialog box opens.
3. *Select* *Visual Basic→Windows* from the *Installed Templates* section in the left pane of the **New Project** dialog box.
4. *Select* *Windows Forms Application* in the middle pane to create a Windows forms application.
5. *Enter* the name of the application as MULTIPLEFORMS (also available on the CD) in the *Name* text box and an appropriate location for the application in the *Location* combo box.
6. *Click* the OK button to close the **New Project** dialog box. The MULTIPLEFORMS application is created, displaying only one form, Form1 (Fig.VB-2.21).
7. *Add* a **Label** control, a **TextBox** control, and a **Button** control to the form from the Toolbox and position them (Fig.VB-2.22).

![](img/9862a98a1a2d3bb14334137965a1ec60_96_1.png)

Fig.VB-2.21

![](img/9862a98a1a2d3bb14334137965a1ec60_96_2.png)

Fig.VB-2.22

8. Set the **Text** property of the **Label** control and the **Button** control to **Enter some text** and **Show Text**, respectively, by using the **Properties** window (Fig.VB-2.23).
9. Select **Project→Add Windows Form** from the menu bar to add one more form to the current project of the Windows forms application (Fig.VB-2.24).

![](img/9862a98a1a2d3bb14334137965a1ec60_97_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_97_1.png)

The **Add New Item** dialog box opens (Fig.VB-2.25). You can notice that **Windows Form** template is already selected in the middle pane of the **Add New Item** dialog box and **Form2.vb** is displayed in the **Name** text box.

10. Click the **Add** button to add the **Form2.vb** form to the application, as shown in Fig.VB-2.25:

![](img/9862a98a1a2d3bb14334137965a1ec60_97_2.png)

A new form, named **Form2**, is added to the current project in the application (Fig.VB-2.26).

11. Add a **TextBox** control to **Form2** and resize it (Fig.VB-2.27).

![](img/9862a98a1a2d3bb14334137965a1ec60_97_3.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_97_4.png)
