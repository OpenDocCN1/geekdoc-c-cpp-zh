TIP Although you can turn any element into a list item or table, don't. This is bad coding for a semantic and accessibility standpoint. Stick to HTML tags for creating lists and tables.

TIP The compact property was dropped in CSS2.1 but may make a comeback in CSS3. At present, only a placeholder exists in the CSS Work Groups Box Model documentation for CSS3.

TIP Any elements that are assigned display:none will be ignored by the browser. Be careful when using none, however. Although it is not an inherited attribute, none turns off the element display as well as the display of any children elements.

TIP display:none is useful for creating dynamic elements—such as drop-down menus—that show and hide the user interacts with the page. However, keep in mind that this also hides the element from screen readers which can be bad for usability.

TIP Another great use for none is to create it a print-specific style sheet that hides elements not needed when the page is printed, such as navigation and form fields. Who needs navigation links, search forms, and low-resolution graphics in a printout?

TIP The display property should not be confused with the visibility property (see "Setting the Visibility of an Element" in Chapter 11). Unlike the visibility property, which leaves a space for the element, display:none completly removes the element from the page, although the browser still loads its content.