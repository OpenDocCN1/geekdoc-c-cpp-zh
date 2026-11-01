# WHAT YOU LEARNED IN THIS CHAPTER

| TOPIC | KEY CONCEPTS |
|---|---|
| Making the keyboard go away | Use the `resignFirstResponder` method on a `UITextField` object to resign its First-Responder status. |
| Displaying the different types of keyboard displayed | Modify the keyboard type by changing the Text Input Traits of a `UITextField` object in the Attributes Inspector window. |
| Handling the return key of the keyboard | You either handle the Did End on Exit event of a `UITextField` object, or implement the `textFieldShouldReturn:` method in your view controller (remember to ensure that your view controller class is the delegate for the `UITextField` object). |
| Detecting when the keyboard appears or hides | Register for the two notifications — `UIKeyboardWillShowNotification` and `UIKeyboardWillHideNotification`. |
| Detecting which `UITextField` object has started editing | Implement the `textFieldDidBeginEditing:` method in your view controller. |
| Detecting which `UITextField` object has ended editing | Implement the `textFieldDidEndEditing:` method in your view controller. |