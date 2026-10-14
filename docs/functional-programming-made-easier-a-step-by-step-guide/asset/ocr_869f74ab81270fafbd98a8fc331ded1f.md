be good for us to see how to develop such a Component and how it will interact with our Page.

Now that we have a plan we’re ready to complete the Logon Page.

The next thing we’ll need to do to is keep track of the data in the fields in our State so that we have the values once the user clicks the Logon Button.

This is normally done with onChange, which is fired when the user exits a field and that field has been modified. But we’re going to want to check on every change. For that, we’re going to want to use onValueInput.

Add an Action called Input and then add onValueInput from Halogen.HTML.Events to both the Username and Password fields to trigger that new Action. Use the code for HE.onClick in this file as reference along with Pursuit.

Return here when you’re ready to move on.

Here are those changes: