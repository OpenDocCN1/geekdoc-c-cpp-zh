# Field Value Edit Format

You might have noticed that the `DateTime_Edit` template uses the `FieldValueEditString` property of the `FieldTemplateUserControl` base class. This property is similar to the `FieldValueString` property discussed earlier in that it respects the `FormattingOptions` when converting the raw column value to a display string. However, it was specifically designed for use in the Edit mode templates, and an additional property is used to control its behavior.

+   - ApplyFormatInEditMode is a Boolean value that determines whether the DataFormatString, NullDisplayText, ConvertEmptyStringToNull, and HtmlEncode display format properties will be used in Edit mode. This property is false by default.

Similar to using the FieldValueString property when implementing Read-only field templates, it is also important to rely on the FieldValueEditString property as much as possible when implementing the Edit and Insert mode templates. This helps the field templates to behave consistently and allow the application developers to change presentation aspects of column values using metadata attributes as well as explicit configuration in page markup.

# Changing Existing Field Template

Dynamic Data uses the same field template for all matching columns in the model. The `DateTime_Edit` field template is automatically used for all columns of type DateTime in the Northwind data model, including OrderDate, RequiredDate, and ShippedDate columns of the Order table as well as BirthDate and HireDate columns of the Employee table. By changing definition of the field template, you affect all web pages where it is used. Figure 3.2 shows how the experience of entering date values can be improved by allowing the users to select a date from a calendar drop-down.