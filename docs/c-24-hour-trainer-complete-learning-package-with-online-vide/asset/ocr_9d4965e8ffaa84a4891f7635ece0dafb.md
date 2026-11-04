For example, the following code creates a NewUserForm and displays it:

```
    NewUserForm userForm;
    userForm = new NewUserForm();
    userForm.ShowDialog();
```

The first statement declares a variable of type NewUserForm. Initially that variable doesn't refer to anything so if you tried to display the form at this point, the program would crash.

The second statement creates a new instance of the NewUserForm type and saves a reference to the new form in the userForm variable.

Now the variable refers to an instance of the NewUserForm type, so the third statement can safely display that form.

# ## Value Types

In contrast to reference types, a *value type* actually contains its data instead of refers to it. Many of the primitive data types such as int, double, and decimal are value types.

The following code creates and uses a variable with the Address structure type described earlier:

```
    Address homeAddress;
    homeAddress.Name = "Benjamin";
```

When the code executes the first statement, the program creates the Address structure so it's all ready to go, although its fields all contain null values. The second statement can immediately set the variable's Name value without needing to use the new keyword to create a new instance of the structure.

# ## Other Differences

Another important difference between value and reference types involves the way the program assigns values to them.

If a program sets one reference variable equal to another, then they both point to *the same object*. For example, suppose ann and ben are two variables that hold references to Student objects. Then the statement ben = ann makes the variable ben refer to the same object to which ann refers.

Figure 17-1 shows this operation graphically. Initially (the picture on the left) variable ann contains a reference to a Student object and variable ben contains the special value null (represented by the box with an X in it) that means it doesn't refer to anything. After executing the statement ben = ann, both variables contain references to the same Student object (the picture on the right).

![](bbox=[0.21, 0.7, 0.704, 0.8])

**FIGURE 17-1**