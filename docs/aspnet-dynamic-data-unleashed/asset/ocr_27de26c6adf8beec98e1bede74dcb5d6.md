```
if (!Validator.TryValidateObject(entity, context, results, true))
    ThrowValidationException(entity, results);
}
```

The new version calls the TryValidateObject method of the static Validator class. Unlike the ValidateObject method used previously, which throws a single ValidationException for the first error it detects, the TryValidateObject method invokes all validation attributes and implementations of the IValidatableObject interface. The TryValidateObject method collects the errors in the list of ValidationResult objects it receives as the third parameter and returns false if any errors were detected.

The ThrowValidationException method (shown next) uses the validation results to create a list of ValidationException objects. If multiple validation results were reported, it throws the AggregateException. Otherwise, it throws the ValidationException to mimic the simple behavior implemented earlier:

```
protected static void ThrowValidationException(
    object entity, IEnumerable<ValidationResult> results)
{
    var exceptions = new List<ValidationException>();
    foreach (ValidationResult result in results)
        exceptions.Add(new ValidationException(result, null, entity));

    if (exceptions.Count == 1)
        throw exceptions[0];

    throw new AggregateException(exceptions);
}
```

> **NOTE**
> The AggregateException does not inherit from the ValidationException class. Now that the SaveChanges method can throw two different exception types, many of the automated tests written so far will fail because they only expect the ValidationException. To make them pass, change the ExpectedValidationExceptionAttribute to support both types of validation exceptions. You can find the updated implementation of this attribute in the source code accompanying this book.

# Extending DynamicValidator to Support AggregateException

As discussed in Chapter 3 and Chapter 6, Dynamic Data relies on the DynamicValidator control for exception handling. When used in a field template, this control is responsible for evaluating the validation attributes applied to the entity property the template instance represents. In field and page templates, this control also handles any exceptions Entity Framework may throw. Here is the part of this class that implements exception handling: