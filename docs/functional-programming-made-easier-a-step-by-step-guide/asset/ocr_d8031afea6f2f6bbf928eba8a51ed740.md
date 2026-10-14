![](bbox=[0.19, 0.06, 0.81, 0.21])

The last thing we need to do on this page is to Create a new User. But to do that, we’re going to need a Modal Dialog Box first.

# 30.12. Modal Dialog Component

We’re going to build a Modal Dialog Component called Modal. It will work similar to our Page Component in that it’ll have an Inner Component. The Inner Component can be anything, e.g. a Form like we’ll need for the Create User Modal or just Text as we’ll need for our error Dialogs that will replace the use of alertError.

Let’s start with a design:

![](bbox=[0.15, 0.46, 0.85, 0.78])

Input from the Parent to the Modal Component will be passed directly to the Inner Component. And Output from the Inner Component will be passed directly to the Parent.

The Modal Component will have 2 buttons with default labels OK and CANCEL, which will produce the Outputs Affirmative and Negative respectively. We’ll allow some configuration on our Modal Component, i.e. re-labeling the buttons and disabling the Cancel Button.

This is going to be pretty complicated compared to other Components that we’ve done so far, and more