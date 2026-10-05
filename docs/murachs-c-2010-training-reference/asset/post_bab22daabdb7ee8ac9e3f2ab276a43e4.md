
# An introduction to inheritance

Inheritance allows you to create a class that's based on another class. When used correctly, inheritance can simplify the overall design of an application. The following topics present an introduction to the basic concepts of inheritance. You need to understand these concepts before you learn how to write the code needed to implement classes that use inheritance.

# How inheritance works

Figure 14-1 illustrates how inheritance works. When inheritance is used, a derived class inherits the properties, methods, and other members of a base class. The objects that are created from the derived class can use these inherited members. The derived class can also provide its own members that extend the base class. In addition, the derived class can also override properties and methods of the base class by providing replacement definitions for them.

The two classes shown in this figure illustrate how this works. Here, the base class is System.Windows.Forms.Form, the .NET class that all Windows forms inherit. As this figure shows, this class has several properties and methods, such as the Text property and the Close method. (This class has many more properties and methods. I included just a few representative ones.)

The derived class in this figure is the class for the New Product form in the Product Maintenance application (ProductMaintenance.frmNewProduct). As you can see, groups of members are listed for this class. The first group includes the properties and methods that the class inherits from its base class. The second group includes the members that have been added to the derived class. In this case, the derived class includes five new properties (the text box and button controls) and one new method (GetProduct).

Although this figure doesn't show it, a derived class can also replace an inherited property or method with its own version of the property or method. You'll learn how this works later in this chapter.

# How inheritance works

| System.Windows.Forms.Form | Public properties and methods |
| :--- | :--- |
| Base class | string Text |
| bool MinimizeBox | |
| bool MinimizeBox | |
| void Close() | |
| void Show() | |
| DialogResult ShowDialog() | |
| ProductMaintenance.frmNewProduct | |
| Derived class | string Text |
| bool MinimizeBox | |
| bool MinimizeBox | |
| void Close() | |
| void Show() | |
| DialogResult ShowDialog() | |
| void Close() | Inherited properties and methods |
| void Show() | |
| DialogResult ShowDialog() | |
| TextBox txtCode | Added properties and methods |
| TextBox txtDescription | |
| TextBox txtPrice | |
| Button btnSave | |
| Button btnClose | |
| Product GetNewProduct() | |

# Description

- Inheritance lets you create a new class based on an existing class. Then, the new class inherits the properties, methods, and other members of the existing class.
- A class that inherits from an existing class is called a *derived class, child class,* or *subclass*. A class that another class inherits is called a *base class, parent class,* or *superclass*.
- A derived class can *extend* the base class by adding new properties, methods, or other members to the base class. It can also replace a member from the base class with its own version of the member. Depending on how that's done, this is called *hiding* or *overriding*.
- When you create a new form in C#, the form inherits the .NET Framework class named System.Windows.Forms.Form. As a result, all C# forms inherit the members defined by this base class. Then, as you add controls and code to the form, you extend the base class by creating new properties and methods.

Figure 14-1 Inheritance works

# How the .NET Framework uses inheritance

14-2 shows that inheritance is used extensively throughout the .NET Framework. This figure shows a portion of the inheritance hierarchy that's used by several of the Windows form controls in the System.Windows.Forms namespace.

The Control class provides features that are common to all Windows form controls. For example, the Control class provides properties such as Visible and Enabled that indicate whether a control is visible and enabled, a Text property that specifies the text associated with a control, as well as properties that specify a control's display location. The Control class also provides the Focus method, which lets you move to a control. Because these features are provided by the Control class, they are available to all Windows form controls.

The shaded classes in this figure are nine of the form control classes you've learned about in this book. Note that all of these are derived directly or indirectly from the Control class. For example, the GroupBox and Label controls inherit the Control class directly. However, the other controls inherit that that are derived from the Control class.

The Button, CheckBox, and RadioButton controls, for example, all inherit the ButtonBase class. This class provides features that are common to all types of button controls. For example, the Image property of this class lets you display an image on a control.

Similarly, combo boxes and list boxes have common features that are provided by the ListControl class. The most important of these are the Items property, which provides the list's displayed by the control, and the SelectedIndex, SelectedValue, and SelectedItem properties, which let you access the item's selected in the list.

Likewise, the TextBoxBase class provides features that are common to text box controls. That includes the MultiLine property that lets you display multiple lines and the ReadOnly property that lets you create read-only boxes. By the way, if you are wondering why an intermediate TextBoxBase class is used in the TextBox hierarchy, it's because the .NET Framework provides a second type of text box, called a RichTextBox, which also inherits TextBoxBase. Because the RichTextBox control isn't covered in this book, however, I didn't include it in this figure.

You may be surprised to learn that the Form class itself is also derived from two other classes: ContainerControl and ScrollControl. A form's ability to contain is provided by ContainerControl. And the form's ability to scroll all at once is provided by ScrollControl class.

Don't be dismayed by the amount of detail presented in this figure. In fact, the inheritance hierarchy for System.Windows.Forms is far more complicated. The intent of this figure is simply to illustrate

# The inheritance hierarchy for form controls

| System namespace | System.Windows.Forms |
| :--- | :--- |
| Object | Control |
| ButtonBase | Button |
| CheckBox | |
| RadioButton | |
| ListControl | ListBox |
| ComboBox | |
| TextBoxBase | TextBox |
| ScrollControl | Form |
| ContainerControl | |

# Description

- The .NET Framework uses inheritance extensively in its controls. For example, inheritance is used throughout System.Windows.Forms.
- All of controls are derived from a base class. This class provides properties and methods that all have, such as Tag and Text.
- Some controls have an additional layer of inheritance. For example, the inheritance hierarchy for ComboBox.
- The fully qualified name of a class includes the name of the namespace that belongs to.

Figure 14-2 Inheritance works

# Methods inherited from the System.Object class

Every class implicitly inherits the System.Object class. In other words, the System.Object class is the base class for every class, including user-defined classes. This means that all classes inherit the methods that are defined for System.Object class. These methods are summarized in figure 14-3. I'll describe the GetType method later in this chapter, and I'll describe each of the other methods.

Although the methods of the.Object class are available to every class, a derived class can provide its own implementation of one or more of these methods. As a result, these methods may work differently from class to class.

For example, the default implementation of the ToString method returns the fully qualified name of the object's type. Because that's not very useful, it's common to override the ToString method to provide a more useful representation. For example, a Customer class might override the ToString method so it returns the customer's name.

As you learned in chapter 13, the Equals and GetHashCode methods are often used to provide a way to compare objects using values rather than instance references. Notice also that the Object class has a static ReferenceEquals method that provides the same function as the static Equals method. The ReferenceEquals method lets you test two objects for reference equality even if the class overrides the Equals method.

Unlike C++ and other languages that require you to manage memory, C# uses a mechanism known as garbage collection that determines when the system is running low on memory. And when the system is idle, it frees the memory for any objects that don't have any more references to them. Before it does that, though, calls the Finalize method for each of those objects, even though the default implementation of this method doesn't do anything.

The last method shown in this figure is MemberwiseClone. You can use this method to create a simple copy of an object that doesn't expose other objects as properties or fields. You'll learn more about cloning objects in the next chapter.
