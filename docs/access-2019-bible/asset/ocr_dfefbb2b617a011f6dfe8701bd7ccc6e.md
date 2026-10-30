# Tip

You can create your own Input Mask properties for Short Text and Date/Time fields by simply clicking the Edit List button in the Input Mask Wizard and entering a descriptive name, input mask, placeholder character, and sample data content. Once created, the new mask will be available the next time you use the Input Mask Wizard.

Enter as many custom masks as you need. You can also determine the international settings so that you can work with multiple country masks. A custom input mask you create in one database is available in other databases.

# Caption

The Caption property determines what appears in the default label attached to a control created by dragging the field from the field list onto a form or report. The caption also appears as the column heading in Datasheet view for tables or queries that include the field.

# CAUTION

Be careful using the Caption property. Because the caption text appears as the column heading in Datasheet view, you might be misled by a column heading in a query’s Datasheet view. When the field appears in a query, you don’t have immediate access to the field’s properties, so you must be aware that the column heading is actually determined by the Caption property and may not reflect the field’s name. To be even more confusing, the caption assigned in the table’s Design view and the caption assigned in a field’s Property Sheet in the Query Design view are different properties and can contain different text.

Captions can be as long as 2,048 characters, more than adequate for all but the most verbose descriptions.

# Validation Rule and Validation Text

The Validation Rule property establishes requirements for input into the field. Enforced by the ACE database engine, the Validation Rule ensures that data entered into the table conforms to the requirements of the application.

Validation properties are a great way to enforce business rules, such as ensuring that a product is not sold for zero dollars, or requiring that an employee review date come after her hire date. And, like other field properties, validation rules are enforced wherever the field is used in the application.

The value of the Validation Rule property is a string containing an expression that is used to test the user’s input. The expression used as a field’s Validation Rule property can’t contain user-defined functions or any of the Access domain or aggregate functions (DCount, DSum, and so on). A field’s Validation Rule property can’t reference forms, queries, or other tables in the application. (These restrictions don’t apply to validation rules applied