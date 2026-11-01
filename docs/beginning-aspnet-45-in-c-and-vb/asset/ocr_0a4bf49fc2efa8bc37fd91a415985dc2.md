This means that the Panel is only visible when the check box is checked. When it isn't, the Panel is hidden automatically.

As you can see, it's easy to add text and other markup to the Panel control in VS. Right now, you only added some plaintext, but in the next section you see how to add a Wizard control and how to use it.

# Magic with the Wizard Control

The Wizard control is a great tool for breaking apart large Web Forms and presenting them as bite-sized chunks of information to the user. Instead of confusing your user with one page with many controls and text on it, you can break the page apart and present each section on a separate wizard page. The Wizard control then handles all navigation issues by creating Next, Previous, and Finish buttons automatically. In the following exercise you use a wizard to ask a user for her name and favorite programming language. Although the example itself is pretty trivial, and you could have placed both questions on the same page without confusing the user, the example shows how the wizard works and why it's useful. You can easily apply the same techniques to your own, possibly larger, Web Forms.

# TRY IT OUT  Using the Wizard to Create Easy-to-Use Forms

In this Try It Out, you place a Wizard inside the panel you created in the previous exercise that enables a user to fill in a form that is spread over a couple of pages. The wizard will have two steps where a user can enter details, and a results page that shows the data the user has provided.

+   1. Make sure you still have Containers.aspx page open in Design View. Remove the text "I am visible now" that you entered in the previous Try It Out, and then drag a Wizard control from the Toolbox inside the Panel. Drag its right edge further to the right, increasing the total width of the control to 500px. Your page now looks similar to Figure 4-11.
+   2. Open the Wizard's Smart Tasks panel (click the arrow in its upper right-hand corner) and choose Add/Remove WizardSteps. In the dialog box that follows, click the Add button to insert a third wizard step, shown in Figure 4-12.

![](bbox=[0.1, 0.78, 0.92, 0.96])