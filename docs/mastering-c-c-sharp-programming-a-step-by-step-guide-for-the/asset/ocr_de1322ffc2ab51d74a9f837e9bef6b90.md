# SimpleForm Application

Windows Form projects are far easier to debug than console applications. All Windows Form projects are classed as event-driven because they will respond to specified events, and that makes it much easier to look at their behavior in the debugger. To do this, you just put a breakpoint inside one of the event handlers.

# Adding a New Form to a Project

Most of the time, your Windows Forms projects will have more than one form. Most have several that are used to handle all the different parts of the applications and generally, a new form is nothing more than a class that descends from the base class of System.Windows.Forms.Form.

You can add new forms in two ways — click on the Project Window and then click on Add New Form, or go to Solution Explorer and right-click on the project name; click on Add Windows Form from the menu. Both ways will open a dialog box to Add New Item.

To add the form, just type in a name for the new class and click on the Open button. The new form class gets created by .Net and added to your project. Any forms that you add to your project will automatically have the Dispose method in them along with a method called InitializeComponent that the Forms Designer uses.

# Modal Forms vs. Modeless Forms

Forms can be displayed to users in two different ways:

+   - **Modal Forms** – this type of form will not allow any other part of the application to be accessed while it is being displayed. This form is useful when your dialog box contains information that a user must accept or acknowledge before they can move on.
+   - **Modeless Forms** – this type of form will allow access to other parts of the application while being displayed. This form is useful when you want a form that can be used over a period of time.