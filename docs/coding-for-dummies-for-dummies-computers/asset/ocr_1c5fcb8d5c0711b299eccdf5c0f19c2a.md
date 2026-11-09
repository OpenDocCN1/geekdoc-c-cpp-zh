# Understanding how forms work

Forms pass information entered by a user to a server by using the following process:

+   1. The browser displays a form on the client machine.
+   2. The user completes the form and presses the submit button.
+   3. The browser submits the data collected from the form to a server.
+   4. The server processes and stores the data and sends a response to the client machine.
+   5. The browser displays the response, usually indicating whether the submission was successful.

See Chapter 2 for an additional discussion about the relationship between the client and server.

![](bbox=[0.12, 0.34, 0.2, 0.49])

A full description of how the server receives and stores data (Steps 3 to 5) is beyond the scope of this book. For now, all you need to know is that server-side programming languages such as Python, PHP, and Ruby are used to write scripts that receive and store form submissions.

Forms are very flexible, and can record a variety of user inputs. Input fields used in forms can include free text fields, radio buttons, checkboxes, drop-down menus, range sliders, dates, phone numbers, and more. (See Table 5-4.) Additionally, input fields can be set to initial default values without any user input.

**Table 5-4 Selected form attributes**

| Attribute name | Possible values | Description |
|---|---|---|
| type | checkbox<br>email<br>submit<br>text<br>password<br>radio<br>(a complete list of values has been omitted here for brevity) | Defines the type of input field to display in the form. For example, text is used for free text fields, and submit is used to create a submit button. |
| value | text | The initial value of the input control. |