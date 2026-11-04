# 10

# Building Custom Dialogs

The standard dialogs described in Lesson 8 make it easy to perform typical chores such as picking files, folders, colors, and fonts. Those dialogs can get you pretty far, but sometimes you may want a dialog that is customized for your application.

For example, you might want to display a dialog where the user can enter a new customer's contact information (name, address, phone number, and hat size). It's unlikely that any predefined standard dialog could ever handle that situation.

Fortunately, it's easy to build custom dialogs. All you need to do is build a new form as described in Lesson 9, add a few buttons, and set a few properties.

In this lesson you learn how to build custom dialogs and make them as easy to use as the standard dialogs that come with C#.

# MAKING CUSTOM DIALOGS

Building a custom dialog is pretty easy. Simply add a new form to your project as described in Lesson 9 and give it whatever controls you need.

To allow the user to finish using the dialog, add one or more buttons. Some dialogs have a single OK button. Others have OK and Cancel buttons or some other combination of buttons. Because you're creating the dialog, you can give it whatever buttons you like.

By convention, the buttons should go in the dialog's lower-right corner. Figure 10-1 shows a very simple dialog that contains a single textbox where the user can enter a name.

![](bbox=[0.65, 0.7, 0.9, 0.85])

FIGURE 10-1

To make using the dialog easier, you can set the form's AcceptButton and CancelButton properties. These determine which button is triggered if the user presses Enter and Esc, respectively. Typically the AcceptButton triggers the dialog's OK or Yes button and the CancelButton triggers the Cancel or No button.