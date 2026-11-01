new page (or Master Page as you learn in Chapter 6) created in VS already contains the `<form>` element, so you don't have to add it yourself. Finally, it's important to understand that an ASP.NET Web Form by default always submits back to itself. In other web environments, like classic ASP and PHP, it's not uncommon to set the `action` attribute of the page to a second page that then processes the data the user has submitted. However, with an ASP.NET page, you'll find that even if you set the `action` attribute in the code explicitly, the ASP.NET run time will revert it to the name of the current page.

> **NOTE** ASP.NET supports a feature called Cross Page Postbacks that enables you to submit from one page to another. To learn more about this concept, search the MSDN site for Cross Page Postbacks or get yourself a copy of Professional ASP.NET 4.5 from Wrox.

The next thing to look at is ASP.NET's View State functionality implemented with the hidden `__VIEWSTATE` field that you see in the HTML source bolded in the following snippet:

```
```html
<form method="post" action="State.aspx" id="form1">
...
<input type="hidden" name="__VIEWSTATE" id="__VIEWSTATE" value="IXcrUZS1B9YmtdoSL5cn2+Vrx5oW3k2kAwoRXGsE3P0/W016/upieH7Nhtlf hyr99U0IRKmJyYk4PdH5B9ZRucaJ0xPkwCyR0NB1K3kidqR5eAVX86D q0f1584e5B0f3F1P4O3Y+ZqD7q2pA==" />
</div>
```
```

Although at first the text appears to contain nothing more than random characters, it actually contains useful information. To protect the information stored in this field, ASP.NET has converted the page state in the preceding string. If you were able to look inside the value of the fields, you'd find a value for the `Label1` control with the current date and time.

When your ASP.NET page loads, the ASP.NET run time fills this hidden field with information about the page. For example, it added the value for the `Text` property of the `Label1` control when you caused a postback by clicking the Set Date button. Similarly, it contains the selected date for the `Calendar` control. When the page is then submitted back by a postback, the value in this hidden `__VIEWSTATE` field is sent with the request. Then, when ASP.NET creates the new page on the server, the information from the `__VIEWSTATE` field is read and applied to the controls in the page. This way, a control like the `Label` can be able to maintain its text even after the page has been posted back to the server.

The `TextBox` doesn't need View State, though. It's able to maintain its value because the browser submits it to the server with each postback.

To reiterate, here's a rundown of the process that took place in the preceding Try It Out.

+   1. You requested the page in the browser by opening it from within VS.
+   2. The browser got the page from the server by making a request for it.
+   3. The ASP.NET run time read the page from disk, processed it, and sent the resulting HTML to the browser. At this stage, all the controls were set to their default values that were defined in the markup of the page. For example, the `Text` of the `Label` control is set to `Label`.