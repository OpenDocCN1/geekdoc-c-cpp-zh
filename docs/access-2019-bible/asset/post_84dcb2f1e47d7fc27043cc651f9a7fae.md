
creating a new table, this process is easy. For existing tables that are referenced elsewhere in your application, changing the field name can cause problems, as discussed in the “Designing tables” section earlier in this chapter.

## Changing a field size

Making a field size larger is simple in a table design. You simply increase the Field Size property for text fields or specify a different field size for number fields. You must pay attention to the Decimal Places property in number fields to make sure you don’t select a new size that supports fewer decimal places than you currently have.

> CAUTION
> When you want to make a field size smaller, make sure that none of the data in the table is larger than the new field width. Choosing a smaller field size may result in data loss.

> TIP
> Remember that each text field uses only the number of characters actually entered in the field. You should still try to make your fields only as large as the largest value so that Access can stop someone from entering a value that might not fit on a form or report.

## Handling data conversion issues

If, in spite of your best efforts, it becomes necessary to change the data type of a field containing data, you might suffer data loss as the data-type conversion occurs. You should be aware of the effects of a data-type conversion on existing data:

- **Any data type to AutoNumber:** Can’t be done. The AutoNumber field type must be created fresh in a new field.
- **Short Text to Number, Currency, Date/Time, or Yes/No:** In most cases, the conversion will be made without damaging the data. Inappropriate values are automatically deleted. For instance, a Short Text field containing “January 28, 2018” will be faithfully converted to a Date/Time field. If, however, you change a field containing “January 28, 2018” to a Yes/No data type, its value will be deleted.
- **Long Text to Short Text:** A straightforward conversion with no corruption of data. Any text longer than the field size specified for the Short Text field is truncated and lost.
- **Number or Large Number to Short Text:** No loss of information. The number value is converted to text using the General Number format.
- **Number or Large Number to Currency:** Because the Currency data type uses a fixed decimal point, some precision may be lost as the number is truncated.
- **Date/Time to Short Text:** No loss of information. Date and time data are converted to text with the General Date format.
- **Currency to Short Text:** No loss of information. The currency value is converted to text without the currency symbol.
- **Currency to Number:** Simple, straightforward conversion. Some data may be lost as the currency value is converted to fit the new number field. For example, when converting Currency to Long Integer, the decimal portion is truncated (cut off).
- **AutoNumber to Short Text:** Conversion occurs without loss of data, except in a case where the width of the text field is inadequate to hold the entire AutoNumber value. In this case, the number is truncated.
- **AutoNumber to Number:** Simple, straightforward conversion. Some data may be lost as the AutoNumber value is converted to fit the new number field. For example, an AutoNumber larger than 32,767 will be truncated if it is converted to an Integer field.
- **Yes/No to Short Text:** Simple conversion of Yes/No value to text. No loss of information.

> NOTE
> The OLE Object data type cannot be converted to any other type of data.

## Assigning field properties

The field properties built into Access tables are powerful allies that can help you manage the data in your tables. In most cases, the field property is enforced by the database engine, which means the property is consistently applied wherever the field's value is used. For example, if you've set the Default Value property in the table design, the default value is available in the table's Datasheet view, on forms, and in queries.

In fact, field properties are among the many differences between Access tables and Excel worksheets. Understanding field properties is just one of several skills necessary to begin using Access tables to store data, rather than Excel worksheets.

Each field data type has its own set of properties. For example, Number fields have a Decimal Places property, and Short Text fields have a Text Align property. Although many data types share a number of properties (such as Caption) in common, there are enough different field properties to make it easy to become confused or to incorrectly use the properties. The following sections discuss some of the more important and frequently used field properties.

> NOTE
> The following sections include many references to properties, and property settings in the Access Table Designer. The formal name for a property (such as DefaultValue) never contains a space, while the property's expression in the Table Designer usually contains a space for readability (Default Value). These relatively minor differences become important when referencing properties in expressions, VBA code, and macros. When making a formal reference to a property in code or a macro, always use the spaceless version of the property's name, not the property reference you see in the Access user interface.

## Common properties

Here’s a list of all the general properties (note that they may not all be displayed, depending on which data type you chose):

- **Field Size:** When applied to Short Text fields, limits the size of the field to the specified number of characters (1–255). The default is 255.
- **New Values:** Applies to AutoNumber fields. Allows specification of Increment or Random type.
- **Format:** Changes the way data appears after you enter it (uppercase, dates, and so on). There are many different types of formats that may be applied to Access data. Many of these differences are explained in the “Format” section, later in this chapter.
- **Input Mask:** Used for data entry into a predefined format (phone numbers, zip codes, Social Security numbers, dates, customer IDs). Applicable to both numeric and text data types.
- **Decimal Places:** Specifies the number of decimal places for the Currency, Number, and Large Number data types.
- **Caption:** Optional label that’s used in place of the field’s name. Access uses the Caption property when displaying a control in a datasheet or on a form or report.
- **Default Value:** The value automatically provided for new data entry into the field. This value can be any value appropriate for the field’s data type. A default is no more than an initial value; you can change it during data entry. To specify a default value, simply enter the desired value into the Default Value property setting. A default value can be an expression, as well as a number or a text string.

> NOTE
> Because the Default Value for Number and Currency data types is set to 0 by default, these fields are automatically set to 0 when you add a new record. In many situations, such as medical test results and many financial applications, 0 is not an appropriate default value for numeric fields. Be sure to verify that 0 is an appropriate default value in your Access applications.

- **Validation Rule:** Ensures that data entered into the field conforms to some business rule, such as “greater than zero,” “date must occur after January 1, 2000,” and so on.
- **Validation Text:** The message displayed when data fails validation.
- **Required:** Specifies whether you must enter a value into a field.
- **Allow Zero Length:** Determines whether you may enter an empty string (“”) into a Short Text or Long Text field to distinguish it from a null value.
- **Indexed:** Speeds up data access and (if desired) limits data to unique values. Indexing is explained in greater detail later in this chapter.
- **Unicode Compression:** Used for multilingual applications. Requires about twice the data storage but enables Office documents, including Access reports, to be
