
## Add a range validator

- 14. Add a range validator for the Arrival date text box. Because the date range will be set at runtime, you don’t need to set the MinimumValue and MaximumValue properties.
- 15. Add code to the Load event handler for the page that sets the minimum value for the range validator to the current date and the maximum value to six months from the current date. This code will be similar to the code shown in figure 7-6.
- 16. Run the application, and enter or select a date that’s before the current date. Click the Submit button. The error message for the range validator should be displayed.
- 17. Enter or select a date that’s more than six months in the future, and click the Submit button again. The error message should still be displayed.
- 18. Enter or select a date within six months of the current date, and click the Submit button one more time. This time, the error message shouldn’t be displayed.

## Add a regular expression validator

- 19. Add a regular expression validator for the Email text box. Use the Regular Expression Editor dialog box as shown in figure 7-9 to set the ValidationExpression property to the Internet E-mail Address expression.
- 20. Run the application, and enter an email address that doesn’t include an at sign (@). The error message for the regular expression validator should be displayed.
- 21. Enter another email address, this time without a period. The error message should still be displayed.
- 22. Enter an email address with both an at sign and a period, and then click the Submit button to see that the error message is no longer displayed.

## Add a validation summary control

- 23. Add a new paragraph at the bottom of the page, and then add a validation summary control to the paragraph. Enter an appropriate value for the HeaderText property.
- 24. Run the application and click the Submit button to see how this looks. Notice that the error messages are displayed in both the validators and the validation summary control.
- 25. Set the Text property of each of the validators to an asterisk. Then, run the application again and click the Submit button to see how this looks.
- 26. Continue experimenting with the page until you’re sure you understand how the validators work.

## How to manage state

In chapters 2 and 3, you were introduced to the way that view state and session state are used. Now you’ll learn more about using these states, and you’ll also learn how to use application state. Beyond that, you’ll learn how to use cookies and URL encoding to pass data between the server and the client. Because HTTP is a stateless protocol, these are essential skills for every web developer.

- How to use view state ................................................... 282
- How to work with view state ................................................... 282
- How to use view state for your own data ................................................... 284
- How to use session state ................................................... 286
- How to work with session state ................................................... 286
- When to save and retrieve session state items ................................................... 288
- Options for storing session state data ................................................... 290
- Options for tracking session IDs ................................................... 290
- How to set session state options ................................................... 292
- How to use application state ................................................... 294
- How application state works ................................................... 294
- How to work with application state data ................................................... 296
- How to work with application events ................................................... 298
- How to use cookies and URL encoding ................................................... 300
- How to create cookies ................................................... 300
- How to work with cookies ................................................... 302
- How to enable or disable cookies ................................................... 304
- How to use URL encoding ................................................... 306
- Perspective ................................................... 308

## How to use view state

For the most part, view state is automatic. Because of that, you don’t have to set any properties or write any code to use it. Nevertheless, you should at least understand how view state works and how to use it to your advantage. In some cases, you may even want to add your own data to view state.

## How to work with view state

As the summary in figure 8-1 says, view state works by saving data in the HTML stream that’s sent to the browser when a page is requested. This data is saved as a hidden input field named _VIEWSTATE. Because the field is hidden, it isn’t displayed in the browser. And because the field is an input field, it’s automatically sent back to the server when the user posts the page.

View state is used to retain the values of the form and control properties that you set in code. In the Future Value application of chapter 2, for example, the values in the drop-down list were set by code. As a result, these values don’t need to be reset by code each time the page is posted back to the server. Instead, they’re automatically reset by view state.

The EnableViewState property of a page and its controls determines if view state is enabled, which it is by default. Although this is usually what you want, you may occasionally want to disable view state. One reason for doing that is to get a control to work the way you want it to. Another reason is to improve performance when view state gets so large that it degrades performance.

If, for example, you change the value of a control property in code, but you want the initial value of that property restored each time the page is loaded, you can turn off view state to get the page to work right. Or, if a page is never posted back to itself, you can turn off view state to improve performance. In practice, though, you probably won’t turn off view state until you discover that it’s creating either a programming or performance problem.

With versions of ASP.NET before ASP.NET 4, you couldn’t disable view state for a page and then enable view state for selected controls. That made it difficult to disable view state for most, but not all, of the controls on a page. But ASP.NET 4 makes this easy to do with its new ViewStateMode property. Note that this works only if the EnableViewState property of the page and the selected controls is set to True. Otherwise, the ViewStateMode property has no effect.

To determine the size of view state, you can enable the ASP.NET Trace feature as described in chapter 4. Then, you can scroll to the Control Tree section of the trace output to see which controls are using view state and how many bytes they’re using. That way, you can tell whether it’s worth the effort to turn view state off.

## View state concepts

- *View state* is an ASP.NET feature that provides for retaining the values of page and control properties that change from one execution of a page to another.
- Before ASP.NET sends a page back to the client, it determines what changes the program has made to the properties of the page and its controls. These changes are encoded into a string that’s assigned to the value of a hidden input field named _VIEWSTATE.
- When the page is posted back to the server, the _VIEWSTATE field is sent back to the server along with the HTTP request. Then, ASP.NET retrieves the property values from the _VIEWSTATE field and uses them to restore the page and control properties.
- ASP.NET also uses view state to save the values of the page properties it uses, such as IsPostBack.
- View state is *not* used to restore data entered by a user into a text box or any other input control unless the control responds to change events.
- If view state is enabled for a data-bound control, the control will not be rebound when the page is reposted. Instead, the control’s values will be restored from view state.

## Two cases when you may want to disable view state

- When restoring the control properties for a page affects the way you want the form to work, you may want to disable view state for one or more controls. Otherwise, you can modify your code so the page works without turning view state off.
- When the size of the view state field gets so large that it affects performance, you may want to disable view state for one or more controls or for an entire page.

## How to disable view state

- To disable view state for a control, set the control’s EnableViewState property to False.
- To disable view state for an entire page, set the EnableViewState property of the page (Page directive) to False. That disables view state for all the controls on the page.

## How to enable view state for selected controls

- Set the EnableViewState property of the page and the controls whose view state you want to enable to True.
- Set the ViewStateMode property of the page (Page directive) to Disabled.
- Set the ViewStateMode property of the controls whose view state you want to enable to Enabled.

## How to determine the size of view state for a page

- Enable the Trace feature for the page by setting the Trace attribute of the Page directive for the page to True as described in chapter 4. Then, scroll down to the Control Tree section of the trace output to see the number of bytes of view state used by the page and its controls.
