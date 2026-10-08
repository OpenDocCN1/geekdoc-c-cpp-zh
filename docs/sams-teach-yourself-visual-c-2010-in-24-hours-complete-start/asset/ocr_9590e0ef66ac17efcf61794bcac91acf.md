+   8. The output will be as follows:
```text
;10;
; 10;
;0010;
24
```
(24)

+   9. Because the `StringBuilder` represents a mutable string, using it for string concatenation inside a loop prevents multiple temporary strings from being created during each iteration to perform the concatenation.

+   10. This is a simple regular expression for parsing a string as an email address. Broken down, it means "Match any word character one or more times followed by the @ character followed by a group containing any word character one or more times followed by a period (.) character, where that group is repeated one or more times, followed by any word character one or more times."

# Exercises

+   1. Add a read-only string property to the `Contact` class of the `AddressBook` project named `DisplayAs`. The `get` accessor should use `String.Format` to return the `FirstName` and `LastName` properties in the order indicated by the `DisplayStyle` property.

+   2. Override the `ToString` method on `PhoneNumber` to return a properly formatted phone number using a `StringBuilder`. If the `CountryCode` or `Extension` properties do not have valid values, they should be excluded. (Any nonzero value for `CountryCode` is valid and any nonempty string value for `Extension` is valid.)

+   3. Implement a `Validate` method on `PhoneNumber` that uses the static `RegEx.IsMatch` method to validate the phone number. Use the result of calling `this.ToString` as the input value for the `IsMatch` method. The regular expression pattern should look like:

```
`^(\+[2-9]\d{3})? \d{7}( \d{4})? [2-9]\d{2}-\d{4}$`
```