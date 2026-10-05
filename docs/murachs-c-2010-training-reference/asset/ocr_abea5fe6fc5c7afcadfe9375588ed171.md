# The property settings

Figure 10-16 presents the property settings for the Customer and Payment forms and their controls. In the Customer form, the AutoSize property of the label that displays the payment method has been set to false. This allows you to use the Form Designer to size the label.

In the Payment form, the properties have been set so the form looks and acts like a dialog box. In addition, the DropDownStyle for the two combo boxes have been set to DropDownList the user must select an item from the list. Finally, the DialogResult property of the Cancel button has set to Cancel, which happens automatically when the CancelButton property of the form is set to the Cancel button.

# The code for the Customer form

Figure 10-17 presents the code for the Customer form. After the code that Visual Studio has generated for the form, a Boolean variable named isSaved is declared and set to true. This variable indicates whether the data's currently displayed in the form has been saved. It's set to false any the data in the Customer Name combo box or the Payment label changes. To accomplish that, the SelectedChanged event of the combo box and the TextChanged event of the label are wired to the DataChanged method.

When the Customer form is loaded, the event handler for the Load event adds two names to the Customer Name combo box. In a production application, of course, the combo box would include many more names, and they would be loaded from a file or database. But for the purposes of this chapter, two names are sufficient.

When the user clicks the Select Payment button, the Click event handler for that button displays the Payment form as a dialog box. Then, if the user clicks the OK button in dialog box, the payment is displayed in the Payment Method label on the Customer form. As you can see, this data is stored in the Tag property of the Payment form.

If the user clicks the Save button, the Click event handler for that button calls the IsValidData method shown on page 2 of this listing. Method checks that the user has selected a customer and entered a payment. If so, the event handler for the Click event of the Save button calls the SaveData method. This method sets the SetSelectedIndex property of the Customer Name combo box to -1 so no customer is selected, and it clears the Payment Method label. Then, it sets the isSaved variable to true and moves the focus to the combo box. In a production application, this data would be saved to a file or database.

The last method is executed when the user tries to close the Customer form. This is the same method you saw in figure 10-14, so you shouldn't have any trouble understanding how it works.