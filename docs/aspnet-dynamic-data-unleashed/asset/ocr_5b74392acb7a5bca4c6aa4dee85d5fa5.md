# Reporting Multiple Errors

As you recall from Listing 8.1, the Validate method of the UnleashedObjectContext class calls the static ValidateObject method of the Validator class to validate all new and modified entity objects. This method throws a ValidationException for the first validation error it encounters. Even though the Validate method of the Order class might report two errors at the same time (one for the OrderDate and one for the RequiredDate properties), only the first one is reported through the exception.

Although reporting a single error at a time might not be a problem in simple pages, like the Order entry form in the sample application, as the number of fields on the form increases, fixing one error only to get another is not very user friendly. Figure 8.9 illustrates the problem.

![](bbox=[0.12, 0.5, 0.52, 0.7])

FIGURE 8.9 First of multiple errors reported in a Dynamic Data web page.

This is not a problem with the built-in validation attributes such as the RequiredAttribute or the CustomValidationAttribute applied to individual properties because they are invoked directly by separate DynamicValidator controls inside the field templates on the web page. In other words, all property-level validation attributes are evaluated independently, and all errors are reported to the user at the same time. However, class-level CustomValidationAttribute instances and the Validate method of the IValidatableObject interface are invoked only by the ValidateObject method called in the SaveChanges method of the UnleashedObjectContext class, and only the first error is reported.

# IDynamicValidatorException Interface

Dynamic Data defines a special interface, IDynamicValidatorException, that allows exception classes to supply information about multiple errors that might have occurred during a single operation. This interface defines a single property, InnerExceptions, which returns a dictionary of entity property names and exceptions encountered for these properties.