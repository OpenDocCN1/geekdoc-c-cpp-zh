# HANDLING THE RETURN KEY OF THE KEYBOARD

Earlier, you saw how you can connect an IBAction with the Did End On Exit event of a TextField view to hide the keyboard when the user taps the Return key. Alternatively, you can also implement the textFieldShouldReturn: method (defined in the UITextFieldDelegate protocol). This method is invoked whenever the user taps the Return key on the keyboard:

```
- (BOOL) textFieldShouldReturn:(UITextField *) textFieldView {
    if (textFieldView == textField) {
        [textField resignFirstResponder];
    }
    return NO;
}
```

# SUMMARY

In this chapter, you learned the various techniques to deal with the keyboard in your iPad application. In particular, this chapter showed you how to make the keyboard go away when you are done with the data entry, how to detect the presence or absence of the keyboard, and how to ensure that views are not blocked by the keyboard.

# EXERCISES

+   1. How do you hide the keyboard for a UITextField object?
+   2. How do you detect whether the keyboard is visible or not?
+   3. How do you get the size of the keyboard?

Answers to the Exercises can be found in Appendix A.