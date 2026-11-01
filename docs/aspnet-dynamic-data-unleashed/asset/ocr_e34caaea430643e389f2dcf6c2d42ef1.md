```
public class DynamicValidator : BaseValidator
{
    protected virtual Exception ValidationException { get; set; }
    protected virtual void ValidateException(Exception exception);
}
```

The control calls the ValidateException method whenever the EntityDataSource fires its Exception event. The method receives an Exception object and determines whether it represents an error condition expected by the DynamicValidator control. If it does, the ValidateException method assigns the exception object to the ValidationException property. If this property is not null during page validation, the DynamicValidator uses it to display the exception's error message.

Out of the box, DynamicValidator supports only ValidationException and exception types, like EntityDataSourceValidationException, that implement the IDynamicValidatorException interface. Because AggregateException used in this example does not implement this interface, the DynamicValidator controls simply ignore it and let the ASP.NET runtime to generate a yellow page of death. To handle AggregateException and other types of expected exceptions your business layer may throw, you need to subclass the DynamicValidator control and override its ValidateException method.

When overriding the ValidateException method, remember that a single web page can contain a number of dynamic validators. The validators created by field templates are associated with specific entity properties (for these controls, the Column property defined in the DynamicValidator base class returns a MetaColumn object describing their entity property). These validators should report only the exceptions related to their respective entity properties. However, the validator at the top of the page is not associated with any particular entity property (its Column property is null) and should report only the exceptions related to the entire entity.

The ValidationException class used in this example allows you to determine if an error is related to a particular entity property by examining its ValidationResult. The MemberNames property of the ValidationResult can be empty if the error is not related to any particular entity property or contain multiple property names depending on how the validation logic was implemented by the entity class.

For complete details on how to extend the DynamicValidator control and implement support for AggregateException that contains multiple ValidationException instances, please refer to the UnleashedValidator control in the sample solution accompanying this book. Figure 8.10 shows how multiple validation errors are reported in the sample web application where all field and page templates have been modified to use the UnleashedValidator control instead of the built-in DynamicValidator.