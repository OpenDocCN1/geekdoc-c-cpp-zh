To add validation checks, you associate ValidationRules with your Binding, as shown in Listing 18.15.

# LISTING 18.15 Associating ValidationRules with a Binding

```
<TextBox Name="LastName">
<TextBox.Text>
<Binding Path="LastName" UpdateSourceTrigger="PropertyChanged">
<Binding.ValidationRules>
<ExceptionValidationRule />
</Binding.ValidationRules>
</Binding>
</TextBox.Text>
</TextBox>
```

As you can see, the ValidationRules property takes a collection of ValidationRule objects. The ExceptionValidationRule is a built-in validation rule that checks for exceptions thrown during the update of the binding source. If the source object implements the IDataError interface, you can use the built-in DataErrorValidationRule to check for errors raised by the IDataError implementation.

> **ValidatesOnException and ValidatesOnDataErrors**

As an alternative to explicitly including the ExceptionValidationRule, you can set the ValidatesOnExceptions property to true. Similarly, you can set the ValidatesOnDataErrors property to true rather than explicitly including the DataErrorValidationRule.

To provide your own application-specific validation rules, you derive a new class from the ValidationRule class and implement the Validate method. Listing 18.16 shows a validation rule for the AddressBook application that can validate phone numbers.

# LISTING 18.16 A Custom ValidationRule

```
class PhoneNumberValidationRule : ValidationRule
{
public override ValidationResult Validate(object value, CultureInfo cultureInfo)
{
string stringValue = value.ToString();
string pattern = @"^((\+?d+)\\s(\\(d{3}\\)\\s\\w{3}[-\\.\\w{4})\\s\\w{3}[-\\.\\w{4}])+";

if (String.IsNullOrEmpty(stringValue) ||
Regex.IsMatch(stringValue, pattern))
{
return ValidationResult.ValidResult;
}
else
{
return new ValidationResult(false, "Value is not a valid phone number.");
}
}
```