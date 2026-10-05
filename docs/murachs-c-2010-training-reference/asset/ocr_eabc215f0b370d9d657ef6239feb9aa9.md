# How to work with multi-form projects

In previous chapters, you learned how to create applications that consist of a single form. However, most Windows applications use two or more forms. In the topics that follow, you'll learn the basic skills for creating applications that consist of two or more forms. In particular, you'll learn how to create an application that consists of a main form and one or more forms that are displayed as dialog boxes.

# How to add a form to a project

When you start a new project for a Windows application, it consists of a single blank form. To add another form to the project, you use the Add New Item dialog box shown in figure 10-7. From this dialog box, you select the Windows Form template and then enter the name of the new form. When you click the Add button, the new form is created with the name you specify.

You can also add an existing form to a project using the Add Existing Item dialog box. This can be useful if you want to use the same form in two different projects or if you want to create a form that's similar to an existing form. Note that when you add an existing form from another project, form is copied into the new project. That way, any changes you make to the form won't be applied to the original form, which is typically what you want.

Also note that a form you add from another project is typically in a different namespace for the forms in the current project. Because of that, you'll usually change the namespace for the form so it's the same as the namespace for the other forms. Alternatively, you can add a using statement for the form's namespace each form that refers to it.