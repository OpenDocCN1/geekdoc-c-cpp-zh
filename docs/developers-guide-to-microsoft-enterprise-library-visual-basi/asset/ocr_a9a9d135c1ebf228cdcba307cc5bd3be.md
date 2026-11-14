For example, to obtain a validator for the **Product** class that validates using only attributes and self-validation methods within the target instance, and validate an instance of this class, you resolve an instance of the **AttributeValidatorFactory** from the container, as shown here.

```
Dim attrFactory As AttributeValidatorFactory = _
EnterpriseLibraryContainer.Current.GetInstance(Of AttributeValidatorFactory)()
Dim pValidator As Validator(Of Product) _
= attrFactory.CreateValidator(Of Product)()
Dim valResults As ValidationResults = pValidator.Validate(myProduct)
```

# CREATING AND USING INDIVIDUAL VALIDATORS

You can create an instance of any of the validators included in the Validation block directly in your code, and then call its **Validate** method to validate an object or value. For example, you can create a new Date Time Range validator and set the properties, such as the upper and lower bounds, the message, and the **Tag** property. Then you call the **Validate** method of the validator, specifying the object or value you want to validate. The example, **Creating and Using Validators Directly**, demonstrates the creation and use of some of the individual and composite validators provided with the Validation block.

# Validating Strings for Contained Characters

The example code first creates a **ContainsCharactersValidator** that specifies that the validated value must contain the characters c, a, and t, and that it must contain all of these characters (you can, if you wish, specify that it must only contain **Any** of the characters). The code also sets the **Tag** property to a user-defined string that helps to identify the validator in the list of errors. The overload of the **Validate** method used here returns a new **ValidationResults** instance containing a **ValidationResult** instance for each validation error that occurred.

```
' Create a Contains Characters Validator and use it to validate a string.
Dim charsValidator As New ContainsCharactersValidator("cat", _
ContainsCharacters.All, _
" Value must contain {4} of the characters '{3}'.")
charsValidator.Tag = "Validating the String value 'disconnected'"
Dim valResults As ValidationResults = charsValidator.Validate("disconnected")
```

# Validating Integers within a Domain

Next, the example code creates a new **DomainValidator** for integer values, specifying an error message and an array of acceptable values. Then it can be used to validate an integer, with a reference to the existing **ValidationResults** instance passed to the **Validate** method this time.

```
' Create a Domain Validator and use it to validate an Integer value.
Dim integerValidator As Validator = New DomainValidator(Of Integer)( _
"Value must be in the list 1, 3, 7, 11, 13.", _
New Integer() {1, 3, 7, 11, 13})
```