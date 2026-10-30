+   - **Form:** Creates a new form that lets you enter information for one record at a time. You must have a table, query, form, or report open or selected to use this command. When you click the Form button with a table or query highlighted in the Navigation pane, Access binds the new form to the data source and opens the form in Layout view.
+   - **Form Design:** Creates a new blank form and displays it in Design view. The form isn't bound to any data source. You must specify a data source (table or query) and build the form by adding controls from the data source's field list.
+   - **Blank Form:** Instantly creates a blank form with no controls. Like Form Design, the new form is not bound to a data source, but it opens in Layout view.
+   - **Form Wizard:** Access features a simple wizard to help you get started building forms. The wizard asks for the data source, provides a screen for selecting fields to include on the form, and lets you choose from a number of very basic layouts for the new form.
+   - **Navigation Form:** The Access navigation form is a specialized form intended to provide user navigation through an application. Navigation forms are discussed in detail later in this chapter.
+   - **More Forms:** The More Forms button in the Forms group drops down a gallery containing a number of other form types.
+     - **Multiple Items:** This is a simple tabular form that shows multiple records bound to the selected data source instead of the usual one-record-at-a-time display.
+     - **Datasheet:** Creates a form that is displayed as a datasheet.
+     - **Split Form:** Creates a split form, which shows a datasheet in the upper, lower, left, or right area of the form, and a traditional form in the opposite section for entering information on the record selected in the datasheet.
+     - **Modal Dialog:** Provides a template for a modal dialog form. A modal dialog form (often called a dialog box) stays on the screen until the user provides information requested by the dialog or is dismissed by the user.

The options in the Forms group of the Create Ribbon all do the same thing—create a form. The difference is that each sets certain form properties to get a desired effect. You can set those properties yourself. For example, if you chose Form Design and restricted the views to only Datasheet View, it would be the same as choosing Datasheet on the More Forms menu. These controls are handy shortcuts, but don't worry if you pick the wrong one. You can change the properties to make the form look and behave exactly as you want.

If any of the terminology in the preceding bullets is new to you, don't worry—each of these terms is discussed in detail in this chapter. Keep in mind that the Access Ribbon and its contents are very context dependent, so every item may not be available when you select the Create tab.

# Creating a new form

Like many other aspects of Access development, Access provides multiple ways of adding new forms to your application. The easiest is to select a data source, such as a table, and