With the key fields added to each table, you can now find a field in each table that links it to other tables in the database. For example, Table 1.4 shows Customer ID in both the Customers table (where it’s the primary key) and the Invoice table (where it’s a foreign key).

You’ve identified the three core tables for your system, as reflected by the first three columns in Table 1.4. This is the general, or first, cut toward the final table designs. You’ve also created an additional fact table to hold the sales payment data. Normally, payment details (such as the credit card number) are not part of a sales invoice.

Taking time to properly design your database and the tables contained within it is arguably the most important step in developing a database-oriented application. By designing your database efficiently, you maintain control of the data, eliminating costly data-entry mistakes and limiting your data entry to essential fields.

Although this book is not geared toward teaching database theory and all its nuances, this is a good place to briefly describe the art of database normalization. You’ll read the details of normalization in Chapter 4, but in the meantime you should know that normalization is the process of breaking data down into constituent tables. Earlier in this chapter you read about how many Access developers add dissimilar information, such as customers, invoice data, and invoice line items, into one large table. A large table containing dissimilar data quickly becomes unwieldy and hard to keep updated. Because a customer’s phone number appears in every row containing that customer’s data, multiple updates must be made when the phone number changes.

# Step 5: Form design

After you’ve created the data and established table relationships, it’s time to design your forms. Forms are made up of the fields that can be entered or viewed in Edit mode. Generally speaking, your Access screens should look a lot like the forms used in a manual system.

When you’re designing forms, you need to place three types of objects onscreen:

+   - Labels and text-box data-entry fields: The fields on Access forms and reports are called controls.
+   - Special controls (command buttons, multiple-line text boxes, option buttons, list boxes, check boxes, business graphs, and pictures).
+   - Graphical objects to enhance the forms (colors, lines, rectangles, and three-dimensional effects).

Ideally, if the form is being developed from an existing printed form, the Access data-entry form should resemble the printed form. The fields should be in the same relative place on the screen as they are in the printed counterpart.

Labels display messages, titles, or captions. Text boxes provide an area where you can type or display text or numbers that are contained in your database. Check boxes indicate a condition and are either unchecked or checked. Other types of controls available with Access include command buttons, list boxes, combo boxes, option buttons, toggle buttons, and option groups.

Starting with Part V, we cover in detail the topic of creating forms.