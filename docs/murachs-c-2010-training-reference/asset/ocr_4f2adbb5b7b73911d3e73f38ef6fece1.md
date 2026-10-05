# The Product class

| Property | Description |
| --- | --- |
| Code | A string that contains a code that uniquely identifies the product. |
| Description | A string that contains a description of the product. |
| Price | A decimal that contains the product's price. |
| Method | Description |
| GetDisplayText (sep) | Returns a string that contains the code, description, and price specified by the sep string. |
| Constructor | Description |
| (code, description, price) | Creates a Product object with default values. Creates a Product object using the specified values. |

# The ProductDB class

| Method | Description |
| --- | --- |
| GetProducts () | A static method that returns a List<> of Product objects from the Products file. |
| SaveProducts (list) | A static method that writes the products in the spccified List<> of Product objects to the Products file. |

# The Validator class

| Property | Description |
| --- | --- |
| Title | A string that contains the text that is displayed in the title bar of a dialog box that is displayed for an error message. |
| Method | Description |
| IsPresent(textBox) | A static method that returns a Boolean value that indicates if data was entered into the specified text box. |
| IsInt32(textBox) | A static method that returns a Boolean value that indicates if an integer was entered into the specified text box. |
| IsDecimal(textBox) | A static method that returns a Boolean value that indicates if a decimal was entered into the specified text box. |
| IsWithinRange(textBox, min, max) | A static method that returns a Boolean value that indicates if the value entered into the specified text box is within the specified range. |

> Note: Each of these methods displays an error message in a dialog box and moves the focus to the text box if the data is invalid.

# Note

+   - Because you don't need to know how the ProductDB class works, its code isn't shown in this class. Please refer to chapters 21 and 22 for three different versions of this class.

Figure 12-13 The classes used by the Product Maintenance application