# How to add navigation features

Windows forms have features that make it easier for users to move around in the forms without using the mouse. These navigation features are described in figure 2-7.

The *tab order* is the order in which the controls on a form receive the *focus* when the user presses the Tab key. The tab order should usually be set so the focus moves left-to-right and top-to-bottom, beginning at the top left of the form and ending at the bottom right. However, in some cases you’ll want to deviate from that order. For example, if you have controls arranged in columns, you may want the tab order to move down each column.

The tab order is initially set based on the order in which you add controls to the form. So if you add the controls in the right order, you won’t need to alter the tab order. But if you do need to change the tab order, you can do so by adjusting the TabIndex property settings. The TabIndex property is simply a number that represents the control’s position in the tab order, beginning with zero. So, the first control in the tab order has a TabIndex of 0, the second control’s TabIndex is 1, and so on.

*Access keys* are shortcut keys that let the user move the focus directly to a control. You set a control’s access key by using the Text property. Just precede the letter in the Text property value that you want to use as the access key with an ampersand (&). Then, the user can move the focus to the control by pressing Alt plus the access key.

If you assign an access key to a control that can’t receive the focus, such as a label control, pressing the access key causes the focus to move to the next control in the tab order that can receive the focus. As a result, you can use an access key with a label control to create a shortcut for a text box control, which can’t have an access key.

If you assign an access key to a button control, you should know that pressing Alt plus the access key doesn’t simply move the focus to the control. Instead, it activates the control just as if it was clicked. Without an access key, a user would have to tab to the button control and then press the Enter key to activate it using the keyboard. The exception is if the button is selected for the AcceptButton or CancelButton property for the form.

The AcceptButton and CancelButton properties specify the buttons that are activated when the user presses the Enter and Esc keys. That can make it easier for a user to work with a form. If, for example, the AcceptButton property of the Invoice Total form in figure 2-3 is set to the Calculate button, the user can press the Enter key after entering a subtotal instead of using the mouse to click the Calculate button or using the access key to activate it.