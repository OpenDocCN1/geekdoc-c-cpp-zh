![](bbox=[0.102, 0.059, 0.897, 0.38])

Now, we have some decisions to make. We want to have the user type in their Username and Password then click on the Logon Button. But what should we do if they haven't done so and they simply click the Logon Button?

There are a few things we could do. We could not enable the Logon Button when there is no data in the required fields. This will require us to monitor every change to Username and Password so we can enable the Logon Button as soon as every required field has data in it.

Another approach we could take is to give an error message when a required field is empty and they've clicked the Logon Button. The only question is how do we display this error message?

There are 2 ways that come to mind. First, we display an error message next to the offending fields, i.e. the required fields that are empty. Another way is to display a pop-up Dialog Box with the error message in it.

Which approach would you take and why do you think that your approach is better than the others? Think about this for a moment before reading my opinion.

My favorite approach is to disable the button and only display it when it's valid since I think it provides for a cleaner UI. The only downside to this approach is when the user doesn't understand what they need to enter to enable the button. But I think we don't run that risk here with this form since any user who has spent any time on the Internet has encountered many Logon Screens.

So, for this scenario, I'm going to choose that approach. However, if this were a more complex form, then I'd choose to add error messages next to the missing fields.

And while the Dialog Box isn't a terrible idea here, we're going to have plenty of opportunities for Dialog Boxes in this app.

Dialog boxes aren't my favorite solution, but sometimes they are necessary to reduce screen clutter and it'll