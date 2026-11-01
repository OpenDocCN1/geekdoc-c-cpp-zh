> **NOTE**
> 
> Validation attributes applied to properties and fields are evaluated before the attributes applied to the class. However, you should not rely on the order of validation within these two groups. The .NET Framework does not guarantee that the order of properties or attributes returned by the reflection APIs will match the order of their appearance in the source code. Even though, in many cases, the order of validation appears to match the order of attributes, there will be exceptions. If the order of validation rules is important, instead of attributes, you need to rely on coded validation discussed in the *Imperative Validation* section of this chapter.

If you want to validate an object without throwing a `ValidationException`, you can call the `TryValidateObject` method of the `Validator` class instead:

```
bool TryValidateObject(object instance, ValidationContext validationContext,
    ICollection<ValidationResult> validationResults, bool validateAllProperties)
```

This method returns a Boolean value that indicates whether or not the object is valid and populates the collection you supply in the `validationResults` parameter with a separate `ValidationResult` object for each error detected.

# Validation Error Messages

In addition to performing the validation itself, the validation attributes are responsible for generating error messages if the validation fails. Each concrete validation attribute, such as `RequiredAttribute`, discussed so far, provides a default error message. For instance, with the following definition of the `ProductName` property, the `RequiredAttribute` generates an error message “The ProductName field is required.”

```
[Required]
public string ProductName { get; set; }
```

Obviously, this error message is very technical and might not be appropriate for business users. You can replace the internal name of the field in the error message with its human-readable form by applying the `DisplayAttribute` as shown here:

```
[Required]
[Display(Name = "Product Name")]
public string ProductName { get; set; }
```

With this updated definition, the `RequiredAttribute` generates the error message as “The Product Name field is required,” which in many instances will be acceptable for display. However, if this is still not enough, you can completely replace the error message by specifying the `ErrorMessage` property in the validation attribute explicitly: