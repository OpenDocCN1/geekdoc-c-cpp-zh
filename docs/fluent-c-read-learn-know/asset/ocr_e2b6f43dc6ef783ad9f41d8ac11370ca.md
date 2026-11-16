# THE LISTBOX AND COMBOBOX

The ListBox and ComboBox controls are two of the most commonly used items controls. They both descend from the Selector class, which adds properties that allow the user to select items in the control.

![](bbox=[0.1, 0.25, 0.9, 0.6])

We'll talk about the difference between SelectedItem (the actual item the user chose) and SelectedValue (the value of a specified property associated with the SelectedItem) when we look at WPF binding in Chapter 22.

Because ListBoxItem descends from ContentControl, not ItemsControl, you set the Content property, not the Header.

The ListBox and ComboBox also define distinct types for their item collection. As you can see, ComboBoxItem inherits from ListBoxItem.

# PUT ON YOUR THINKING HAT

We've been working in XAML a lot in this chapter, so let's do something in C#. Can you write an application that displays a ListBox with three or four items, selects the second item in the list when the Window is loaded, and then displays the SelectedIndex in a MessageBox when the user chooses something else? (Hint: You'll need to add an event handler. Do you remember how to do that from the Properties window?) When you run the application, it will display the MessageBox twice. Do you know why?